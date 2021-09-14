---
type: docs
title: "Dynamic content"
linkTitle: "Dynamic content"
weight: 25
description: >
  Why be static when you can be dynamic?
---

## Create feature branch

feature/dynamic-content

## Update index.html

~~~
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=yes">
    <title>Let's Hear from the Backend</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.1/jquery.min.js"></script>
</head>

<body>
    <main>
        <h1>Movies</h1>
        <table id="movies" border='1'>
            <thead>
                <tr>
                    <th>id</th>
                    <th>title</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </main>

    <script>
        (async function () {
            const movies = await (await fetch('https://bootcampsharedbff.azurewebsites.net/movies')).json();

            var trHTML = '';

            movies.forEach(movie => {
                trHTML += '<tr><td>' + movie.id + '</td><td>' + movie.title + '</td></tr>';
            });

            $('#movies').append(trHTML);
        }())
    </script>
</body>

</html>
~~~

## Commit

Commit with "index.html is now dynamic"

## Don't create a PR yet!

Don't create a PR just yet. We've broken an important rule and we need to make things right.

What rule did we break? Here's a hint, from `index.html`:

~~~
            const movies = await (await fetch('https://bootcampsharedbff.azurewebsites.net/movies')).json();
~~~

{{% alert title="Hey, instructor!" color="primary" %}}
Now would be a good time for the "What Did We Do Wrong?" slide.
{{% /alert %}}
