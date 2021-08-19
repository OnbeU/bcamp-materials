---
type: docs
title: "Header"
linkTitle: "Header"
weight: 30
description: >
  Add a header.
---

## Create a branch

`feature/header`

### Add a header

~~~
npx ng generate component areas/app/header
~~~

...which may be abbreviated to...

~~~
npx ng g c areas/app/header
~~~

At this point we'd inspect the changes made to:

~~~
app.module.ts
src\app\areas\dashboard\pages\movie-list\dashboard.component.html
src\app\areas\dashboard\pages\movie-list\dashboard.component.scss
src\app\areas\dashboard\pages\movie-list\dashboard.component.spec.ts
src\app\areas\dashboard\pages\movie-list\dashboard.component.ts
~~~

Commit with comment "ng g c header"

Change `src\app\areas\app\header\header.component.html` to:
~~~
<header>
  <nav class="navbar navbar-expand navbar-dark bg-primary border-bottom box-shadow mb-3">
      <a class="navbar-brand" href="/">boulevard</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
      </button>
      <div class="navbar-collapse collapse d-sm-inline-flex flex-sm-row-reverse" id="navbarNavAltMarkup">
          <div class="navbar-nav">
              <a class="nav-link text-light bg-primary" title="Profile" href="/Account">
                  Signed in as Alice Brooks
              </a>
              <a class="nav-link text-light bg-primary" title="Logout" href="/Account/Logout">Log Out</a>
          </div>
          <div class="navbar-nav flex-grow-1">
              <a class="nav-link text-light bg-primary" routerLink="/movies">Movies</a>
          </div>
      </div>
  </nav>
</header>
~~~

Change `app.component.html` to:
~~~
<div>
  <app-header></app-header>
</div>

<router-outlet></router-outlet>
~~~

Commit with comment "Site now shows the header"

### Fix the warning that came from adding the header

In the Terminal window that's running Karma you might see the following:

~~~
ERROR: 'NG0304: 'app-header' is not a known element:
1. If 'app-header' is an Angular component, then verify that it is part of this module.
2. If 'app-header' is a Web Component then add 'CUSTOM_ELEMENTS_SCHEMA' to the '@NgModule.schemas' of this component to suppress this message.'
~~~

There's nothing really wrong; it's just that one of the tests can't find the new header component.

Add an import for `FormsModule` and a declaration for `HeaderComponent` to `src\app\app.component.spec.ts` like so:

~~~
...
    await TestBed.configureTestingModule({
      imports: [
        FormsModule,
        RouterTestingModule
      ],
      declarations: [
        AppComponent,
        HeaderComponent
      ],
...
~~~

Commit with the comment "Fixed error NG0304.".

### Deploy

Push, create a pull request, complete the pull request and delete the branches.
