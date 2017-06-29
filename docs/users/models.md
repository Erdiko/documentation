# Models

## Intro

This package uses a combination of ORM Entities and Service Models to manipulate the user records stored in the database tables. This package relies upon Doctrine as an ORM framework.

All interactions with the data model must be performed via entity models, and all interactions with the entities must be performed via service model methods.

## Entities

The entities in this package relate directly to a mapped database table, and an instance of an entity represents a single table row.

All entity properties have a protected scope, and must use the provided getter/setters to retrieve and manipulate their values. 

In addition to the getter/setters, all entities have a few lifecycle setters to set values based upon record creates and updates. These special case methods are indicated in this documentation.

### Role

This entity represents the `roles` table.

##### Properties

* *protected* *int* **$id**
    * Represents the autoincrement ID for Roles Table
* *protected* *int* **$active**
    * Integer flag representing boolean; Role is active if value is "1"/true, inactive if value is "0"/false
* *protected* *string* **$name**
    * String representing the Role name
* *protected* *string* **$created**
    * Date string for the timestamp when the record was created
* *protected* *string* **$updated**
    * Date string for timestamp when the record was last updated

##### Methods

* *public* **getId()**
    * Returns the current record $id
* *public* **setId(*int* $id)**
    * Sets the current record $id with a provided value
* *public* **getActive()**
    * Returns the current record $active value
* *public* **setActive(*string* $active)**
    * Sets the current record $active with a provided value
* *public* **getName()**
    * Returns the current record $name value
* *public* **setName(*string* $name)**
    * Sets the current record $name with a provided value
* *public* **getCreated()**
    * Returns the current record $created value
* *public* **setCreated(*string* $created)**
    * Sets the current record $created with a provided value
* *public* **getUpdated()**
    * Returns the current record $updated value
* *public* **setUpdated(*string* $updated)**
    * Sets the current record $updated with a provided value
* *public* **doStuffOnPrePersist()**
    * Lifecycle method called on initial record create via @PrePersist annotation
    * Calls existing **setCreated()** method with current timestamp as value
* *public* **doStuffOnPreMerge()**
    * Lifecycle method called on record update via @PreUpdate annotation
    * Calls existing **setUpdated()** method with current timestamp as value

### User

This entity represents the `users` table.

##### Properties

* *protected* *int* **$id**
    * Represents the autoincrement ID for Users Table
* *protected* *string* **$email**
    * Represents the email for a user
* *protected* *string* **$password**
    * Represents the user's hashed password 
* *protected* *int* **$role**
    * Foreign Key ID to the role table; represents a user's role
* *protected* *string* **$name**
    * Represents a user's name   
* *protected* *string* **$gateway_customer_id**
    * Foreign Key Id to a payment gateway table; represents a user's relationship to a payement gateway
    * _Please Note_: this will be implemented in a future feature.
* *protected* *string* **$last_login**
    * Timestamp of the user's last successful login
* *protected* *string* **$created**
    * Timestamp when the record was created
* *protected* *string* **updated**
    * Timestamp when the record was last updated

##### Methods

* *public* **getId()**
    * Returns the current record $id
* *public* **setId(*int* $id)**
    * Sets the current record $id with a provided value
* *public* **getEmail()**
    * Returns the current record $email value
* *public* **setEmail(*string* $email)**
    * Sets the current record $email with a provided value
* *public* **getPassword()**
    * Description: Returns the current record $password value
* *public* **setPassword(*password* $password)**
    * Description: MD5 encodes the provided string and sets the current record's $password value to this hashed string
* *public* **getRole()**
    * Description: Returns the current record $role value
* *public* **setRole(*string* $role)**
   * Sets the current record $role value with a provided value
* *public* **getName()**
    * Returns the current record $name value
* *public* **setName(*string* $name)**
   * Sets the current record $name with a provided value
* *public* **getGatewayCustomerId()**
    * Returns the current record gateway_customer_id value
* *public* **setGatewayCustomerId(*int* $gateway_customer_id)**
    * Sets the current record $gateway_customer_id with a provided value
* *public* **getLastLogin()**
    * Returns the current record $last_login value
* *public* **setLastLogin(*string* $last_login)**
    * Sets the current record $last_login to the provided value
* *public* **getCreatedAt()**
    * Returns the current record $created_at value
