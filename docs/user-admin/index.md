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

- username: erdiko@arroyolabs.com
- password: password


## How Erdiko serves the Angular Application

This Erdiko application serves up the Javascript files that bootstrap the JS application itself, and also provide the AJAX routes as noted above. 

In our `user-admin` erdiko theme, we use the `theme.json` file to define the Javascript files that actually serve the application. Please refer to our [erdiko/erdiko documentation](https://github.com/Erdiko/erdiko) for more information.

The build npm script (noted below) from the Angular CLI application actually compiles the typecsript into common JS files. We would highly recommend reviewing this file if you plan on editing any code.

## Setup / Configuration of ngx-user-admin for local development

Running the Angular CLI application locally is an easy way to see your changes quickly before "building" and allowing the Erdiko Application to serve the compiled files. 

To start this process, navigate to your local clone of the user-admin repository and type the following command in the terminal:

    cd /app/themes/user-admin/src/app


### NPM Local Server

This command will start the npm server locally. Files in the angular application are then "watched" and updates to the angular application will be displayed once you save the files. 

You can view the local server at this address: http://localhost:4200

    npm run start

### Compiling your changes

Once you have tested and completed your updates, you must "build" the application to compile the typescript to be served by the erdiko application. This step is required before any code can be deployed to a staging or production server.

You can view the Erdiko application at this address: http://docker.local:8088

