# Authorize

**erdiko/authorize package**

installation:

    composer require erdiko/authorize

## Overview

This package implements the authorization process, allowing grant or reject user for performing an action over a resource
based on your own business rules.

## Setup / Configuration

##### Requirements

Between its requirements we count on Pimple and Symfony Security.
In case of Pimple, we choose this package to manage Dependency Injection, allowing us to add more flexibility and 
extensibility. 
It also adds compatibility with Symfony Security module.

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