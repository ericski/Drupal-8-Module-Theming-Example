This is a demo drupal 8 module that demonstrates the full request -> response life cycle using custom theming.

This module is a slightly modified version of a gist (https://gist.github.com/jmolivas/d29065493a91f16f35b2) by @jmolivas

We define a route in the acme.route.yml file which points to the path /acme/hello/{name}

{name} will be captured in the mapped function in a controller as the variable $name

We define the function "hello" on the controller Drupal\acme\Controller\DefaultController

The way modules are loaded into Drupal this maps to the file acme/src/Controller/DefaultController.php

The hello() function captures the $name variable from our route and returns a render array with 3 keys:

'#theme' This uses the key from our $theme array in the acme.module file
'#name' Defines the variable name in the template, in this case it's the same as our captured variable
'#attached' Allows us to include a library in the response

 We have created an incredibly basic library in the acme.libraries.yml file which pulls in a little bit of CSS.
 Libraries can contain many CSS and/or JS files (https://www.drupal.org/developing/api/assets)

 Lastly our acme.module file implements the hook_theme() hook.
 We return an array with a custom key (that we use for #theme in our render array)
 The only key we really need to provide is the 'template' key
 The template key points to a file in the templates/ folder
 By default it will fine a file named whatever you pass plus '.html.twig'
 In this case that means our template of "hello" translates to the file templates/hello.html.twig

 We also initialize the name variable just in case it's not in the render array
