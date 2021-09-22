---
type: docs
title: "List Movies"
linkTitle: "List Movies"
weight: 020
description: >
  Let the theater managers see the movie list.
---

Create `color-theatermanagement-bff\test\Dii_TheaterManagement_Bff.Acceptance.Tests\Features\ViewMovies.feature`
~~~
Feature: ViewMovies
	View the list of movies

Background:
    Given the following movies
    | Title                                          |
    | Solo: A Star Wars Story                        |
    | Rogue One: A Star Wars Story                   |
    | Star Wars: Episode I - The Phantom Menace      |
    | Star Wars: Episode II - Attack of the Clones   |
    | Star Wars: Episode III - Revenge of the Sith   |
    | Star Wars: Episode IV - A New Hope             |
    | Star Wars: Episode IX - The Rise of Skywalker  |
    | Star Wars: Episode V - The Empire Strikes Back |
    | The Star Wars Holiday Special                  |
    | Star Wars: Episode VI - Return of the Jedi     |
    | Star Wars: Episode VII - The Force Awakens     |
    | Star Wars: Episode VIII - The Last Jedi        |
    | The Star Wars Holiday Special                  |

@mytag
Scenario: The title can be seen
	When I view the list of movies
	Then the movie list should show
        | Title                                          |
        | Solo: A Star Wars Story                        |
        | Rogue One: A Star Wars Story                   |
        | Star Wars: Episode I - The Phantom Menace      |
        | Star Wars: Episode II - Attack of the Clones   |
        | Star Wars: Episode III - Revenge of the Sith   |
        | Star Wars: Episode IV - A New Hope             |
        | Star Wars: Episode IX - The Rise of Skywalker  |
        | Star Wars: Episode V - The Empire Strikes Back |
        | The Star Wars Holiday Special                  |
        | Star Wars: Episode VI - Return of the Jedi     |
        | Star Wars: Episode VII - The Force Awakens     |
        | Star Wars: Episode VIII - The Last Jedi        |
        | The Star Wars Holiday Special                  |
~~~

Right-click on the feature file and choose "Generate Step Definitions".

Generate all steps into the class `BookingSteps`. (Note that that name is different than the default class name.)

Choose the `Steps` directory as the target.

Notice that the generated steps all say...

~~~
ScenarioContext.Current.Pending();
~~~

...because we haven't yet coded the steps.

Add a constructor to you class like so:

~~~
...
        private readonly Driver _driver;
        private readonly HttpClient _client;
        private List<Movie> _moviesViewed;

        public BookingSteps(Driver driver)
        {
            _driver = driver;
            _client = driver._client;
        }
...
~~~

In your Given step, add this code to let the driver do the database work:

~~~
        [Given(@"the following movies")]
        public void GivenTheFollowingMovies(Table table)
        {
            _driver.AddMoviesToDatabase(table);
        }
~~~

Use the "Generate method" fix to generate the `AddMoviesToDatabase` in the `Driver` class and use this code:

~~~
        internal void AddMoviesToDatabase(Table table)
        {
            // Note that we assume the specified movies are already in the seed data.
        }
~~~

In your When step, add this code to change the method to `async` and to perform the action that is being tested:

~~~
        [When(@"I view the list of movies")]
        public async Task WhenIViewTheListOfMoviesAsync()
        {
            var response = await _client.GetAsync("/api/movies");

            // Get the response
            var json = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
            Console.WriteLine("Your response data is: " + json);

            // Save the result so we can inspect it later.
            _moviesViewed = JsonConvert.DeserializeObject<List<Movie>>(json);
        }
~~~

In your Then step, add this code to confirm the expected ourcome:

~~~
        [Then(@"the movie list should show")]
        public void ThenTheMovieListShouldShow(Table table)
        {
            var expectedMovies = table.CreateSet<MovieView>();

            var expectedTitles = expectedMovies.Select(em => em.title);
            var actualTitles = _moviesViewed.Select(am => am.Title);

            actualTitles.Should().Contain(expectedTitles);
        }
~~~
