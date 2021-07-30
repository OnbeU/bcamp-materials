## How we set up hugo (actually hugo-extended)

Made sure that `.gitignore` included these lines:

~~~
project/build
project/node_modules/
project/public
project/resources/_gen
~~~

Ran these commands:

~~~
md project
cd project
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
~~~

Edited `package.json` to remove some features we don't want:
  - `"main": "index.js",`

Added some scripts to our `package.json`,
per "[Deploying a static website to Azure Storage using Azure DevOps](https://www.blogtrack.io/blog/powerful-blog-setup-with-hugo-and-npm/#polishing-the-project)":

    {
      ...
      "scripts": {
        "build": "npm run hugo:build",
        "clean": "npm run hugo:clean",
        "serve": "npm run hugo:serve",
        "hugo:build": "hugo -d build",
        "hugo:serve": "hugo server",
        "hugo:clean": "shx rm -rf build resources/_gen public dist && shx echo Done"
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
