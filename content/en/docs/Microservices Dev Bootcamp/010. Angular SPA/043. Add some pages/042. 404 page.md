---
type: docs
title: "404 page"
linkTitle: "404 page"
weight: 42
description: >
  Add a 404 page.
---

## Create a branch

`feature/404-page`

### Add the 404

~~~
npx ng generate component areas/404/pages/page-not-found
~~~

...which may be abbreviated to...

~~~
npx ng g c areas/404/pages/page-not-found
~~~

At this point we'd inspect the changes made to:

~~~
app.module.ts
src\app\areas\404\pages\page-not-found\page-not-found.component.html
src\app\areas\404\pages\page-not-found\page-not-found.component.scss
src\app\areas\404\pages\page-not-found\page-not-found.component.spec.ts
src\app\areas\404\pages\page-not-found\page-not-found.component.ts
~~~

Commit with comment "ng g c page-not-found"

Edit `src\app\app-routing.module.ts`

~~~
import { PageNotFoundComponent } from './areas/404/pages/page-not-found/page-not-found.component';
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  {path: '404', component: PageNotFoundComponent},
  {path: '**', redirectTo: '/404'}

];
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
~~~

TODO: Might need to change the above so there's a default page.

Commit with comment "Redirection to /404"

Download the file at https://i.imgur.com/qhMbkGi.jpg to `project\src\assets\images\confused-travolta.gif`

Change the contents of `src\app\areas\404\pages\page-not-found\page-not-found.component.html` to:

~~~
<h1 align="center">Page Not Found</h1>
<div class="text-center">
  <img src="./assets/images/confused-travolta.gif"/>
</div>
~~~

TODO: Discuss the removal of `project\src\assets\.gitkeep`




### Deploy

Commit with comment "Confused Travolta"

Push, create a pull request, complete the pull request and delete the branches.
