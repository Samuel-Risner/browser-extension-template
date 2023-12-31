# browser-extension-template

A template for creating a browser extension (Firefox).

# Doing more

See https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json for a list of what can be added to the ```manifest.json``` file.

# Setup

To use this template you should reset/set some stuff:

## manifest.json

- set "name" to your extensions name
- set "description"
- set "homepage_url" to your repos readme

## package.json

- change the "name" to your extensions/repos name
- change the "description"
- under "repository" change the "url" to that of your repos
- change "author" to your name
- change "license" to your license
- under "bugs" change "url" to that of your repos
- change "homepage" to your repos readme

## package-lock.json

Delete this file and then run:

```shell
npm install
```

## LICENSE

- change the whole thing

or

- change the name
- change the date

## Remove .gitkeep files

- extension/css/dist/
- extension/js/dist/
- extension/icons/
- src/shared/

# How to add another content script (or something else that you want to build separately):

- decide on a name (```<name>```)
- go to the ```config``` folder
    - create a new folder with the name ```<name>```
    - copy ```tsconfig.json```, ```webpack.config.js``` and optionally ```tailwind.config.cjs``` from another folder to the newly created folder (```<name>```)
    - enter the newly created folder (```<name>```)
        - in ```tsconfig.json``` change:
            - ```"include": ["../../src/<name>/**/*.ts"],```
        - in ```webpack.config.js``` change:
            - ```entry: path.resolve(__dirname, "..", "..", "src", "<name>", "index.ts"),```
            - ```filename: "<name>.js",```
        - in ```tailwind.config.cjs``` change:
            - ```content: ["src/<name>/**/*.ts"],``` or
            - ```content: ["src/<name>/**/*.ts", "extension/html/<name>.html],"``` if you require an html file
- go to the ```extension``` folder
    - add your html file (if you have/need one) ```<name>.html``` to the folder ```html``` (you can use your script by using ```<script type="text/javascript" src="/js/dist/<name>.js"></script>``` and your css by using: ```<link href="/css/dist/<name>.css" rel="stylesheet">```)
    - add your script (and css) to the ```manifest.json``` file (you can link your script by using: ```js/dist/<name>.js``` and css by using ```css/dist/<name>.css```)
- go to the ```src``` folder
    - add the folder ```<name>``` and enter it
        - create the file ```index.ts``` inside that folder
- if you added a TailwindCSS config file:
    - go to the ```tw``` folder
    - create a new file called ```<name>.css```
    - add the contents of another file in that directory to the newly created file
- go to the ```package.json``` file and add the following scripts:
    - ```"build_wp_<name>": "webpack --config config/<name>/webpack.config.js",```
    - ```"watch_wp_<name>": "webpack --config config/<name>/webpack.config.js --watch",```
    - ```"build_tw_<name>": "tailwindcss -c ./config/<name>/tailwind.config.cjs -i ./tw/<name>.css -o ./extension/css/dist/<name>.css --minify",```
    - ```"watch_tw_<name>": "tailwindcss -c ./config/<name>/tailwind.config.cjs -i ./tw/<name>.css -o ./extension/css/dist/<name>.css --minify --watch",```
    - also add the newly created scripts to the ```build``` script

# How to remove one of the predefined configs

In the ```config``` folder are three other folders: ```background```, ```content``` and ```popup```.

Just walk through [adding another content script](#how-to-add-another-content-script-or-something-else-that-you-want-to-build-separately) backwards and use the folder names as ```<name>```.

# Build instructions

System requirements:

- Node v18.13.0
- npm 9.7.1

Install the required npm packages:

```shell
npm install
```

Run the build script to build everything:

```shell
npm run build
```

Or build single parts:

## extension/js/dist/content.js

The TypeScript source files are under ```src/content``` and ```src/shared``` and the config files are under ```config/content```.

Build script:

```shell
npm run build_wp_content
```

## extension/js/dist/popup.js

The TypeScript source files are under ```src/popup``` and ```src/shared``` and the config files are under ```config/popup```.

Build script:

```shell
npm run build_wp_popup
```

## extension/js/dist/background.js

The TypeScript source files are under ```src/background``` and ```src/shared``` and the config files are under ```config/background```.

Build script:

```shell
npm run build_wp_background
```
