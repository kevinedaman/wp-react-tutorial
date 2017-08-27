# Wordpress and React Tutorial

## Description

Tutorial on setting up React to work within Wordpress.

## Technology Used
  * Wordpress
  * React
  * Webpack
  * Babel
  * NPM

## Getting Started

All of the sample code is in the repository.  You can follow the tutorial, or you can download the code and play with it.  This isn't a full theme, just a setup that allows you to build with React within Wordpress.

## Introduction

One of the things I like to do is mash things together that aren't necessarily made to go together.  And, since I've spent most of this summer working with Wordpress, I've done a lot of combining with technologies I either know or am working on with Wordpress.  Not because I should, but because I can

### Why React?

I'm not the genius who decided that Wordpress and React should go with each other.  That's up to those guys at Automattic - the "business" side of Wordpress.  They've already put together this thing called Calypso that, for some reason, combines Wordpress with React.  

People way smarter than me have made this decision.  And as I play around with React, the more I am inclined to agree with them.  It's a lightweight library that is pretty powerful.  What it doesn't have is the full functionality of a framework like Angular.  Working with Wordpress, that's a good thing.  What React does is give you a powerful way to do cool stuff with the DOM, while choosing whether or not you want to add any extra stuff, such as Redux.

The other thing that helped push this evolution along was the Wordpress REST API.  If you are unfamiliar with the REST API, it allows developers to pull from the Wordpress backend while having a front end of their choosing.  This opens the door to any front end technology you want.

## The Theme

We are going to create a theme that taps into some of the core functionality of Wordpress while allowing you to do whatever you want with the React front end.  This is a pretty bare setup, but it will get you started.

## Disclaimer

I've figured this stuff out mostly by hacking around and combining what I know and am learning.  Is it right?  I have no idea.  It works.  If you have a better way to do what I am doing, please contribute in the comments.  Now let's get started.

## Setting Up Wordpress

First things first, we need to get the basic Wordpress framework set up.  In order to do that, we are going to need 3 files:
  1. style.css
  2. index.php
  3. function.php

With these three you should be able to do everything.  I'm also going to add a footer.php and a header.php, just because it seems like the Wordpressy thing to do.

### style.css

The two things that every theme needs is the style.css and the index.php.

In the stylesheet, the information in the code block at the top, is what defines the theme for Wordpress.