* *public* **setCreatedAt(*string* $created_at)**
    * Sets the current record $created_at to the provided value
* *public* **getUpdatedAt()**
    * Returns the current record $created_at value
* *public* **setUpdatedAt()**
    * Sets the current record $updated_at to the provided value
* *public* **doStuffOnPrePersist()**
    * Lifecycle method called on initial record create via @PrePersist annotation
    * Calls existing **setCreatedAt()** method with current timestamp as value
* *public* **doStuffOnPreMerge()**
    * Lifecycle method called on record update via @PreUpdate annotation
    * Calls existing **setUpdatedAt()** method with current timestamp as value
* *public* **marshall(*string* $type = 'json')**
    * Method that returns a current record as a 'safe' datatype
    * Used for serializing a record  

### User/Log

This entity represents the `user_event_log` table.

##### Properties

* *protected* *int* **$id**
    * Represents the autoincrement ID for User Event Log Table
* *protected* *int* **$user_id**
    * Foreign Key ID to the role table; represents a user record and associates it to this log record
* *protected* *string* **$event_log**
    * A string indicating the type of user event logged
* *protected* *string* **$event_data**
    * A JSON serialized object string representing a user logged event
* *protected* *string* **$created_at**
    * Date string for the timestamp when the record was created

##### Methods

* *public* **getId()**
    * Returns the current record $id
* *public* **setId(*int* $id)**
    * Sets the current record $id
* *public* **getUserId()**
    * Returns the current record $user_id value
* *public* **setUserId(*string* $userId)**
    * Sets the current record $user_id to the provided value
* *public* **getEventLog()**
    * Returns the current record $event_log value
* *public* **setEventLog(*string* $eventLog)**
    * Sets the current record $event_log to the provided value
* *public* **getEventData()**
    * `json_decodes` and returns the current record $event_data value
* *public* **setEventData(*string* $eventData)**
    * `json_encodes` the provided value and sets this to the current record $event_data value
* *public* **getCreatedAt()**
    * Returns the current record $created_at value
* *public* **setCreatedAt(*string* $created)**
    * Sets the current record $created_at to the provided value
* *public* **doStuffOnPrePersist()**
    * Lifecycle method called on initial record create via @PrePersist annotation
    * Calls existing **setCreatedAt()** method with current timestamp as value

## Service Models

### Mailgun

The Mailgun service model provides an interface to Mailgun to send emails following user events.

This service model extends the `Mailgun\Mailgun` model provided by the Mailgun composer package.

##### Properties

* *string* **$domain**
    * String representing the sender domain for this erdiko instance. 

##### Methods

* *public* **__construct()**
    * Creates an instance of the Mailgun service model.
    * Loads a config file and sets some local variables from this loaded config, before calling the parent constructor in `Mailgun\Mailgun`
* *protected* **getDefaults()**
    * Returns an array of default values for mailgun settings
* *public* **sendMail(*object* $postData)**
    * Sends an email with provided data. 
    * Filters the provided $postData object after typecasting to an array, returns the method call to the parent class `sendMessage` method call
* *public* **forgotPassword(*string* $email, *string* $html)**
    * Sends an email to a provided email using the provided HTML template string
    * Calls the class `sendMail` method with provided values

### Role

The Role service model provides an interface to create and manipulate role records via the Role entity.

This class uses the Erdiko Doctrine EntityTrait to allow it to get & set the entity manager.

##### Properties

* *private* *EntityManager* **$_em**

##### Methods

* *public* **__construct()**
    * Creates an instance of the Role service model.
* *public* **create(*object* $data)**
    * Create a new role entity instance
* *public* **findById(*int*|*string* $id)**
    * Return a Role entity by id
* *public* **findByName(*string* $name)**
    * Return a Role entity with a name given
* *public* **findByStatus(*int* $status)**
    * Return an array of Roles that have the provided status
* *public* **getCountByRole(*string* $role)**
    *  Return a count for role records for the provided role name
* *public* **getUsersForRole(*string* $role)**
    * Return a list of users for a provided role name
* *public* **save(*array* $data)**
    * Save/Persist a new role entity for the provided values
* *public* **getEntity(*array* $filter)**
    * Returns a Role entity record based on the provided parameters, if none found return an empty entity
* *public* **delete(*string* $id)**
    * Delete a Role entity record for the provided id

### User

The User service model provides an interface to create and manipulate user records via the User entity.

