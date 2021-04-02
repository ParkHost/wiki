---
title: Feathersjs
description: 
published: true
date: 2021-03-29T10:00:21.233Z
tags: 
editor: markdown
dateCreated: 2020-06-07T19:25:20.708Z
---

![MongoDB](https://feathersjs.com/img/feathers-logo-wide.png =270x70){.align-left}
A framework for real-time applications and REST APIs.
It uses common library as:
1. expressjs
2. socketio 
3. Database connectors as (mongoose)
4. Authentication with grant and passwordjs

# Overview
![image.svg](/image.svg =700x600){.align-center}

## Services
Services is the heart of every Feathers application.

- Reading and/or writing from a database
- interacting with the file system
- Call another API
- Call other services like:
	- Sending an email
  - Processing a paymens
  - Returning the current weather for a location, etc.



> Services methods are CRUD (find(all), get(single), create, update(replace), patch(merge), remove)

# Feathers CLI
The command line interface for Feathers applications
[Github Page](https://github.com/feathersjs/cli)

---

## Installation
```js
npm install -g @feathersjs/cli
```

## Generate an app
```js
feathers generate app
```

## Generate a new service
```Javascript
feathers generate service
```
```js
? What kind of service it it? //(Database)
? What is the name of the service? // messages {service.name}
? Which path should the service be registered on? // /message (endpoint)
? Does the service require authentication? // Yes
```
```js

create src\services\{service.name}\{service.name}.service.js
// force src\services\index.js // app adds {sevice.name}.service.js
create src\services\{service.name}\{service.name}.class.js  // no idea 
create src\models\{service.name}.model.js // this is your DB model / schema
create src\services\{service.name}\{service.name}.hooks.js  // these are your (CRUD) hooks
create test\services\{service.name}.test.js
```
----

## Generate a hook

Use the feathers authentication hook to limit the user access after login:


```shell
npm install feathers-authentication-hooks
```

```js
// Example:
const { setField } = require('feathers-authentication-hooks');

const limitToUser = setField({
	// mongodb = _id
  from: 'params.user._id',
  as: 'params.query._id'
});
```

> Github: [feathers-authentication-hooks](https://github.com/feathersjs-ecosystem/feathers-authentication-hooks)
{.is-success}

---
```js
feathers generate hook
```

```js
? What is the name of the hook?
? What kind of hook should it be?
? What service(s) should this hook be for?
? What methods should this hook be for?
```

> Feathers: [Useful Hooks Library](https://hooks-common.feathersjs.com)
{.is-warning}


# Authentication
----
```js
// Modules:
@feathersjs/authentication
@feathersjs/authentication-oauth
```

For OAuth you need to extend the OAuthStrategy class to get the pofile data which i need to identify the user.
in `config/default.json` you configure the Oauth service with a `key` and `secret` of the provider (service).

```js
class ServiceStrategy extends OAuthStrategy {

  async getEntityQuery(profile) {
    return {
      service_id: profile.id
    };
  }

  async getEntityData(profile) {
  // set new object keys to the output
    const {
      userPrincipalName: service_username,
      id: service_id,
      displayName: name,
    } = profile;
    
    return {
      service_username,
      service_id,
      name
    };
  }
}
```

> Feathers uses Grant as main OAuth library: [See grant on Github](https://github.com/simov/grant) 
{.is-info}

# WebSockets
Feathers uses `SocketIO` as Realtime communication **middelware**.
More *info* see: [SocketIO](/SocketIO)


##  Channels
> `Event channels` determine which connected clients to send real-time events to and how the sent data should look like.

Some **examples** where channels are used:

- Real-time events should only be sent to authenticated users
- Users should only get updates about messages if they joined a certain chat room
- Only users in the same organization should receive real-time updates about their data changes
- Only admins should be notified when new users are created
- When a user is created, modified or removed, non-admins should only receive a "safe" version of the user object (e.g. only email, id and avatar)


> The client **doesn’t** listen to individual channels directly, but rather `subscribes` to specific events on *services* that it is interested in. Those events will only fire on the client if the server pushes data to one or more channels that the client has been added to.
{.is-info}

```js
module.exports = function(app) {
  if(typeof app.channel !== 'function') {
    // If no real-time functionality has been configured just return
    return;
  }

  app.on('connection', connection => {
    app.channel('anonymous').join(connection);
  });

  app.on('login', (authResult, { connection }) => {
    
    // app.on('login', (authResult, params, context) => {}) is sent by the 
    // AuthenticationService (see link below) on successful login.

    if(connection) {
      // Obtain the logged in user from the connection
      // const user = connection.user;
      app.channel('anonymous').leave(connection);
      app.channel('authenticated').join(connection);
    }
  });
  
  app.publish((data, hook) => {
    return app.channel('authenticated');
  });
};
```

> [AuthenticationService](https://docs.feathersjs.com/api/authentication/service.html#app-on-login)
{.is-success}

# Express REST API