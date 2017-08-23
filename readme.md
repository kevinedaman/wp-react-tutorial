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

According to the Wordpress Codex (https://codex.wordpress.org/Theme_Development) the stylesheet should contain:
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
