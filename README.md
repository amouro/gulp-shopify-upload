gulp-shopify-upload
===================

## Introduction

**gulp-shopify-upload** is a [Gulpjs](https://github.com/gulpjs/gulp) plugin used to watch and upload theme files to Shopify.
By using this plugin you can watch all of the different folders in a Shopify theme and have them automatically sync to your Shopify store on save. This is more lightweight than using Shopifys inline theme editor or desktop theme editor, and works on Windows, Mac and Linux.

This is a port of a similar plugin using Grunt called [grunt-shopify](https://github.com/wilr/grunt-shopify), thank you to the author for making a great plugin for Shopify.
## Features

- Uploads any file changes to Shopify on save in the folders:  `assets, layout, config, snippets, templates, locales`
- Automatically uploads changes to the current working theme in shopify unless a themeid is specified
- Lightweight and fast, changes are uploaded instantly


## Usage

1. Download whatever theme you are working on from Shopify to a local directory
2. Create a [private app](http://docs.shopify.com/api/authentication/creating-a-private-app) in Shopify and get the API Key and Password for it.
3. Your folder structure and gulpfile.js should have look something like below

	```
	shopifyTheme/
	|-- gulpfile.js
	|-- assets/
	|-- config/
	|-- layout/
	|-- locales/
	|-- snippets/
	|-- templates/
	```

	**Example Gulpfile**

	```
	// Gulp plugin setup
	var gulp = require('gulp');
	// Watches single files
	var watch = require('gulp-watch');
	var gulpShopify = require('gulp-shopify-upload');

	// Setup Shopify Theme and Private App credential
	var shopify_key = 'API KEY';
	var shopify_pass = 'PASSWORD';
	var shopify_name = 'MYSITE';
	var shopify_themeid = 'THEME ID';

	gulp.task('shopifywatch', function() {
		return watch('./+(assets|layout|config|snippets|templates|locales)/**')
	  .pipe(gulpShopify(shopify_key, shopify_pass, shopify_name + '.myshopify.com', shopify_themeid))
	});

	// Default gulp action when gulp is run
	gulp.task('default', [
	        'shopifywatch'
	]);
	```

4. The basic function call looks like 

	```
	gulpShopify('API KEY', 'PASSWORD', 'MYSITE.myshopify.com', 'THEME ID')
	```

	- `API KEY` is the API Key generated when creating a private app in Shopify
	- `PASSWORD` is the Password generated when creating a private app in Shopify
	- `MYSITE.myshopify.com` is the URL of your shop
	- `THEME ID` is the ID of your theme and is **OPTIONAL**, if not passed in, the current working theme will be used

4. Run `npm install gulp`, `npm install gulp-watch` and `npm install gulp-shopify-upload`
5. Run `gulp` and edit one of your theme files, it should automatically be uploaded to Shopify


*Created by [Able Sense Media](http://ablesense.com) - 2015*

*Modified by [Chris Wu](http://github.com/amouro)*
