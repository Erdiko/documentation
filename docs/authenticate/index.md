# Authenticate

**erdiko/authenticate package**

installation:

```
composer require erdiko/authenticate
```

Git repo: [https://github.com/Erdiko/authenticate](https://github.com/Erdiko/authenticate)  

## Overview

This package helps you to manage authentication process.
It includes JWT as default authenticator.

### Requirements

Authenticate uses Pimple, Symfony Security and Firebase PHP-JWT. These are listed in the package.json file and are automatically downloaded.

In case of Pimple, we chose this package to manage Dependency Injection, allowing us to add more flexibility and
extensibility. It also adds compatibility with Symfony Security module. Finally the JWT package, is being used to
provide a build in  working example of authentication extension using this protocol.

## Setup / Configuration

Before you start using this package, it needs some initial setup/config.

### Add config

Authenticate needs a config file called `authenticate.json`

```
app\config\default\authenticate.json
```

In this file will be defined two major components, the first one related with storage and the other related with
authentication.

### Configuration

For the storage we provided a SessionStorage service, but you can add your custom storage service just implementing
`erdiko\authenticate\StorageInterface` interface and adding it to the config file. For more details refer to
**[Extending](extending/)**

In case of authentication, there are two steps, __Authenticator__ and __Authentication__ that implements
`erdiko\authenticate\AuthenticatorInterface` and `erdiko\authenticate\AuthenticationInterface` respectively.
Within your app, let's say LoginController or whenever you place the __login__, you will use an instance of
__Authenticator__ that will provide you a set of useful method to login, logout, maintain cache among others.
This authenticator object will use the __authentication__ type you select, between all of the enabled options you defined
in the `authenticate.json` config, and that is the implementation of the second Interface.

There is an example of config file located in the package. You can copy from `vendor/erdiko/authenticate/app/config/default/authenticate.json`

```
{
  "authentication": {
    "available_types": [{
      "name": "jwt_auth",
      "namespace": "erdiko_authenticate_services",
      "classname": "JWTAuthentication",
      "enabled": true
    }]
  },
  "storage": {
    "selected": "session",
    "storage_types": [{
      "name": "session",
      "namespace": "erdiko_authenticate_Services",
      "classname": "SessionStorage",
      "enabled": true
    }]
  }
}
```  

As we mention above, the _authentication_ will define the available classes that
implements the user's validation logic. You can choose between a list of them defined in this config. For example, you
can have one class that allows you to authenticate using oAuth methods, other that use LDAP, other that use database,
and so on.

Same for the storage section, except that you should use only one type at time, that's why this section has a `selected`
field.

Let's breakdown the config fields.
In both cases:

* _**name**_: is the key will be used to references an individual class.
* _**namespace**_: represents a translated class namespace, e.g.: for `app\lib\service` should be `app_lib_services`,
the rule is: replace back slash with underscore.
* _**classname**_: is the exact name of the class and it is case-sensitive.
* _**enabled**_: True, if it's available to use, false, if you want to disable temporarily.
