---
type: docs
title: "Instructor Notes"
linkTitle: "Instructor Notes"
weight: 003
description: >
  You'll want to read these if you're leading the bootcamp.
---

## Attendee repos, etc. setup

### bc000-admin-spa

Create repo in GitHub.

~~~
npm init
~~~

~~~
npm install -D shx copyfiles
~~~

package.json
~~~
{
  "name": "project",
  "version": "0.0.0",
  "scripts": {
    "build": "copyfiles index.html dist/project/.",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "devDependencies": {
    "copyfiles": "^2.4.1"
  }
}
~~~

.gitignore
~~~
/dist
/node_modules
.vscode
.DS_Store
Thumbs.db
~~~

index.html
~~~
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport"
      content="width=device-width, initial-scale=1, user-scalable=yes">
  
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

