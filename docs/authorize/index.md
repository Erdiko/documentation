# Authorize

**erdiko/authorize package**

installation:

    composer require erdiko/authorize

## Overview

This package implements the authorization process, allowing grant or reject user for performing an action over a resource
based on your own business rules.

## Setup / Configuration

### Requirements

This package requires Pimple version 3.0 or above and Symfony-security package version 3.2 or above.
To ensure all dependencies are installed when you run composer update in your project folder run the following commands:

`composer require pimple/pimple`

`composer require symfony/security`

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