# Databases

## Configuring a database

Your database credentials belong in `app/config/shared/database.json`

The default settings are good for most projects, but can be easily changed.  At a minimum, you will need to update 'host', 'database', 'username', and 'password'.

```
{
    "default": "master",
    "entities": "/entities",
    "is_dev_mode": 1,
    "connections": {
        "master": {
            "driver": "pdo_mysql",
            "host": "localhost",
            "database": "orms",
            "username": "webuser",
            "password": "webuserpass",
            "charset": "utf8",
            "collation": "utf8_unicode_ci",
            "prefix": ""
        }
    }
}
```

## Pick your ORM or db adapter

We have built in support for the (arguably) two most popular database ORMs in the PHP community.  These are Doctrine and Eloquent.

Install one of the existing adapters by using composer.  Update the database.json config file and use following composer commands to add the ORM of choice.

### Doctrine

```
composer require erdiko/doctrine
```

See more information on [Github](https://github.com/Erdiko/doctrine)

### Eloquent

```
composer require erdiko/eloquent
```

See more information on [Github](https://github.com/Erdiko/eloquent)

## Roll your own

Look at the above packages for examples of how you can easily create your own.  Reach out to us if you have some ideas or need help using other ORMs or database adapters with Erdiko.

We have used erdiko with other database packages but have not officially supported them.  We have been contemplating adding [zend-db](https://zendframework.github.io/zend-db/) and [propel](http://propelorm.org/) and [spot](http://phpdatamapper.com/).  If you wish to contribute an integration package please let us know.
