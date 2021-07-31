---
type: docs
title: "Ready?"
linkTitle: "Ready?"
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

 - [Visual Studio Code](https://code.visualstudio.com/)
   - Confirm with `code --version`
 - For Windows
   - [nvm-windows, node.js, and npm](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows)
   - Confirm with:
     - `TODO: nvm --version, right?`
 - For Mac
   - [nvm, node.js and npm](https://nodesource.com/blog/installing-node-js-tutorial-using-nvm-on-mac-os-x-and-ubuntu/)

## Some miscellaneous stuff about removing node.exe from Windows

https://stackoverflow.com/questions/20711240/how-to-completely-remove-node-js-from-windows

~~~
tasklist | find /i "node"

c:\Program Files\nodejs
    C:\Program Files (x86)\Nodejs
    C:\Program Files\Nodejs
    C:\Users\{User}\AppData\Roaming\npm (or %appdata%\npm)
    C:\Users\{User}\AppData\Roaming\npm-cache (or %appdata%\npm-cache)
    C:\Users\{User}\.npmrc (and possibly check for that without the . prefix too)
    C:\Users\{User}\AppData\Local\Temp\npm-*
dir %appdata%\..\local\temp\npm*

~~~

Don't forget Windows uninstall.