According to the [Wordpress Codex] (https://codex.wordpress.org/Theme_Development) the stylesheet should contain:
  1. Theme Name
  2. Theme URI
  3. Author
  4. Author URI
  5. Description
  6. Version
  7. License
  8. License URI
  9. Tags
  10. Text Domain

For this theme, the header of the CSS file would look like a version of this:

```
/*
Theme Name: WP React Setup Tutorial
Theme URI: https://github.com/KevinDahlberg/wp-react-tutorial
Author: Kevin Dahlberg
Author URI: http://www.kevindahlberg.com
Description: This is the theme created for a tutorial on combining Wordpress with React.
License: GNU General Public License
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Tags: React, Wordpress REST API, Webpack, Babel
Text Domain: wp-react-setup

This theme, like WordPress, is licensed under the GPL.
Use it to make something cool, have fun, and share what you've learned with others.
*/
```

### index.php

This is the main template, and must be present in the theme.  At this point, we can put all of the HTML information needed for the app right into the index.php.  For this tutorial, I'm going to keep the index.php pretty minimal.

1. Write a php comment block at the top of the page explaining what theme this is.

```
<?php
/**
* Theme Name: Wordpress React Setup Tutorial
* Version: 1.0
*/
?>
```

2. Because we are going to have a header and a footer, add the relevant code to access those template files.

```
<?php get_header(); ?>

<?php get_footer(); ?>
```

3. Last, we need to create the div that React is going to access.  This goes after the get_header() and before get_footer().

```
<div id="container"></div>
```

#### Your index.php file ends up looking like this:

```
<?php
/**
* Theme Name: Wordpress React Setup Tutorial
* Version: 1.0
*/
?>

<?php get_header(); ?>

<div id="container"></div>

<?php get_footer(); ?>
```

### header.php

The header.php file is where we are going to put everything that goes above the body in a normal HTML file and the function wp_head php/Wordpress function.

1. Like the other files, we start with a comment block.

```
<?php
/**
 * Theme Header
 *
 * @package Wordpress React Setup Tutorial
 * @version 1.0
 */
 ?>
```
2. Next, the doctype and head up to the opening <body>.

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
```
3. The wp_head() function that brings in the head information that gets put together by Wordpress.  This goes right above the closing </head> tag.

```
<?php wp_head(); ?>
```
#### You end up with a file that looks like this:

```
<?php
/**
 * Theme Header
 *
 * @package Wordpress React Setup Tutorial
 * @version 1.0
 */
 ?>

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  <?php wp_head(); ?>
  </head>
  <body>
```

### footer.php
Like the header, the footer.php is very similar in that it contains a function that Wordpress core accesses, wp_footer().  The other information you put in the footer are closing tags for anything that opened up in the header.  Also, if we weren't going to do everything with react, you would put the footer content in the footer.php.

1. Comment Block:

```
<?php
/**
* Theme Footer
*
* @package Wordpress React Setup Tutorial
* @version 1.0
 */

?>
```

2. Closing Tags:

```
</body>
</html>
```

3. Footer function:

```
<?php wp_footer(); ?>
```

#### The end result:

```
<?php
/**
* Theme Footer
*
* @package Wordpress React Setup Tutorial
* @version 1.0
 */

?>

<?php wp_footer(); ?>

</body>
</html>
```

### Alternate Format
We don't have a lot of information in these three files.  If you wanted to put all of this into the index.php file, you could do that as well.  That file would look something like this:

```
<?php
/**
 * @package Wordpress React Setup Tutorial
 * @version 1.0
 */
?>

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>

  <?php wp_head(); ?>

  </head>
  <body>

    <div id="container"></div>

    <?php wp_footer(); ?>

  </body>
</html>
```

### functions.php
The next file we need to set up is the functions.php file.  This is the file that sets up various parts of your theme, in particular, sourcing any javascript or CSS files that you need.

1. Comment Block

```
<?php
/**
 * enqueue scripts and styles
 * @package Wordpress React Setup Tutorial
 * @version 1.0
 */
```
* note - we are going to keep the php open for the whole document.

2. Theme Scripts - This is where the js and css gets set up.  wp_enqueue_style takes care of the CSS, wp_enqueue_script takes care of the js.

```
function theme_scripts() {
  wp_enqueue_style ('stylesheet', get_stylesheet_uri() );


  //adds the compiled react file
  wp_enqueue_script ('bundle', get_template_directory_uri() . '/assets/bundle.js', array('jquery'), 1.0, true);

  //makes various wordpress settings available for use in the JS
  wp_localize_script('queries', 'WPsettings', array(
			'root' => esc_url_raw( rest_url() )
		));

}
add_action( 'wp_enqueue_scripts', 'theme_scripts');

?>
```
## Installing and Configuring Webpack

After we have Wordpress set up, the next step is to get Webpack setup.  While we could just source React in and write the website that way, Webpack opens up the possibility to use more powerful tools, and streamlines the development process as well.

I prefer to use NPM to set up Webpack.

1. In the command line, run NPM Init for this project to create the package.json file.

2. Next, run the command npm install webpack --save-dev

3. Create a file called webpack.config.js

* if you are using git, you will also want to create a .gitignore file and add node_modules to it.  This keeps the node_modules folder from ending up on git.

Once you have created the webpack.config.js, we can add the configuration information to the file.

For this project, we are going to configure Webpack to package all of our JS files up into a file called bundle.js, set up Babel so that we can use ES6, and set up the jquery plugin, for the AJAX calls.  The reason we are using jQuery and not a leaner option, is because jQuery is already included in Wordpress.

Your configuration file will end up looking like this:

```
var webpack = require('webpack');

module.exports = {
  entry: __dirname + '/src/index.js',
  output: {
    path: __dirname + '/public/assets',
    filename: 'bundle.js',
    publicPath: 'assets'
  },
  module: {
    loaders: [
      {
        test: /\.js$/,
        exclude: /(node_modules)/,
        loader: 'babel-loader',
        options: {
          presets: ['latest', 'stage-0', 'react']
        }
      }
    ]
  },
  plugins: [
    new webpack.ProvidePlugin({
    $: "jquery",
    jQuery: "jquery"
  })
  ]
};
```

We still have a few more steps before we are up and running.

1. NPM install everything that we configured in Webpack, this includes Babel, the babel presets, and react

```
npm install babel babel-loader babel-preset-latest babel-preset-stage-0 babel-preset-react --save-dev
```
You also want to run a separate install without the dev tag for react and react-dom
```
npm install react react-dom --save
```

2. Set up your scripts in package.json.
You need a build script to compile all of the Javascript (and anything else) that you have set up in webpack.

```
"build": "webpack --config webpack.config.js",
```
The other thing, which is nice to have, is a watch command.  What this will do is refresh your build every time you save.
```
"watch": "webpack --watch"
```

One thing I didn't set up, which I might on a strictly react project, is a dev server.  This is because everything we do is already up and running in our Wordpress environment.  
