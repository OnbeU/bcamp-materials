---
type: docs
title: "Instructor Notes"
linkTitle: "Instructor Notes"
weight: 003
description: >
  You'll want to read these if you're leading the bootcamp.
---

## Attendee repos, etc. setup

### Create feature branch

feature/attendee-setup

### bc000-theatermanagement-spa

Create repo in GitHub.

.gitignore
~~~
/dist
/node_modules
.vscode
.DS_Store
Thumbs.db
~~~

~~~
npm init
~~~

~~~
npm install -D copyfiles http-server
~~~

package.json
~~~
{
  "name": "project",
  "version": "0.0.0",
  "scripts": {
    "start": "http-server .",
    "build": "copyfiles index.html dist/project/.",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "devDependencies": {
    "copyfiles": "^2.4.1",
    "http-server": "^0.12.3"
  }
}
~~~

index.html
~~~
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=yes">

    <title>Hello World!</title>
</head>

<body>
    Hello World!
</body>

</html>
~~~

TODO: Add more steps.

Lock down main.

 - Settings | Branches | Add rule
 - Branch name pattern: main
 - Require pull request reviews before merging: true
 - Include administrators: False

