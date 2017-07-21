# Erdiko Framework Overview

Installation:

```
composer create erdiko/erdiko
```

Git repo: [https://github.com/Erdiko/erdiko](https://github.com/Erdiko/erdiko)

## Config

The config folder is stored in `/app/config/` directory and the default application config file is located at `/app/config/application/default.json`.
In the config file, you can modify some settings of the site and plugins, such as logging, cache, and analytics.  

If you wish to store configurations for other applications, we recommend you to create a new config file under `/app/config/` directory. Moreover, all config files are stored in JSON format and you can retrieve config from the config file though the getConfig function in Erdiko class.  

For example, to read the configuration of Cache which is located at `/app/config/cache.json` directory, you can use the following code:

```
$config = \Erdiko::getConfig("local/cache");
$host = $config["memcached"]["host"];				
$port = $config["memcached"]["port"];
```

## Routes

Application routes are defined in the file, `/app/config/application/routes.json`
Update your app's routes in this file.

Erdiko uses the same routing conventions defined by ToroPHP (modeled after Tornado, a python framework)

To route the root of the site to the Example controller

		"/": "\app\controllers\Example"

To route example.com/examples/token, where the token is an alpha only name used in the controller

		"examples/:alpha": "\app\controllers\Example"

For more information on routing see [Toro PHP routing](https://github.com/anandkunal/ToroPHP#routing-basics)

### Tokens

you can use convenient tokens in your routes.  These token are simply convenient regular expressions and defined as follows.

```
':string' // '([a-zA-Z]+)'
':number' // '([0-9]+)',
':alpha'  // '([a-zA-Z0-9-_]+)',
':action' // '([a-zA-Z0-9-_/]+)'
```

### Examples

```
// This will match /page/one
"page/:string": "\app\controllers\Page"

// This will match /page/123
"page/:number": "\app\controllers\Page"

// This will match /page/123 and /page/one
"page/:alpha": "\app\controllers\Page"

// This will match /book/1/page/123 and pass the everything including
// the '/' to the method so it can be further parsed. e.g. '1/page/123'
"book/:action": "\app\controllers\Book"
```

### RESTful routes

Your route will come in based off of the route and http request type

```
// Route (in routes.json)
"rest/:alpha": "\app\controllers\Rest"

// Controller
class Rest extends \erdiko\core\Controller
{
    function get() {}
    function post() {}
    function get_xhr() {}
    function post_xhr() {}
}
```

### Auto routes

If you do not explicitly define a route for get(), post(), etc then Erdiko will automatically route based off of a naming convention.

Lets look at this route

		"examples/:alpha": "\app\controllers\Example"

If you go to yoursite.com/examples/hello, this will resolve to Example->getHello().  Where Example is the controller and getHello() is the method

## Controllers

If you have already configurated the routes file, the next step would be creating controllers which determine the content of pages.  Controllers are typically stored in `app/controllers/` directory.  Since Erdiko uses Composer to auto-load our PHP classes, you may place controllers in other directory as long as they have the same namespace anc corresponding folder structure.

Here is an example of a basic controller class:

```
class Example extends \erdiko\core\Controller
{
		/** Before */
		public function _before()
		{
				$this->setThemeName('bootstrap');
				$this->prepareTheme();
		}

		/** Get Hello */
		public function getHello()
		{
				$this->setTitle('Hello World');
				$this->setContent("Hello World");
		}
}
```

In a controller class, every function whose name starts with 'get' represents the logic of a page. For example, if you are running the site on your local machine, the url of the site on the example above would be `http://localhost/hello`.

## Views

The views are stored in `app/views/` directory.  Views is similar to Layout, however, they are not actually the same. Layout can set inside a layout or a view which view can only contain Layout. Moreover, you can put any HTML or PHP code inside a view.

Here is an example of a view:

		<p>This is a view template.</p>
		<p><?php echo $data[0] ?> world</p>

It supports HTML tags and ables to use PHP to retrieve variables.

## Models

Erdiko is a mash-up framework and our goal is to make Erdiko be able to mash-up multiple applications/frameworks like Drupal, Magento, WordPress, Zend, and etc.  There are lots of different models out there and it is not feasible to cover all of that.  Therefore, you may design your model layer depending on your needs.

For example, if you site is using database MySQL, Oracle, Microsoft SQL Server, PostgreSQL, SAP Sybase SQL Anywhere, SQLite, or Drizzle, you may consider to adopt Doctrine's Database Abstraction Layer framework to Erdiko.
Here is a link to a tutorial of basic usage.

## Hooks

In Erdiko, a hook is mainly driven by the ToroPHP router. Hook is very useful in Erdiko framework and it allows you to execute code before and after a controller is called.  It can also increase the security when communicating with third party applications.  For example, when you made a request to a third party application which is going to do a call-back action to your site, you can use hooks to hooks to verfiy the session.

For more hooks information, please see https://github.com/anandkunal/ToroPHP#torohook-callbacks

## About Erdiko

Erdiko wants to make your php development easier. If you need a lightweight MVC framework you have come to the right place. Our goal is to offer a clean framework to create sites optimized for mobile devices, APIs and multiple browsers.  Get work done without a lot of unneccessary plumbing to get in the way.  It is camptible with composer, which makes it easy to use with other PHP projects like Doctrine

Erdiko can act as a middleware framework, hence the name which means 'middle' in the Basque language (Euskara). Use Erdiko if you need to mash-up multiple applications/frameworks like Drupal, Magento, WordPress, and Zend into a unified application.

## Team

**Author**

* John Arroyo - Architect, Lead Developer

**Contributors**

* Andy Armstrong - Development
* Leo Daidone - Development

To see all the see all the contributors go to [erdiko](https://github.com/Erdiko/erdiko/graphs/contributors) and [core](https://github.com/Erdiko/core/graphs/contributors)

If you want to help, please do, we'd love more code! Make your enhancements and do a pull request. If you want to get to even more involved please contact us!

## Special Thanks

Arroyo Labs - For sponsoring development, [http://arroyolabs.com](http://arroyolabs.com)
