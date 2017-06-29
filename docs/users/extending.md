# Extending the Users Package

## Intro

Extending the Users package allows you to add or modify the existing functionality of this package for use in your application. Since this is a modular package we designed this in a way that you can easily install locally with composer and clear paths to extend this code.

If you find yourself writing a bunch of custom code, we would suggest creating a custom package to store this extended code into.

Please note, this package is still limited by the constraints of PHP's object inheritance. You can only overload methods permitted by PHP [scoping](http://php.net/manual/en/language.oop5.visibility.php).

## Extending a Service Model

Extending the service models is easy and best explained with an example where we extend the User/Event/Log class where we overload the `getAllLogs` method and do some custom stuff.

For the sake of berevity, we'll pseudo code the custom stuff.

```
<?php

/**
 * MyLog extends the existing Log class and over rides the 
 * existing `getAllLogs` method
 *
 */
class MyLog extends erdiko\users\models\user\event\Log {

    /**
     *
     *
     */
    public function getAllLogs()
    {
        // custom code

        // call to the parent method we are overloading
        $results = parent::getAllLogs();

        // more custom code
        
        return $results;
    }

}
```


## Extending the Controllers

Extending controllers is just as easy as extending models, but please note that controllers do not return typical datatypes but most commonly set some values for the response object.

The AJAX controllers in this package typically extend the `\erdiko\core\AjaxController` class from the Erdiko Core package. Please refer to the relevant documentation for more information on the response object.

```
<?php

/**
 * MyUserAjax extends the existing UserAjax controller class 
 * and over rides the existing `postRegister` method
 *
 */
class MyUserAjax extends \erdiko\core\AjaxController {

    /**
     *
     *
     */
    public function postRegister()
    {
        // custom code goes here
        
        // send a pretty email to the user
        
        // set some variables for the response object
        
    }

}
```