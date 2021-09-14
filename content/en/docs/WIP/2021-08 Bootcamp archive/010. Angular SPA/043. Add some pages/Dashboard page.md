---
type: docs
title: "Dashboard page"
linkTitle: "Dashboard page"
weight: 20
description: >
  Add a Dashboard page.
---

## Create a branch

`feature/dashboard-page`

### Add the dashboard

~~~
npx ng generate component areas/dashboard/pages/dashboard
~~~

...which may be abbreviated to...

~~~
npx ng g c areas/dashboard/pages/dashboard
~~~

At this point we'd inspect the changes made to:

~~~
app.module.ts
src\app\areas\dashboard\pages\movie-list\dashboard.component.html
src\app\areas\dashboard\pages\movie-list\dashboard.component.scss
src\app\areas\dashboard\pages\movie-list\dashboard.component.spec.ts
src\app\areas\dashboard\pages\movie-list\dashboard.component.ts
~~~

Commit with comment "ng g c dashboard"

~~~
<div class="container">
  <app-dashboard></app-dashboard>
</div>
~~~

### Add the dashboard root

TODO: Copy the instructions from https://angular.io/tutorial/toh-pt5#add-the-dashboard-route

Begin TODO: Discuss the difference between `src\app\app.component.html` being this...

~~~
<div class="container">
  <app-dashboard></app-dashboard>
</div>
~~~

...and `src\app\app.component.html` being this...

~~~
<router-outlet></router-outlet>
~~~

End TODO:

Edit `src\app\app-routing.module.ts`

~~~
import { DashboardComponent } from './areas/dashboard/pages/dashboard/dashboard.component';
import { PageNotFoundComponent } from './areas/404/pages/page-not-found/page-not-found.component';
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  {path: '' , component: DashboardComponent  },
  {path: '404', component: PageNotFoundComponent},
  {path: '**', redirectTo: '/404'}

];
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
~~~





### Deploy

Commit with comment "Dashboard is now the default page"

Push, create a pull request, complete the pull request and delete the branches.
