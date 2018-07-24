# nwjs_templates

This is a template for starting an NWJS project.  It is a two-tiered implementation where manifests for installing the app, and running the app are separate.  I recommend this approach as it keeps modules required only for installing from being bundled in the build.

## Quick Start

Clone or [download](https://github.com/Allasso/nwjs_templates/archive/master.zip) this repository.

Example:

```
git clone https://github.com/Allasso/nwjs_templates.git
cd nwjs_templates
npm install
```

To run for development:

```
npm run dev
```

To build for production:

```
npm run prod
```

As is, this will create a build for OS X.  To create builds for other platforms, edit the following line in package.json in the root directory:

```
"prod": "nwbuild --platforms osx64 --buildDir dist/ src"
```

and add/remove comma separated platform keys, eg, to create builds for all available platforms,

```
"prod": "nwbuild --platforms win32,win64,osx64,linux32,linux64 --buildDir dist/ src/"
```

Builds will be placed in a newly created "dist" directory.  A full path will be printed when the build is finished.

## Other Info

In its basic form, the root directory contains a package.json file, and a src directory.  The src directory contains all files pertaining to your app, and also another package.json file.

Note that there are 2 package.json files.  The root package.json file contains manifest data for __installing__ the app, while src/package.json contains manifest data for __running__ your app.

The root manifest:

```
{
  "name": "NWJSTemplate2level",
  "description": "Template (2 level) for making NWJS apps.",
  "version": "0.0.1",
  "scripts": {
    "start": "nw src",
    "dev": "nw src",
    "prod": "nwbuild --platforms osx64 --buildDir dist/ src"
  },
  "devDependencies": {
    "nw": "^0.30.2",
    "nw-builder": "^3.1.2"
  }
}
```

"name" and "version" are minimum requirement.  If not passed as arguments in the install command, "devDependencies": "nw" is required to run the app, while "devDependencies": "nw-builder" is required to build the app.  "scripts" provide mapping for commands for running and building the app.

The src directory contains an html file structure just as you would set up on a website.

In addition it contains the manifest file for running your app:

```
{
  "name": "NWJSTemplate2level",
  "description": "Template (2 level) for making NWJS apps.",
  "version": "0.0.1",
  "main": "html/main.html",
  "window": {
    "toolbar": false,
    "width": 660,
    "height": 500
  }
}
```

The src/package.json file also requires "name" and "version".  It also requires a "main" entry, which will be the path to the file that should be executed when the app starts.  The path is relative to the src directory.  Additional data may be provided for initializing the app.  You may find documentation on that [here](http://docs.nwjs.io/en/latest/References/Manifest%20Format/).  Note that the documentation refers to a single-tiered implementation where the manifests for installing and running the app are combined in a single package.json file.
