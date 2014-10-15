---
layout: docs
navgroup: docs
navactive: docsgrunt
title: "Kickoff &#10084;'s Grunt"

meta:
  title: Grunt setup
  description: Read Kickoff's Grunt documentation

next:
 - title: Kickoff's CSS
   body: Find out how Kickoff's CSS works
   link: css.html
 - title: Kickoff's Javascript
   body: Find out how Kickoff's JS works
   link: js.html
---

Grunt is used extensively in Kickoff; It is the beating heart of the framework.

We use it to compile our Sass, concatinate and then minify our JavaScript files, or to fire up a simple local server with LiveReload for some testing.

Using Grunt has other benefits besides this.  It allows any dev to pick up a project, regardless of if they've worked on it before, and get up and running in no time.  It also helps to ensure the menial tasks that can sometimes be forgotten, are already configured when you are ready to deploy your site.


<hr class="sectionSplitter">

<a name="setup"></a>

## Setting up Grunt

Setting up Kickoff to use Grunt is extremely simple – just follow these simple steps:


#### Step 1 - Install Node
Download and install Node.js from [nodejs.org](http://nodejs.org/)


#### Step 2 - Install the Grunt CLI
In order to get started, you'll want to install Grunt's command line interface (CLI) globally.

Run `npm install -g grunt-cli` in your terminal or command shell. This will put the `grunt` command in your system path, allowing it to be run from any directory.

N.b. If you have any problems running the above command due to permission errors, you may need to use sudo (on OSX, *nix, BSD etc) or run your command shell as Administrator (on Windows).


#### Step 3 - Install Sass
Make sure you have Ruby v2 installed, then run `gem install sass` – or if you get a permission error, use `sudo gem install sass`.

You can also install the pre-release version of Sass using `gem install sass --pre`. This will install it globally on your machine so that Grunt has access to it.


#### Step 4 - Install LiveReload browser extension
In order to have your browser's styles refresh when a Sass file is modified, you will need to install the [LiveReload browser extension](http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-) – there are versions for Chrome, Safari and Firefox.


#### Step 5 - Get Kickoff
Download Kickoff using any of the options on the [Get Kickoff page](get.html).


#### Step 6 - Install Node dependencies
Grunt will not work without having installed it's dependencies. Kickoff's [package.json](https://github.com/tmwagency/kickoff/blob/master/package.json) uses a few essential Grunt plugins to operate.

To install them, use your terminal to `cd` into the root of the Kickoff directory, and then run `npm install`.  This will install all of the required dependencies to a new folder called `node_modules` inside your project.


#### Grunt is now setup!

<hr class="sectionSplitter">

<a name="tasks"></a>

## Kickoff’s Grunt tasks

Kickoff comes with a number of useful Grunt tasks configured for you to use.  These are tasks that you can run in the command line from the root directory of your Kickoff project.

Here is a guide to the tasks that are available and what each of them does.

---
<a name="grunt-default"></a>
#### grunt (the default task)

Running `grunt` will carry out the following tasks on your code:

* Runs [Shimly](#task-shimly) to compile together a small set of JavaScript shims to use in your project.
* [Uglify](#task-uglify) – minifies and concatinates your JavaScript files into one file
* [sass:kickoff](#task-sass) - compiles Kickoff’s Sass files into native CSS
* [autoprefixer:kickoff](#task-autoprefixer) – adds vendor prefixes to your CSS

---

<a name="grunt-start"></a>
#### grunt start

The very first grunt task you should run when starting a new Kickoff project.

This sets up all of Kickoff’s dependencies, spins up a local server and takes you to the Kickoff docs checklist so you can follow the guidelines for first steps when starting a Kickoff project.

---

<a name="grunt-dev"></a>
#### grunt dev

A task for development environments.  Compiles your code without minifying or optimising it.

Tasks carried out when **`grunt dev`** is run:

* [Shimly](#task-shimly)
* [Uglify](#task-uglify)
* [sass:kickoff](#task-sass) - compiles Kickoff’s Sass files into native CSS
* [autoprefixer:kickoff](#task-autoprefixer) – adds vendor prefixes to the CSS


---

<a name="grunt-deploy"></a>
#### grunt deploy

A task for production environments.

This task is essentially the same as **`grunt dev`** but minifies the CSS output as well ready for deployment on production environments.

Tasks carried out when **`grunt deploy`** is run:

* [Shimly](#task-shimly)
* [Uglify](#task-uglify)
* [sass:kickoff](#task-sass) - compiles Kickoff’s Sass files into native CSS
* [autoprefixer:kickoff](#task-autoprefixer) – adds vendor prefixes to the CSS
* [CSSO](#task-csso) – minifies CSS

---

<a name="grunt-serve"></a>
#### grunt serve

Running **`grunt serve`** creates a simple static server (using [grunt-contrib-connect](https://github.com/gruntjs/grunt-contrib-connect) via [grunt-browser-sync](https://github.com/shakyShane/grunt-browser-sync)) for previewing your work.

This task will open your defaut browser and enable Livereload so that CSS changes are updated when you edit your Sass.  Because Kickoff uses BrowserSync, it also keeps all of your devices in sync when connected to your local server (see [BrowserSync’s feature list for more details](https://github.com/shakyShane/browser-sync#features))

Tasks carried out when **`grunt serve`** is run:

* [Shimly](#task-shimly)
* [Uglify](#task-uglify)
* [sass:kickoff](#task-sass) - compiles Kickoff’s Sass files into native CSS
* [autoprefixer:kickoff](#task-autoprefixer) – adds vendor prefixes to the CSS
* [BrowserSync](#task-browsersync) – Starts local server available across multiple devices
* [Watch](#task-watch) – watches for code changes and reacts to them on save

---

<a name="grunt-watch"></a>
#### grunt watch

For documentation on the `grunt watch` task, [check out this section in the Kickoff task index](#task-watch)

---

<a name="grunt-icons"></a>
#### grunt icons

A task to help you create and maintain icons using Grunticon.

Running `grunt icons` carries out the [svgmin](#task-svgmin) and [Grunticon](#task-grunticon) tasks,
generating a set of icons for you to use in the front-end of your project.

<hr>
<a name="grunt-checks"></a>
#### grunt checks

A task to help you validate your code.

Running `grunt checks` will run the [JSHint](#task-jshint) task to check the projects JavaScript for errors and formatting inconsistencies.

We plan to expand on the checks carried out using this task in future versions of Kickoff.

<hr class="sectionSplitter">
<a name="config"></a>
## Kickoff config variables

Kickoff’s Grunt config variables allow you to control some of the basic settings of your Kickoff project.

Here we take a look at it’s structure and what each part controls.

<a name="config-structure"></a>
### Config structure

Kickoff’s config variables can be [found in the `Gruntfile.js` file in the root of a Kickoff project](https://github.com/tmwagency/kickoff/blob/master/Gruntfile.js#L8-L58), and looks like the following snippet of code:

```js
/**
 * Grunt global vars
 * Many of the Grunt tasks use these vars
 */
config : {
	src: "_grunt-configs/*.js",

	css : {
		distDir : 'css',     // <%=config.css.distDir%>
		srcFile : 'kickoff', // <%=config.css.srcFile%>
		scssDir : 'scss'     // <%=config.css.scssDir%>
	},

	js : {
		distDir  : 'js/dist/',   // <%=config.js.distDir%>
		distFile : 'app.min.js', // <%=config.js.distFile%>

		// <%=config.js.fileList%>
		fileList : [
			// if you would like to remove jQuery from your concatenated JS, comment out the line below
			'bower_modules/jquery/dist/jquery.js',

			// if you would like some basic JS shims (when not using jQuery),
			// uncomment the line below to compile Shimly output
			//'js/helpers/shims.js',

			'js/helpers/console.js',
			'bower_modules/trak/dist/trak.js',
			'bower_modules/swiftclick/js/libs/swiftclick.js',
			'bower_modules/cookies-js/src/cookies.js',

			'js/script.js'
		]
	},

	localserver: 'kickoff.dev', // <%=config.localserver%>

	testing: {
		visual : {
			sizes: [ '600', '1000', '1200' ], // <%=config.testing.visual.sizes%>

			// <%=config.testing.visual.urls%>
			urls : [
				'http://localhost:3000',
				'http://localhost:3000/_docs/',
				'http://localhost:3000/_docs/styleguide.html'
			]
		}
	}
}
````

<a name="taskindex"></a>
 ### Breaking this down

<a name="config-src"></a>
#### config.src

The first line you encounter in the Grunt config is the `config.src` variable.

	src: "_grunt-configs/*.js"

This is used to specify the path at which the rest of your Grunt config lives.  The default location for this is in the `_grunt-configs` folder, but if you’d like to rename or move this folder for any reason, make sure that you update this value in the config as well.

<a name="config-css"></a>
#### config.css

	css : {
		distDir : 'css',     // <%=config.css.distDir%>
		srcFile : 'kickoff', // <%=config.css.srcFile%>
		scssDir : 'scss'     // <%=config.css.scssDir%>
	}

The `config.css` variables all relate to the directories and paths of the project CSS.

**`config.css.distDir`** is the directory to which the CSS files will be compiled when a Grunt build is run.  By default, this is set to the `css` folder.

**`config.css.srcFile`** is the name given to the compiled CSS file when it is built from the projects SCSS files.  By default, the filename is `kickoff`.

**`config.css.scssDir`** is the directory at which the projects SCSS files are stored.  By default, this is the `scss` folder, but if you want to move them, be sure to update this config variable.

<a name="config-js"></a>
#### config.js

	js : {
		distDir  : 'js/dist/',   // <%=config.js.distDir%>
		distFile : 'app.min.js', // <%=config.js.distFile%>

		// <%=config.js.fileList%>
		fileList : [
			// if you would like to remove jQuery from your concatenated JS, comment out the line below
			'bower_modules/jquery/dist/jquery.js',

			// if you would like some basic JS shims (when not using jQuery),
			// uncomment the line below to compile Shimly output
			//'js/helpers/shims.js',

			'js/helpers/console.js',
			'bower_modules/trak/dist/trak.js',
			'bower_modules/swiftclick/js/libs/swiftclick.js',
			'bower_modules/cookies-js/src/cookies.js',

			'js/script.js'
		]
	}

The `config.js` variables relate to the directories and paths of the project JavaScript, as well as specifying what JavaScript files are included in the project compilation.

**`config.js.distDir`** is the directory to which the JavaScript files will be compiled when a Grunt build is run.  By default, this is set to the `js/dist/` folder.

**`config.js.distFile`** is the name given to the compiled JavaScript file when it is built.  By default, the filename is `app.min.js`.

**`config.js.fileList`** is the list of files that are included in the JavaScript build.  These are concatenated together when Grunt is run in the order specified in this list.  To find our more about what is included in the default JavaScript for Kickoff, see [Kickoff’s JavaScript documentation](js.html).

<a name="config-localserver"></a>
#### config.localserver

TO BE WRITTEN

<a name="config-testing"></a>
#### config.testing

TO BE WRITTEN

<hr class="sectionSplitter">
<a name="task-appendices"></a>
## Task Index

This is an exhaustive list of all the grunt tasks that Kickoff uses and what they do.

They are ordered similarly to how Kickoff’s tasks are grouped in the `_grunt-configs` directory.

### CSS Tasks

<a name="task-sass"></a>
#### Sass

Uses [grunt-contrib-sass](https://github.com/gruntjs/grunt-contrib-sass) to compile Kickoff’s Sass files into native CSS.

We compile Kickoff’s Sass into 2 CSS files; the first is a straight compile of the Sass into native CSS, while the second takes a width parameter and compiles a CSS file without media queries.  This second file is so that we can write our Sass mobile-first, but serve old versions of Internet Explorer CSS a more suitable width layout.  For more information on this approach, see [Jake Archibald’s excellent article on the subject](http://jakearchibald.github.io/sass-ie/).

The Sass task also has a configuration to compile CSS for the project styleguide, when running `grunt styleguide`.

<a name="task-autoprefixer"></a>
#### Autoprefixer

Kickoff uses [grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer) to add browser prefixes to the CSS, so that the base Sass files are kept as clean as possible.  This means that you can exclude writing browser specific prefixes, and the plugin will add it in when your CSS is compiled.

This task is run after the Sass task has converted Kickoff’s Sass into native CSS.

For more information on Autoprefixer and how it works, see it’s [Github repo and documentation](https://github.com/ai/autoprefixer).

<a name="task-csso"></a>
#### CSSO

To minify our CSS, we use CSSO via the [grunt-csso](https://github.com/t32k/grunt-csso) plugin.


### Icon tasks

The icon tasks included in Kickoff all have to be initiated separately from the default build tasks.  They are there to help with creating icons that work across devices that can be hard to manage otherwise.

<a name="task-grunticon"></a>
#### Grunticon

[Grunticon](https://github.com/filamentgroup/grunticon) is a Grunt.js task that makes it easy to manage icons and background images for all devices.

If you want to use Grunticon, take a look at [their documenation and examples](https://github.com/filamentgroup/grunticon).

Kickoff includes a basic config that makes it easy to get started with Grunticon.  Simply add SVG and PNG files to the `img/src` and run `grunt icons` from the project root directory.  This will run the icons task and give you the icons and code to include those icons in the front–end of your project.

<a name="task-svgmin"></a>
#### SVGMin

This is used as a precursor to Grunticon to ensure SVG files are optimised.  For more information on `grunt-svgmin`, [check out the documentation](https://github.com/sindresorhus/grunt-svgmin).


### JavaScript Tasks

<a name="task-uglify"></a>
#### Uglify

Uses [grunt-contrib-uglify](https://github.com/gruntjs/grunt-contrib-uglify) to minify and concatenate the defined JavaScript files into one file.  It also creates a JavaScript source map for use by developer tools, making debugging minified code much more straightforward.

<a name="task-shimly"></a>
#### Shimly

Using the [grunt-shimly](https://github.com/nicbell/shimly) plugin, this allows you to specifiy any JavaScript shims you would like to include in your project.

This allows you to then use native features such as Element.classList, with shim fallbacks for browsers that don’t implement it.

Although this is built by default by Kickoff, the associated JS file needs to be [included in the file list to be compiled](#config-js).

<a name="task-jshint"></a>
#### JSHint

Uses the [grunt-contrib-jshint](https://github.com/gruntjs/grunt-contrib-jshint) plugin to validate your JavaScript files.

This task isn’t specified in the default Kickoff build tasks, but can be initiated by running `grunt checks` from the project root directory.

JSHint can take a number of options when validating your JavaScript, all of which can be managed inside a `.jshintrc` file, found in Kickoff’s root directory.

---

## Server tasks

Kickoff’s server tasks help create a local development environment for your development.

<a name="task-connect"></a>
#### Connect

Using [grunt-contrib-connect](https://github.com/gruntjs/grunt-contrib-connect), Kickoff can start a static web server for you to use when developing.

<a name="task-browsersync"></a>
#### BrowserSync
Browsersync is used in our `grunt serve` task to create a simple server to preview your static site. Not only does it live reload any style changes (without a browser plugin I might add), but it also makes your workflow faster by synchronising URLs, interactions and code changes across multiple devices.

See this video for a demo:
<div class="fluidVideo"><iframe width="640" height="480" src="//www.youtube-nocookie.com/embed/heNWfzc7ufQ" frameborder="0" allowfullscreen></iframe></div>

---

## Utility Tasks

<a name="task-clean"></a>
#### Clean

The clean task uses [grunt-contrib-clean](https://github.com/gruntjs/grunt-contrib-clean) to remove files from directories specified.  This is useful when copying files from one directory to another to avoid old files remaining when they may have been deleted from the original directory.

<a name="task-clean"></a>
#### Shell
The clean task uses [grunt-shell](https://github.com/sindresorhus/grunt-shell) to run shell commands. We use it to install bower dependencies in the `grunt start` command.

<a name="task-watch"></a>
### Watch Task

The `grunt watch` task is incredibly powerful; it watches for changes in files you are working on and acts on any changes you make to them.

For example, if you edit a Sass file, upon saving the file the watch task will run Kickoff’s Sass and autoprefixer tasks to generate your projects CSS.  It will also live reload the CSS into your web browser so that you can see the styling changes immediately.

Kickoff is setup by default to watch:

* The scss files for changes, compiling them to CSS when saved
* JavaScript for changes, minifying and concatinating them when saved
* Any SVG file that is added to the 'img/src' directory, subsequently running SVGMin & Grunticon tasks

This task uses the [grunt-contrib-watch](https://github.com/gruntjs/grunt-contrib-watch) plugin.


