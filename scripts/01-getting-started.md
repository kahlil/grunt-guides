# Grunt Guides
# 01 Getting Started

Welcome to Grunt Guides. In this guide I will show you how you can get up and running with Grunt in just a few minutes.

## Grunt

Grunt is a "JavaScript Task Runner". "Tasks" are small file operations that you might want to do as a front-end developer or designer when you build a website. For instance, once you are done programming your CSS or JavaScript you might want to concatenate all your files so that you only have one file to serve as you go live.

This is just one of many different tasks you can use Grunt for, but let's start at the beginning.

In order to install Grunt we need to install Node.js and npm first.

## Node & npm

Node.js is a platform that allows you to run JavaScript files right on your computer. You don't have to know anything about it in order to run Grunt.js but you can find out more at nodejs.org.

npm is installed with Node by default. It is a command line tool that allows you to install small programs that run on the Node platform like Grunt and the Grunt plugins.

If you want to find out more about npm you can go to npmjs.org but no further knowledge about npm is required to get started with Grunt.

### Install Node & npm

Installing Node and npm is very easy just go to  nodejs.org and click on the big Install button. This will download an installer that you then can use to install Node. npm is installed next to Node by default.

That's it, you're done.

## The Terminal

Grunt needs to be installed and run from the command line, but there are only a couple of very simple commands needed to do that. You won't have to learn how to be a command-line Ninja in order to use Grunt, all you need to know is to type a few words,  or where to look to find the right command. You can also always come back to this guide at any time and copy and paste them.

## Open the your project folder in the terminal

Once you have Node and npm installed open your terminal and change the directory to your project folder.

On the Mac you can just type

```sh
cd
```

(it's short for change directory) into the command line and then drag and drop the project folder on to the terminal window. This will add the path of the project directory next to the `cd` you just typed. Hit return and you have changed to your project folder.

On Windows you will have to open cmd.exe and then type in

```sh
cd path\to\project\directory
```

and hit return to change into your project directory.

## Create a package.json File

Open your project folder in your favorite editor and create a new file called package.json.

This file will store all the names of the programs that you will install with the `npm` command.

You can optionally also keep meta data in there like the project name and a version number and later on use that data in Grunt tasks.

But for now all you need to know is that you need to copy and paste this little snippet into your package.json file:

```js
{
  "name": "my-project-name",
  "version": "0.1.0"
}
```

You can change the name into anything you want, just make sure it is URL-friendly.

## Install grunt Locally In Your Project Folder

Next we need to install Grunt locally for this project and store it's name and it's version in the package.json.

Just type

```sh
npm grunt install --save-dev
```

into the command line and hit return. After the installation is done and you look into your project folder you will be able to notice two things:

1. a new folder appeared in the directory called node_modules this is where all the programs (which also called "packages") you install with npm are stored. This is all you need to know. You don't have to touch that folder at all.

2. the package.json file now has a new entry:

```js
devDependencies: {
	grunt: "~0.4.0"
}
```

We will make sure that all the Grunt plugins will be automatically added to the package.json later on as well. This is useful because if you want to use the same Grunt setup later on in a different project you can just copy the package.json file and type `npm install` into the command line in order to install Grunt and all the Grunt plugins at once.


## grunt-cli

In order to be able to run Grunt from the terminal we need to install a little tool called grunt-cli. "cli" stands for "comand line interface". This program only needs to be installed once. It is installed globally so it is available on your computer everywhere and it is used to actually run the Grunt installation that we just installed in your project directory locally. This just means that every project can use a different version of Grunt locally without worry.

Just type

```sh
npm install -g grunt-cli
```
into your terminal and hit return.


## Installing a Grunt plugin

Now we are going to install our first Grunt plugin. We will install the concatenation plugin maintained by the Grunt team.

This plugin will allow us to make one file out of multiple ones. Type

```sh
npm install grunt-contrib-concat --save-dev
```
into the command line.

Once the install is done go ahead and download the  sample project zip folder via the link underneath this video. Unzip it and copy the contents to your project folder. It contains a folder called "js" which contains a file called "main.js" with custom code and a "libs" folder that contains some libraries.

It is our goal to concatenate all our files together to one file. Libraries first, then the "main.js".

## The Gruntfile

In order to tell Grunt to do that we have to create a file named Gruntfile.js also just called "Gruntfile". That file will contain our task configurations. When we call Grunt on the command line later it will load that file in order to find out what to do.

First copy and paste this piece of code into your Gruntfile.

```js
module.exports = function(grunt) {
  // Project configuration.
  grunt.initConfig({

  });
};
```
This is the boilerplate code we need to make the configuration accessible to Grunt. You don't need to know what it does exactly to use and to configure Grunt.

Next we will go to the Github page of grunt-contrib-concat and figure out how to configure the plugin.

The easiest way to find out how to configure a Grunt plugin is to look for the usage example on it's GitHub README file.

Once you found it, copy the part of the example that is in between the curly braces in the 'initConfig' function and head over to your Gruntfile. Paste that configuration right into your `initConfig` like this.

```js
// Project configuration.
grunt.initConfig({
  concat: {
    src: [
      'js/libs/*.js',
      'main.js'
    ],
    dest: 'js/prod/main.js'
  }
});
```
Next we will change the configuration according to the needs of our project. We first want all our lib files and then our main.js file concatenated. Luckily you can use the star symbol as a wildcard like this.

Now we have to tell Grunt where to find the plugin with `grunt.loadNpmTasks('grunt-contrib-concat')`. The contents of your Gruntfile end up looking like this:

```js
module.exports = function(grunt) {
  // Project configuration.
  grunt.initConfig({
    concat: {
      src: [
        'js/libs/*.js',
        'main.js'
      ],
      dest: 'js/prod/main.js'
    }
  });

  grunt.loadNpmTasks('grunt-contrib-concat');
};
```
Now the task is configured and we are all set to execute it!

## Execute!

Type `grunt concat` into the terminal and watch what happens.

Grunt gives us a pretty output about what it is doing. Grunt says it executed the concat task and created a new file in js/prod called main.js.

If you open that file in editor like this you will see that all the files have been put together to one single file.

## Errors

If you get an error in the console just go ahead and read it carefully. Often it just means that the configuration in the Gruntfile was not properly formatted. In this example I missed a comma for instance.

## Next Steps

Awesome you configured your first Grunt task and executed it! I hope you can feel all that power at your fingertips now and are excited about the ways that Grunt can help you!

In the upcoming Grunt Guides I will show you how to configure more tasks for your project. Please check out gruntjs.com for more info and follow us on Twitter @gruntjs.

Thanks for watching this Grunt Guide. My name is Kahlil and I'd love to hear from you if you have any feedback for this guide. You can reach me on Twitter via my handle @distilledhype or send me an email to hello@kahlil.co.
