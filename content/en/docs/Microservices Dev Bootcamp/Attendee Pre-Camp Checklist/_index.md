---
type: docs
title: "Attendee Pre-Camp Checklist"
linkTitle: "Attendee Pre-Camp Checklist"
weight: 005
description: >
  Make sure you have everything you need to begin bootcamp.
---

{{% alert title="Sorry, Steve and Linus" color="warning" %}}
This training module assumes you're running Windows. Along the way we might
also include some info for you Mac/Linux people, but mostly
you're on your own.
{{% /alert %}}

## Software you'll need

### Visual Studio Code

 - [Visual Studio Code](https://code.visualstudio.com/)
   - Confirm with `code --version`
   - Extension: [GitHub Pull Requests and Issues](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
   - Extension: [Azure Static Web Apps](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps)
   - Extension: [Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
   - Extension: [Terminals Manager](https://marketplace.visualstudio.com/items?itemName=fabiospampinato.vscode-terminals)

### nvm, node and npm

We're going to run a specific version of `node`. (See the next section, "Switch node to version 12.22.4".)

Since you might want to run other versions
of `node` on other projects, we're going to use `nvm`, the [Node Version Manager](https://github.com/nvm-sh/nvm)
to make it easy to switch between versions.

Before proceeding, check to see if you already have `nvm` installed by running this command:

~~~
nvm version
~~~

If it tells you a version number, you've already got `nvm` which means you've got `node` and `npm` as well,
so you can skip to the next section, "Switch node to version 12.22.4".

{{% alert title="Special note for current Windows node users" color="info" %}}
As you perform the steps below you'll be instructed to fully remove `node` from your system before
installing `nvm-windows`. Here are some suggestions that will help you make sure you fully remove everything:

 1. https://stackoverflow.com/questions/20711240/how-to-completely-remove-node-js-from-windows
 2. Don't forget Windows uninstall.
 3. Be sure to check these locations:
~~~
C:\Program Files\nodejs
C:\Program Files (x86)\Nodejs
C:\Program Files\Nodejs
C:\Users\{User}\AppData\Roaming\npm (or %appdata%\npm)
C:\Users\{User}\AppData\Roaming\npm-cache (or %appdata%\npm-cache)
C:\Users\{User}\.npmrc (and possibly check for that without the . prefix too)
C:\Users\{User}\AppData\Local\Temp\npm-*
%appdata%\..\local\temp\npm*
~~~
{{% /alert %}}

To install nvm-windows (or nvm), node.js, and npm:
   - [Windows instructions](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows)
   - [Mac/Linux instructions](https://nodesource.com/blog/installing-node-js-tutorial-using-nvm-on-mac-os-x-and-ubuntu/)

Confirm installation with:
~~~
nvm version
node -v
npm version
~~~

### Switch node to version 12.22.4

Run these commands:
~~~
nvm install 12.22.4
nvm use 12.22.4
~~~
 
Confirm switch with:
~~~
node -v
~~~

### Install global node packages

Run these commands:
- `npm install -g @azure/static-web-apps-cli`
- `npm install -g azure-functions-core-tools@3`

### GitHub CLI

Installation instructions for [GitHub CLI](https://github.com/cli/cli):
 - [For Windows](https://github.com/cli/cli#windows)
 - [For macOs](https://github.com/cli/cli#macos)
 - [For Linux](https://github.com/cli/cli#linux)

### Visual Studio

### Docker Desktop

 - You'll want to add `C:\src\onbe` as a file sharing resource.

**Settings** > **Resources** > **File Sharing** > **⊕** >> ...

