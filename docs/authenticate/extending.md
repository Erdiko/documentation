# Extending Authenticate

### Storage

We provide a Session Storage type as default method to manage your user's status and other data. However you can choose
a different storage like database, filesystem or memcached just mention few.

In order to create your own storage service, you will have to create a class that implements `erdiko\authenticate\StorageInterface`
like:
```php
Class SessionStorage implements StorageInterface {

	public function persist(UserStorageInterface $user)
	{
		$this->startSession();
		$_SESSION["current_user"] = $user->marshall();
	}

	public function attemptLoad(UserStorageInterface $userModel)
	{
		$user = null;

		$sapi = php_sapi_name();
		if(!$this->contains('cli', $sapi)){
			$this->startSession();
		}

		if(array_key_exists("current_user", $_SESSION)){
			$_user = $_SESSION["current_user"];
			if(!empty($_user)){
				$user = $userModel::unmarshall($_user);
			}
		}
		return $user;
	}

	public function contains($needle, $haystack)
	{
		return strpos($haystack, $needle) !== false;
	}

	public function destroy()
	{
		$this->startSession();
		if(array_key_exists("current_user", $_SESSION)){
			unset($_SESSION["current_user"]);
		}
		@session_destroy();
	}

	private function startSession()
	{
		if(!file_exists(ERDIKO_VAR . "/session")) {
			mkdir(ERDIKO_VAR . "/session");
		}
		ini_set('session.save_path',ERDIKO_VAR . "/session");
		if(session_id() == '') {
			@session_start();
		} else {
			if (session_status() === PHP_SESSION_NONE) {
				@session_start();
			}
		}
	}
}
```

and edit your `authenticate.json` config by adding new item in the __**storage**__ section and put it as __selected__

```json
{
  "storage": {
    "selected": "custom",
    "storage_types": [{
      "name": "session",
      "namespace": "erdiko_authenticate_services",
      "classname": "SessionStorage",
      "enabled": true
    },
    {
      "name": "custom",
      "namespace": "app_lib_authenticate_services",
      "classname": "CustomStorage",
      "enabled": true
    }]
  }
}
```

Authentication types
--------------------

As we mention before, here we need to split in two, __authentication__ and __authenticator__.
Let's start with __authentication___, here we will create class that implements __**AuthenticationInterface**__ where 
we will put the custom user's validation logic, no matter if it's just a `return true`, and **LDAP** call or any other
crazy algorithm.
  
Same as we did with __storage__, we need to add this new class in the `authenticate.json` within the `available_types`
section.

```json
{
  "authentication": {
    "available_types": [{
      "name": "jwt_auth",
      "namespace": "erdiko_authenticate_services",
      "classname": "JWTAuthentication",
      "enabled": true
    },
    {
      "name": "custom_auth",
      "namespace": "app_lib_authenticate_services",
      "classname": "CustomAuthentication",
      "enabled": true
    }]
  }
}
```

The last step is create an __authenticator__ class that implements __**AuthenticatorInterface**__.
This class is the one you will use in your app to preform the actual login process.

Within this class you will use previous defined tools to authenticate and store data, based on configuration file.
Here's an example of login method:

```php
public function login($credentials = array(), $type = 'jwt_auth')
{
    $storage = $this->container["STORAGES"][$this->selectedStorage];
    $result = false;

    // checks if it's already logged in
    $user = $storage->attemptLoad($this->erdikoUser);
    if($user instanceof UserStorageInterface) {
        $this->logout();
    }

    $auth = $this->container["AUTHENTICATIONS"][$type];
    $result = $auth->login($credentials);
    if(isset($result->user))
        $user = $result->user;
    else
        throw new \Exception("User failed to load");

    if(!empty($user) && (false !== $user)) {
        $this->persistUser( $user );
        $response = true;
    }

    return $result;
}
```

Of course is your choice what method implement, for example, you can opt to skip `persistUser` if you want to use client
side cookie instead of session or any other method on the server side. Said that, we encourage you to implement  
`persistUser` method like this:

```php
public function persistUser(UserStorageInterface $user)
{
    $this->generateTokenStorage($user);
}

public function generateTokenStorage(UserStorageInterface $user)
{
    $entityUser = $user->getEntity();

    $userToken = new UsernamePasswordToken($entityUser->getEmail(),$entityUser->getPassword(),'main',$user->getRoles());
    $_SESSION['tokenstorage'] = $userToken;
}
```

It will give you the chance to interconnect your authenticated user with other packages like `erdiko/authorize` or any
`Symfony/Security`.