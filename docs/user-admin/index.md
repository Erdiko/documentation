# User Admin

**erdiko/user-admin package**

Installation:

    composer create erdiko/user-admin

## Intro

This is what it does...

## Docker (Quick Start)

The easiest, and recommended, way to get start is to use Docker.  The instructions assume you have Composer, Docker, & Docker Compose already installed on your machine.

To start your environment do the following.

    composer create erdiko/user-admin
    cd user-admin
    docker-compose up -d

If you are on a PC or mac, the easiest way to install Docker and Docker Compose is to install the [Docker Toolbox](https://www.docker.com/products/docker-toolbox) on your computer.  It will also install Kitematic and Machine.

## Default Login

If you followed the quick start above, it will create a sample admin user for you.  You can login with the following credentials.

user: erdiko@arroyolabs.com
pass: password

## Setup / Configuration


In the user-admin repository type the following command in the terminal:

    cd /app/themes/user-admin/src/app

Once you're in the correct directory, use the following commands to run the tests.

Local Server:

    npm run start

After the command, going to localhost:4200 will direct you to the local page.

Docker Server:

    npm run build

After the command, going to docker.local:8088 will direct you to the build page.


## Theming

Here are brief overview of how Erdiko does theming.

 - **addMeta()**: Manages metadata of the application.
 - **setPageTitle()** and **setBodyTitle()**: Manages the title.
 - **getCss()** and **getJs()**: their setters add units of code, but the getters retrieves an array of that specific nature (array of css, or array of js stored). The result is a well formed <link> tag according to each array cell.
 - **getTemplateHtml($aPartialToBeRendered)**: we can switch the template for a theme to render html with data.
 - **toHtml()**: Renders HTML.

## Contributing


