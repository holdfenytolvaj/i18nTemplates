# grunt-i18nTemplates


Parses your template files looking for locale Definitions with the syntax `[[key: text]]`, and Generates or Updates the locale files. 
Then uses those values to translate ang generate a single json file containig all your templates  (one file for each defined language), so you can access those templates easily from javascript.


## features
+ Parse your templates and automatically generate the locale files.
+ Compatible with multiple template engines. the syntax used to create a locale-Definition `[[key: text]]` is not used by many other javascript templates engines. The translation is done statically with grunt, so template engines work with filles already translated.
+ Join all your templates in a single `html.json` file, so you can access them from javascript in a more convenient way.
+ Yuo will not loose the information edited in your locale files. You can run the task whenever you want to parse new and existent templates, any new locale-Definition will be added to locale files, but will keep all your previously translated values, your translation will stay and never been overwrited.


### Generated templates
All you templates will be Joined in the file `html.json` this file contain all your templates without translation just joined in a json file for convenient access in the case you dont want to use any translation at all.

For every one of the languages defined in the options, the task will generate an extra file with all the templates translated using the values grabbed from the locale files. i.e: if `options.locales = ["en","de","oth_er"]` then the task will generate the files `en_html.json , de_html.json and oth_er_html.json` all of them already translated and ready to use in javascript.

If you have two templates `index.html and form.html`, the generated json will contain one entry for each of the templates, as shown in the code bellow, using the template's name as key.
```js
{
  "index":"<p>the template content .....",
  "form":"<for><inpup> ......"
}
```

### Using the generated code.
i.e: using Jquery and mustache
```js
//this is the english template file generated by this task and contains all you templates.
var templatesFile = "./templates/en_html.json";
jQuery.getJSON(templateFile, function(data){
      /* data contains all the templates */
      var templates = data;
      Mustache.render(templates.index,{});
});  
```

# Grunt and Task Configuration
This plugin requires Grunt `~0.4.5`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-i18nTemplates --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-i18n-templates');
```

## The "i18nTemplates" task

### Overview
In your project's Gruntfile, add a section named `i18nTemplates` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  i18nTemplates: {
  	options: {
    	locales: ["en","es","de"],
        templatesFolder: "./public/templates", //this is where the translated templates will be generated
        localesFolder: "./src/locales"  //this is where translation files will be stored	
   	},
  	your_target: {
       src: ['./src/templates/**/*.html']
    },
  },
});
```

### Options 

#### options.templatesFolder
Type: `String`
Default value: `none, this value is required and not set by default.`

A path to the templates folder.

#### options.localesFolder
Type: `String`
Default value: `none, this value is required and not set by default.`

A path to the locales folder.

#### options.locales
Type: `Array`
Default value: `none`

An Array defining all the languages. i.e: `["en","es","de"]`

### Usage Examples
This example will generate 4 locale files in the `./src/locales` folder (one for each language), and will generate 5 templates files in the `./public/templates`, (one for each language + the one without translate).
```js
grunt.initConfig({
  i18nTemplates: {
  	options: {
    	locales: ["en","es","de"],
        templatesFolder: "./public/templates", 
        localesFolder: "./src/locales" 	
   	},
  	your_target: {
       src: ['./src/templates/**/*.html']
    },
  },
});
```

## Release History
`0.1.3`  Improve Log Info and update readme.
`0.1.2`  fix bugs.
`0.1.0`  first working version. 
