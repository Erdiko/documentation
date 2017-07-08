## Add a BMI calculator page using Javascript

1. 	Open the main config file located at `app/config/default/application.json`

2. 	Find the menu section, for example:

```
"menu": {
	"main": [{
		"href": "/examples/examples",
		"title": "Examples"
	}, {
		"href": "/examples/markup",
		"title": "Mark-Up"
	} ...
```

Insert the following json code under main:

```
	{
  		"href":"/examples/bmi",
  		"title":"BMI"
	}
```

3. 	Open the routing config file located at `/app/config/default/routes.json`.
	We can see that sites located at `/` will be routed to the controller Index and sites located at `/examples/` will be routed to the controller Example.

4.  Open the controller Example located at `/app/controllers/Examples.php`

5.  Add the following function inside the Examples class

<script src="https://gist.github.com/rajesh28892/20a1af56027064effdb9.js"></script>

6.  Create a file called `bmi.php` under `/app/views/examples/`

7.  Open the bmi.php and add the following code:

<script src="https://gist.github.com/colemantung/3cff36bbc3ac250db19f.js"></script>

8.  Create `example.js` under the folder `/app/themes/hello/js/`

9.  Paste the following code to `example.js`

<script src="https://gist.github.com/colemantung/6fb653cd88415e427a14.js"></script>

10.  Save all changes, and open a web brower.

11.  Go to localhost, click the BMI tab on the menu, and then you should see [this](./assets/themes/bootstrap-3.1.1/img/getStarted/BMI_V1_1.png).

## Add a BMI calculator page using new route

1. 	Open the main config file located at `/app/config/default/application.json`

2. 	Find the menu section and insert the following code.

		,
         {
            "href":"/Calculator/bmi_version2",
            "title":"BMI"
         }

3. 	Open the routing config file located at `Erdiko/app/config/default/routes.json`.
	Add a new rule to the route.

		["Calculator/([a-zA-Z0-9_\-/]+)", "\app\controllers\Calculator"],

4.  Then, we will need to create a new controller for the new route.
	To create a new controller, create `Calculator.php` under the folder `/app/controllers/`

5.  Paste the following code inside the `Calculator.php`

<script src="https://gist.github.com/rajesh28892/dc523f2739b48b1ff224.js"></script>

6.  Create a file called `bmi.php` under `/app/views/examples/`

7.  Open the bmi.php and add the following code:

<script src="https://gist.github.com/colemantung/c45003580e391cff6239.js"></script>

8.  Create a file called `bmi_post.php` under `/app/views/examples/`

9.  Open the bmi_post.php and add the following code:

<script src="https://gist.github.com/colemantung/ffffdf39b78d650a4734.js"></script>

10.  Save all changes, and open the site in your web brower.

11.  Click the BMI tab on the menu, and then you should see the following results.

	 [BMI Version 2](./assets/themes/bootstrap-3.1.1/img/getStarted/BMI_V2_1.png)

	 [BMI Version 2 Result](./assets/themes/bootstrap-3.1.1/img/getStarted/BMI_V2_2.png)
