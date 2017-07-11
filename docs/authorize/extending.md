# Extending Authorize

This package provides you with a framework to create custom validation. There are two different methods to create custom
validation:

- Custom Voters

    Implement `Symfony\Component\Security\Core\Authorization\Voter\VoterInterface`
    interface, and pass them in an array as second argument of `Authorizer` constructor.

- Custom Validator

    Or you can create a `Validator` class that implements `erdiko\authorize ValidatorInterface` interface.
    Then you will have to register all validators in `/app/config/default/authorize.json`, and voila, all the custom validation
    logic you've created is already available to the authorizer.  

authorize.json
```json
{
     "validators":{
       "custom_types": [{
         "name": "example",
         "namespace": "app_validators_example",
         "classname": "ExampleValidator",
         "enabled": true
       }]
     }
   }
```

In these validator classes you will be able to define custom attributes, "VIEW_ADMIN_DASHBOARD" as we mention above,
we might want to add "IS_PREMIUM_ACCOUNT", or any other attributes you want.

Note that `namespace` field of the above JSON indicate the class `namespace` and is related to the app root folder,
e.g. `/app/validators/example/ExampleValidator.php`

Let's implement the example class registered in the example JSON.  

```php
class ExampleValidator implements ValidatorInterface
{
    public static function supportedAttributes()
    {
        return array('IS_PREMIUM_ACCOUNT');
    }

    public function supportsAttribute($attribute)
    {
        return in_array($attribute, self::supportedAttributes());
    }

    public function validate($token)
    {
        $result = false;
        $user = $token->getUser();
        if (!$user instanceof UserInterface) {
            $result = false;
        } else {
            $result = ($user->getRole()=='ROLE_PREMIUM');
        }
        return $result;
    }
}
```