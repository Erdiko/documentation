# User Admin

**erdiko/user-admin package**

Installation:

    composer create erdiko/user-admin

## Intro

The user-admin package provides a secure and attractive UI for managing users with our Erdiko framework. The UX is provided by an AngularJS Application served by our very own Erdiko framework.

The Angular Application itself is based on a Angular CLI application that imports our custom [ngx-user-admin](https://www.npmjs.com/package/@erdiko/ngx-user-admin) package from npm. This package is used to define the angular routes and provide the services and components used to create the UX.

The Erdiko application serves the JS files required for the Angular application as well as providing the routes for the AJAX requests. 

## Docker (Quick Start)

Please refer to the [README file](https://github.com/erdiko/user-admin#installation) of this repo for the most up to date information on installing this application.

## Default Login

If you followed the quick start instructions from the readme, it will create a sample admin user for you.  You can login with the following credentials:

user: erdiko@arroyolabs.com
pass: password


## How Erdiko serves the Angular Application

This Erdiko application serves up the Javascript files that bootstrap the JS application itself, and also provide the AJAX routes as noted above. In our `user-admin` erdiko theme, we use the `theme.json` file to define the Javascript files that actually serve the application. 

The build npm script (noted below) from the Angular CLI application actually compiles the typecsript into common JS files. We would highly recommend reviewing this file if you plan on editing any code.

## Setup / Configuration for ngx-user-admin for local development

Running the Angular CLI application locally is an easy way to see your changes quickly before "building" and allowing the Erdiko Application to serve the compiled files. 

To start this process, navigate to your local clone of the user-admin repository and type the following command in the terminal:

    cd /app/themes/user-admin/src/app


### NPM Local Server

This command will start the npm server locally. Files in the angular application are then "watched" and updates to the angular application will be displayed once you save the files. 

You can view the local server at this address: http://localhost:4200

    npm run start

#### Compiling you changes

Once you have tested and completed your updates, you must "build" the application to compile the typescript to be served by the erdiko application. This step is required before any code can be deployed to a staging or production server.

You can view the Erdiko application at this address: http://docker.local:8088

    npm run build


## ngx-user-admin Directory Hierarchy

The following is a brief hiearchy that highlights the components and the services.

```
├── auth.guard.ts
├── auth.service.spec.ts
├── auth.service.ts
├── header
│   ├── header.component.tpl.ts
│   └── header.component.ts
├── home
│   ├── home.component.tpl.ts
│   └── home.component.ts
├── login
│   ├── login.component.tpl.ts
│   └── login.component.ts
├── message
│   ├── message.component.tpl.ts
│   └── message.component.ts
├── message.service.ts
├── password
│   ├── password.component.tpl.ts
│   └── password.component.ts
├── user-admin.module.ts
├── user-edit
│   ├── user-edit.component.tpl.ts
│   └── user-edit.component.ts
├── user-event-log
│   ├── user-event-log.component.tpl.ts
│   └── user-event-log.component.ts
├── user-list
│   ├── user-list.component.spec.ts
│   ├── user-list.component.tpl.ts
│   └── user-list.component.ts
├── user-resolve.service.ts
├── user.model.ts
├── users-event-log
│   ├── users-event-log.component.spec.ts
│   ├── users-event-log.component.tpl.ts
│   └── users-event-log.component.ts
└── users.service.ts
```


## Components

Ngx-User-Admins are broken up in following Components.
Note: tpl.ts is used instead of HTML due to compilation process with rollup.js

### Header Component


Header Component contains the header menu used to navigate to User List and User Event Log.
At logged in state, the option to log out is available.


##### Component & Template Files

  - header.component.tpl.ts 
  - header.component.ts

### Home Component

Home Component holds the page the user-admin will see once logged in. From there, the user-admin can opt to create a user, go to User List or go to User Event Log.


##### Component & Template Files

  - home.component.tpl.ts 
  - home.component.ts

### Login

Login Components displays the Login form that is displayed when user is to log in. It also houses the user login form validation.

##### Component & Template Files

  - login.component.tpl.ts 
  - login.component.ts


### Message

Message Components hold small notification on the UI whenever there are updates. If the user-admin is successfully / unsuccessfully adding, editing, deleting 
users in the database, this component is responsible of such notification.

##### Component & Template Files

  - message.component.tpl.ts 
  - message.component.ts

### Password

Password Component is responsible for changing the user's password.

##### Component & Template Files

  - password.component.tpl.ts 
  - password.component.ts

### User-Edit

User Edit Component's function is split into to two tabs:

1. Edit the name, email address, role associated with the user
2. Change the password assoiated with the user (See Password Component).

##### Component & Template Files

  - user-edit.component.tpl.ts 
  - user-edit.component.ts


### User-Event-Log

User Event Log Component is nested within the User-Edit component and is displayed under the user-edit form. 
It retrieves recorded action the specified user has taken. The component also features sort and pagination for easy organization.

##### Component & Template Files

  - user-event-log.component.tpl.ts 
  - user-event-log.component.ts

### User-List

User-List Component retrieves all the users that are on the database. From here user-admin may target specific user to edit or delete.

##### Component & Template Files

  - user-list.component.tpl.ts 
  - user-list.component.ts

### Users-Event-Log

Users-Event-Log component generates aggregate of all actions taken by every user.
The component also features sort and pagination for easy organization.

##### Component & Template Files

  - user-event-log.component.tpl.ts 
  - user-event-log.component.ts


## Services

### Auth - auth.service.ts

This service handles logging the users in and out.

Components/Services Using this service:
 - Header Component
 - Login Component
 - Users Service

### Message - message.service.ts

This service handles the observables which relays information from source to the message component.

Components/Services Using this service:
 - Message Component
 - User Edit Component
 - User List Component

### User Resolve - user-resolve.service.ts

This service returns a User model for a provided ID, if one is found. 
If not found, it returns false and navigate the user to the default route

Components/Services Using this service:
- Users Service

### Users - users.service.ts

This service deals with create/retrieve/update/delete aspects of the Users.
It is also responsible of listing the users as well as retrieving the user events.

Components/Services Using this service:
 - User Edit Component
 - Auth Service
 - User Event Log Component
 - User List Component
 - Users Event Log Component
 - User Resolve Service
 
## Contributing

Please refer to our main project documentation about [contributing](/user-admin/contributing/). 
