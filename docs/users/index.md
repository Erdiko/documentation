# Users

**erdiko/users package**

The `erdiko/users` is a package adding Service Models and AJAX endpoints for user 
management in a Erdiko application.

## Intro

This package provides ORM entities & service models to manage user records, and exposes AJAX endpoints to allow your application to interact with these service models.

## Package Installation & Setup:

### Install the Package

Install the package via composer:

`composer require erdiko/users`

### Create & Install the DB

This package relies upon a number of database tables to store user records. You must create the database & tables before you can use this package.

We highly recomend installing the DB and tables with our install scripts found in the erdiko/user-admin repo (`scripts/install-db.sh`). More information can be found on the erdiko/user-admin README file.

If you would like to install the database manually, please use the `users\sql\dumps\user-admin.sql` to create the database defintion.

### Add the required routes to your Erdiko application

Below are examples of the minimum required routes to interact with the `users` package:

* Login Controller OR UserAuthenticationAjax Controller Route
    * The Login Controller exposes self-contained login/logout actions and views, these methods expose an HTML form to allow users to login
        * `"/[ROUTE NAME]/:action": "\erdiko\users\controllers\admin\UserAjax"`
    * The UserAuthenticationAjax controller provides actions to manage login/logout and password related situations as forgotPass and changePassword. This route is for AJAX login & logout.
        * `"/[ROUTE NAME]/:action": "\erdiko\users\controllers\UserAuthenticationAjax"`
* Userajax Controller Route
    * Provides actions relative to manage users without privileges, to have it accessible.
        * `"/[ROUTE NAME]]/:action": "\erdiko\users\controllers\UserAjax"`
* admin\Userajax Controller Route
    * Provides actions relative to manage users as admin level
        * `"/ROUTE NAME]/:action": "\erdiko\users\controllers\admin\Userajax"`

##### Example Route Config

Below is an example config containing all the AJAX endpoints exposed by the package:

```
 {
     "routes": {
         "/ajax/users/admin/:action": "\erdiko\users\controllers\admin\UserAjax",
         "/ajax/users/:action": "\erdiko\users\controllers\UserAjax",
         "/ajax/roles/:action": "\erdiko\users\controllers\RoleAjax",
         "/ajax/auth/:action": "\erdiko\users\controllers\UserAuthenticationAjax",
         "/users/:action": "\erdiko\users\controllers\Login"
     }
 }
```


## Current Directory Structure

Below is the current directory structure for the project, with a brief explanation below:

```
├── composer.json	
├── scripts		 
├── sql
│   ├── dumps
│   └── updates
├── src
│   ├── controllers
│   ├── entities
│   ├── models
│   ├── shared
│   ├── validators
│   └── views
└── tests
```

### scripts

The scripts directory contains helper scripts to help with package installation, as well some allowing for our CI setup.

Scripts used to upgrade the DB structure or manipulate persistent data will be stored here in future features.

### sql

This directory contains complete database dumps and update scripts, named respectively `dumps` and `updates`

The database dumps in `dumps` are used to create the initial tables. There is a version of the database structure named `user-admin.sql` that contains the base table definition and an alternate version named `user-admin-with-data.sql` with some sample data used for testing and development of the package.

The `updates` directory contains upgrade SQL scripts used to alter the DB defintion and table structures without touching the existing data in these tables. 

#### Update File Naming Structure

These files have a naming scheme so we can create a script to run these in order with a future feature. The file name is prepended with an integer indicating the order in which this script needs to be run, the larger the number the later the upgrade. 

Here is an example filename:

`[INTEGER WITH LEADING ZEROS]-[USER FRIENDLY NAME].sql`

### src

This directory contains all the source files for the package itself: Entities, Models, Controllers, Validator Classes and template partials.

### tests

This directory contains all the phpunit tests for this package.

## Unit Testing

We provide unit tests via PHPUnit and we constantly update these tests with feature updates and bug fixes. These tests are run by our CI environment on every commit and build, but you can also run these tests manually from the `tests` directory:

`phpunit AllTests`