This class uses the Erdiko Doctrine EntityTrait to allow it to get & set the entity manager.

##### Properties

* *CONST* PASSWORDSALT
    * String used to salt a password before hashing
    * *Note* This will eventually be moved to a config file, currently it is just a class constant
* *protected* *Entity/User* $_user
* *protected* *EntityManager* $_em 

##### Methods

* *public* **__construct(*EntityManager* $em = null)**
    * Creates an instance of the User service model.
    * Optional EntityManager parameter to substitute the one provided by the trait
* *public* **setEntity(*Entity/User* $entity)**
    * Sets $_user to a provided *Entity/User*
* *public* **getEntity()**
    * Returns the current $_user value
* *public* **unmarshall(*string* $encoded)**
    * Unserializes a user object and returns a populated User Entity 
    * Required by the iErdikoUser Interface
* *protected* **createAnonymous()**
    * Returns a new anonymous user entity
    * Required by the iErdikoUser Interface
* *public* *static* **getAnonymous()**
    * Returns a new anonymous user entity
    * Required by the iErdikoUser Interface
* *public* **marshall(*string* $type = 'json')**
    * Serializes a populated User Entity
* *public* **getUsername()**
    * Returns current $_user name value
* *public* **getDisplayName()**
    * Returns current $_user name value
* *public* **createUser(*array* $data)**
    * Create a new entity and set it to current user model
* *public* **getSalted(*string* $password)**
    * Returns password string concat'd with password salt 
* *public* **authenticate(*string* $email, *string* $password)**
    * Attempt to validate the user by querying the DB with the provided email and password. Returns populated User Entity if found, else returns false
* *public* **isLoggedIn()**
    * Returns true if the user is logged in
* *public* **isEmailUnique()**
    * Returns true if provided email was not found in the user table 
* *public* **getRoles()**
    * Return the friendly user role names
* *public* **isAdmin()**
    * Returns true if the current $_user has an Admin role
* *public* **isAnonymous()**
    * Returns true if the current $_user has an anonymous role 
* *public* **hasRole(*string* $role = 'anonymous')**
    * Returns true if current user has the provided role
* *public* **getRole()**
    * Returns current $_user role value
* *public* **getUsers(*int* $page = 0, *int* $pagesize = 100, *string* $sort = 'id', *string* $direction = 'asc')**
    * Return all the users paginated by parameters
* *public* **deleteUser(*int*|*string* $id)**
    * Delete a user record for a provided id. Returns false if a user record is not found, and returns true if successful deletion
* *public* **getUserId()**
    * Returns current $_user id value
* *public* **save(*object* $data)**
    * Update an existing user or return a new user populated with data provided.
* *public* **getById(*int*|*string* $id)**
    * Return a user by id
* *public* **getByParams(*array* $params)**
    * Return users using params as query filter
* *public* **getGatewayCustomerId(*int*|*string* $uid)**
    * Return the Gateway Customer ID for a provided user id

### User/Event/Log

The User/Event/Log service model provides an interface to create an manipulate user event log records via the User/Log entity.

This class uses the Erdiko Doctrine EntityTrait to allow it to get & set the entity manager.

##### Properties

* *protected* *EntityManager* $_em 

##### Methods

* *public* **__construct()**
    * Creates an instance of the User/Log service model. 
* *public* **save(*Entity/User/Log* $logEntity)**
    * Persist and save the provided User/Log entity
* *public* **generateEntity(*int*|*string* $uid, *string* $event_log, *string* $event_data = null)**
    * Return a populated User/Log entity with the provided values
* *public* **getAllLogs()**
    * Return all User/Log records as an array of User/Log entities
* *public* **getLogs(*int* $page = 0, *int* $pagesize = 100, *string* $sort = 'id', $direction = 'asc')**
    * Return an array of User/Log records based on provided parameters
* *public* **getLogsByUserId(*int* $id, *int* $page = 0, *int* $pagesize = 100, *string* $sort = 'id', *string* $direction = 'asc')**
    * Return an array of User/Log records for a provided user, filtered by additional parameters
* *public* **findById(*int*|*string* $id)**
    * Return a single User/Log entity for a provided ID
* *public* **create(*int*|*string* $user_id = null, *string* $event_log = null, *string* $event_data = null)**
    * Create a new User/Log entity, wrapper for **generateEntity()** method
