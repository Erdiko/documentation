# Authorize

**erdiko/authorize package**

Installation:

```
composer require erdiko/authorize
```

Git repo: [https://github.com/Erdiko/authorize](https://github.com/Erdiko/authorize)  

## Overview

This package implements the authorization process, allowing grant or reject user for performing an action over a resource
based on your own business rules.

## Setup / Configuration

#### Requirements

Authorize uses Pimple and Symfony Security.  These are listed in the package.json file and are automatically downloaded.

In the case of Pimple, we chose this package to manage Dependency Injection, allowing us to add more flexibility and
extensibility. It also adds compatibility with the Symfony Security package.

### Configuration

In `/app/config/default/` folder add `authorize.json` like below example:

```json
{
     "validators":{
       "custom_types": [{
         "name": "example",
         "namespace": "app_validators_example",
         "classname": "ExampleValidator",
         "enabled": false
       }]
     }
   }
```

It can be copied from `/authorize/app/config/default/authorize.json`. We will discuss this file in detail in [**Extending**](extending/)
section.
