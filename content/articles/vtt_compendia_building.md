---
title: "Building Compendia for Foundry VTT"
date: 2020-09-07
thumbnail: "articles/compendia_gulpfile.png"
categories: ["Software"]
tags: ["Foundry VTT", "Programming", "Virtual Tabletop"]
draft: false
---

## Creating A Compendium

From the [official Knowledge Base](https://foundryvtt.com/article/compendium/) and the [community web site](https://foundry-vtt-community.github.io/), there are two explanations given on how to create a compendium for [Foundry VTT](https://foundryvtt.com/), others are often discussed on the Discord server. The first, and most obvious, is to create it manually within a game world, but this has several limitations: it's slow and time consuming to create and edit once created, and (without some jiggery-pokery) the compendium is bound to that particular world and not easily re-used across several game worlds.

The second way is to record the data for the compendium as JSON files (conforming to the schema for items in a particular game system), and import the data using a macro. This is more flexible than the manual method because that same data can be imported into several game worlds and re-imported when changes are made, but it still has it's issues, the main one being that using a macro seems very "hackey" and a misuse of the macro API.

What I was looking for was a way to quickly create several compendia from easily edited raw data and compile the compendia into a module which could then be used in any game world simply by installing and enabling the module in the world settings.

# A Note About Foundry VTT "Databases"

If you take a look at a `.db` file in Foundry (check the world folders and you'll see a few), you will see that while they're called *databases* the contents are basically a list of JSON objects. The NodeJS/JavaScript module used to manage these databases is called [NEDB](https://stackabuse.com/nedb-a-lightweight-javascript-database/), which has a MongoDB-like API but manages databases kept in memory or on disk.

So, inspired by some of the chatter on Discord from **@Spacemandev** and **@Spice_King**, it occurred that one way of creating compendia outside of Foundry but retain compatibility with Foundry is to use a Gulp script and NEDB to build the compendia from raw data files. Although there's heated discussion on the topic, the format I chose for the data files was YAML rather than JSON, simply because YAML is a readily parseable, structured format but is easier to manually edit (fewer open and close quotes and no brackets).

## Project Structure

After some experimentation, I had a project structure that looked something like this:

```
.
├── package.json
├── gulpfile.js
├── .nvmrc
├── .gitignore
├── src
│   ├── module.json
│   └── assets
│       └── icons
│           └── broadsword.png
│       └── images
│       └── maps
│       └── portraits
│   └── packs
│       └── equipment
│           └── broadsword.yml
│           └── mace.yml
│           └── backpack.yml
│       └── spells
│           └── magic_missile.yml
│       └── prayers
│       └── npcs
│       └── tables
│           └── encounters.yml
├── build
├── dist
```

`package.json` is the standard NodeJS package declaration, before running the Gulp script you'll need to create one for your project and add the required modules you see at the top of the script (except for `fs` and `path` which are built-in modules). `.gitignore` should ignore the `node_modules`, `build` and `dist` folders so that any development dependencies or generated files are kept out of source control. `.nvmrc` is there because I use multiple versions of NodeJS for different work and having a `.nvmrc` file means I can just type `nvm use && gulp` to start development with the correct version. `src/module.json` is the standard module declaration file for a Foundry VTT module.

When the build is run, any folder underneath `src/packs` will become a compendium database with the same name as the folder: `src/equipment` becomes `packs/equipment.db` in the `build` folder, for example. Each YAML file within a folder becomes an entry in the compendium database. You can create new compendia by creating new folders and copy or move the YAML files around as you see fit. `assets` includes any additional files for the module, such as images and icons for compendia entries 

Compendia must be declared in the `module.json` file `packs` section, like this:

```json
  "packs": [
    {
      "name": "equipment",
      "label": "Equipment",
      "path": "/packs/equipment.db",
      "entity": "Item"
    },
    {
      "name": "spells",
      "label": "Spells",
      "path": "/packs/spells.db",
      "entity": "Item"
    }
```

Each YAML file contains the data for an individual compendium entry. The first few lines (name, type, img) are consistent for all Foundry types; add whatever data is required for your game system's schema under the `data`section - make sure you use the correct YAML indentation though. If you're unsure what that data should look like, just create an item manually then export the data as JSON using the Foundry menus, then run it through a JSON to YAML converter such as https://www.json2yaml.com/.

```yaml
name: "Broadsword"
type: weapon
img: modules/compendia/icons/broadsword.png
data:
    ...:
```

Note that you don't need certain fields in your raw data as they're intended for *internal* use by Foundry, such as the `_id` field - that will be created for you automatically by NEDB when it creates a new database entry.

## Gulp Script 

And finally, here's the Gulp script used to generate the final module.

```javascript
const gulp = require("gulp");
const through2 = require("through2");
const yaml = require("gulp-yaml");
const Datastore = require("nedb");
const cb = require("cb");
const mergeStream = require("merge-stream");
const clean = require("gulp-clean");
const zip = require("gulp-zip");
const fs = require("fs");
const path = require("path");

const MODULE = JSON.parse(fs.readFileSync("src/module.json"));
const STATIC_FILES = ["src/module.json", "src/assets/**/*"];
const PACK_SRC = "src/packs";
const BUILD_DIR = "build";
const DIST_DIR = "dist";

/* ----------------------------------------- */
/*  Compile Compendia
/* ----------------------------------------- */

function compilePacks() {
  // determine the source folders to process
  const folders = fs.readdirSync(PACK_SRC).filter((file) => {
    return fs.statSync(path.join(PACK_SRC, file)).isDirectory();
  });

  // process each folder into a compendium db
  const packs = folders.map((folder) => {
    const db = new Datastore({ filename: path.resolve(__dirname, BUILD_DIR, "packs", `${folder}.db`), autoload: true });
    return gulp
      .src(path.join(PACK_SRC, folder, "/**/*.yml"))
      .pipe(yaml({ space: 0, safe: true, json: true }))
      .pipe(
        through2.obj((file, enc, cb) => {
          db.insert(JSON.parse(file.contents.toString()));
          cb(null, file);
        })
      );
  });
  return mergeStream.call(null, packs);
}

/* ----------------------------------------- */
/*  Copy static files
/* ----------------------------------------- */

function copyFiles() {
  return gulp.src(STATIC_FILES).pipe(gulp.dest(BUILD_DIR));
}

/* ----------------------------------------- */
/*  Create distribution archive
/* ----------------------------------------- */

function createZip() {
  return gulp
    .src(`${BUILD_DIR}/**/*`)
    .pipe(zip(`foundryvtt-${MODULE.name}-v${MODULE.version}.zip`))
    .pipe(gulp.dest(DIST_DIR));
}

/* ----------------------------------------- */
/*  Other Functions
/* ----------------------------------------- */

function cleanBuild() {
  return gulp.src(`${BUILD_DIR}`, { allowEmpty: true }, { read: false }).pipe(clean());
}

function watchUpdates() {
  gulp.watch("src/**/*", gulp.series(cleanBuild, copyFiles, compilePacks));
}

/* ----------------------------------------- */
/*  Export Tasks
/* ----------------------------------------- */

exports.clean = gulp.series(cleanBuild);
exports.compile = gulp.series(compilePacks);
exports.copy = gulp.series(copyFiles);
exports.build = gulp.series(cleanBuild, copyFiles, compilePacks);
exports.dist = gulp.series(createZip);
exports.default = gulp.series(watchUpdates);
```

## Development and Distribution Builds

While you're building the module, just type `gulp` at the command line and gulp will watch for any changes to files in the `src` folder and rebuild the compendia on-the-fly. What I generally do is to *symlink* the `build` folder to the `Data/modules` folder in my local Foundry setup, then I can edit and test the contents with a reload of the Foundry app.

If you want to create a distributable archive then use `gulp build` followed by `gulp dist`. The Gulp script will read the module name and version from the `module.json` file and create an appropriately named *zip* archive in the `dist` folder.

## Caveats

A couple of things I've found: Firstly, if you add a new compendia to the module (ie: a new data folder and entry in `module.json`) then you need to shutdown Foundry and restart it in order to pick up the change. Secondly, Foundry will see each of the compendia databases as a working database in the application and will modify the databases as you use the compendia, when you exit or reload Foundry it will compact those databases. Make sure you *Return to Setup* from the sidebar menu **before** you allow a rebuild or the databases you get may not be the ones you think you should get.

## Summary

That's about it. I've used this method a lot over the last week or so to create a few modules for different game systems I'm working on and have found it really quick and simple to use once set up.

One additional idea that I have yet to implement is that if you have items that you would like to use in several game systems, but obviously they have a different data model, then it should be possible to record the data in YAML in a "system-neutral" format and add a *convertor* function to the Gulp pipeline to take that generic data and convert it to a particular game system format before writing it to the compendia database. Ah well, maybe another day.