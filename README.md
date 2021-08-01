## How we set up hugo (actually hugo-extended)

Made sure that `.gitignore` included these lines:

~~~
.vs/
.vscode/
build
node_modules/
public/
resources/
~~~

Ran these commands:

~~~
npm init
~~~

Used these options for `init`:
 - package name: (project) onbe-bootcamp-training-materials
 - description: Onbe Bootcamp Training Materials
 - license: (ISC) UNLICENSED

Ran these commands:

~~~
npm install -D shx
npm install -D autoprefixer
npm install -D postcss-cli
npm install -D hugo-extended
npm install postcss
~~~

(Note that `npm install postcss` does not have a `-D` because 
[Hugo needs it in order to run on the GitHub build server]()https://github.com/google/docsy/issues/235.)

Edited `package.json` to remove some features we don't want:
  - `"main": "index.js",`

Added some scripts to our `package.json`,
per "[Deploying a static website to Azure Storage using Azure DevOps](https://www.blogtrack.io/blog/powerful-blog-setup-with-hugo-and-npm/#polishing-the-project)":

    {
      ...
      "scripts": {
        "build": "npm run submodule:build && npm run hugo:build",
        "clean": "npm run hugo:clean",
        "serve": "npm run hugo:serve",
        "submodule:build": "git submodule update --init --recursive --depth 1",
        "hugo:build": "hugo -d build",
        "hugo:serve": "hugo server",
        "hugo:clean": "shx rm -rf build resources/_gen public dist && shx echo Done",
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      ... 
    }

Since we want to use Docsy as a submodule, we did this:

~~~
git submodule add https://github.com/google/docsy.git themes/docsy
git submodule update --init --recursive
~~~

## How to build, clean and serve

    npm run build

    npm run clean

    npm run serve
