TwigstringBundle information & howto
====================================

This Symfony2 Bundle adds the possibility to render strings instead of files with the Symfony2 native Twig templating engine.
The Bundle adds an additional service named `twigstring`. It is used the same way as the original templating service.
The only difference is that the first argument of the method `render(<string>, [<array])` is a string to parse instead of a template file.

One example usage scenario is to load templates from the database instead of using files.

Install on your project:
------------------------

    git submodule add git://github.com/LaKrue/TwigstringBundle.git src/LK/TwigstringBundle

Set configuration on config.yml (as top level entry):
-----------------------------------------------------

    lk_twigstring: ~

Update autoload.php
-------------------

``` php
$loader->registerNamespaces(array(
     //...//
     'LK'          => __DIR__.'/../src',
     //...//
));
````

Update AppKernel.php
--------------------

``` php
$bundles = array(
    //...//
    new LK\TwigtringBundle\LKTwigstringBundle(),
    //...//
);
```

Use LK/TwigstringBundle:
------------------------

``` php
// set example parameter
$vars = array('var'=>'x');

// get twigstring service
$tpl_engine = $this->get('twigstring');

// render example string
$vars['test'] = 'u ' . $tpl_engine->render('v {{ var }} {% if var is defined %} y {% endif %} z{% for i in 1..5 %} {{ i }}{% endfor %}', $vars);
```

or use the short way:

``` php
// set example parameter
$vars = array('var'=>'x');

// render example string
$vars['test'] = 'u ' . $this->get('twigstring')->render('v {{ var }} {% if var is defined %} y {% endif %} z{% for i in 1..5 %} {{ i }}{% endfor %}', $vars);
```

Example output:
---------------

    u v x y z


Authors:
--------
LarsK, cordoval