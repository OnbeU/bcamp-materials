---
type: docs
title: "Onbe Angular repo structure"
linkTitle: "Onbe Angular repo structure"
description: >
  Onbe Angular repo structure.
---

## Structure

```
<repo root>/                                 // Root of your repository
|- README.md                                 // Repo-level README
|- readme/                                   // Supplemental files for repo-level README
|- project                                   // Root of your Angular project
   |- .gitignore                             // Ignore dist, node_modules, etc.
   !- <other standard Angular files>         // angular.json, package.json, etc.
   |- e2e/                                   // End-to-end testing (for local development & build)
   |- src/                                   // Source code of your Angular project
      |- app/
         |- README.md                        // App-level README
         |- readme/                          // Supplemental files for app-level README
         |- app.module.ts
         |- app-routing.module.ts
         |- areas/                           // An Area is a high-level group for Pages
            |- heroes/                       // An example of an area
               |- heroes.module.ts
               |- heroes-routing.module.ts
               |- components                 // Components for this area
                  |- heroes-list-item/
                     |- heroes-list.component.ts, ...
               |- pages                      // A page is a Pomponent that has routing
                  |- hero-create/
                     |- hero-create.component.ts, ...
                  |- hero-detail/
                     |- hero-detail.component.ts, ...
                  |- hero-delete/
                     |- hero-delete.component.ts, ...
                  |- heroes-list/
                     |- hero-delete.component.ts, ...
            |- 404/                          // Best practice: Provide a 404 page
               |- 404.module.ts
               |- 404-routing.module.ts
                  |- pages/
                     |- page-not-found/
                        |- page-not-found.component.ts, ...
            |- app/                          // A special area for app.component
               |- components/                // Components used only by app.component
                  |- header/
                     |- header.component.ts, ...
                  |- nav-bar/
                     |- nav-bar.component.ts, ...
               |- components                 // Components for this area
                  |- heroes-list-item/
                     |- heroes-list.component.ts, ...
            |- <some-other-area>
               |- components/
                  |- ...
               |- pages/
                  |- ...
         |- reusable/                        // Modules that can be reused in other projects
            |- spinner/                      // Example of a reusable module
               |- spinner.module.ts
               |- index.ts
               |- spinner/
                  |- spinner.component.ts, ...
         |- shared/                          // Shared throughout the app
            |- components/                   // Components shared throughout the app
               |- <some-component>
                  |- <some-component>.component.ts, ...
            |- directives/                   // Directives shared throughout the app
               |- <some-directive>
                  |- <some-directive>.directive.ts, ...
            |- guards/                       // Guards shared throughout the app
               |- <some-guard>
                  |- <some-guard>.guard.ts, ...
            |- pipes/                        // Pipes shared throughout the app
               |- <some-pipe>
                  |- <some-pipe>.pipe.ts, ...
         |- core/
            |- singleton-services            // Singleton services
               |- backend-api/               // Example of a singleton service
                  |- backend-api.service.ts, ...
                  |- hero.ts                 // Example of a model
                  |- city.ts                 // Example of a model
   |- assets/
      |- images/                             // Example of a directory of assets
         |- logo.jpg                         // Example of an asset
   |- environments/
      |- environment.prod.ts
      |- environment.prod.ts
|- dev/                                      // Projects to assist in development
   |- fake-backend-server\                   // Example of a project for development
      |- ...
   |- <some-other-dev-project>\
      |- ...
```

## Explanation of directories

### ./project/
### ./project/e2e/
### ./project/src/
### ./project/src/app/areas/
### ./dev/

## Other important standards 

### Cyrille Tuzi

Cyrille Tuzi’s
[Architecture in Angular projects]([Cyrille Tuzi’s Architecture in Angular projects](https://medium.com/@cyrilletuzi/architecture-in-angular-projects-242606567e40))
is similar to Onbe’s approach, with a few differences.

Tuzi places places the app’s pages into an app-level directory
(e.g. `app/heroes/`), where we place these directories one level 
deeper under an areas directory (e.g. `app/areas/heroes/`) 
to avoid confusion with other app-level directories
(such as `app/core/`).

