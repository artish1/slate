---
title: Anywhere Fitness API Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  # - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Anywhere Fitness API Docs.
Docs are powered by [Slate](https://github.com/lord/slate)

Please talk to Mark Artishuk for any questions, comments, bugs, or feature requests that concern the API

### Base URL

The hosted base URL for the api is: `https://anywhere-fitness-bw.herokuapp.com`
Use this URL as a base for all routes,
example for registration:
`POST https://anywhere-fitness-bw.herokuapp.com/auth/register/`

# Authentication

Anywhere Fitness API requires a register/login process that will return a `token` to be used in the Authorization header.

Example header:
`Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

Protected API routes that require authentication and the authorization header is not present, it will throw a 401 error followed with a message "Invalid Token".

<aside class="notice">
Do not use the token in the example.
</aside>

# Users

## Registration

This endpoint is used for registration.

> Example Javascript code using axios:

```javascript
const axios = require("axios");

const body = {
  username: "fitness_dood_7",
  password: "doyouevenliftbro?",
  isInstructor: true
};
axios
  .post("/auth/register", body)
  .then(res => {
    //Handle successful registration.
  })
  .catch(err => {
    //Handle unsuccessful registration.
  });
```

> Example JSON return body:

```json
{
  "id": 3, //The user ID
  "username": "fitness_dood_7", //username that was registered with.
  "role_id": 2 //The id of the role of the user. 2 is instructor, 1 is client.
}
```

### HTTP Request

`POST /auth/register`

### JSON request body

| Field        | Example Value     | Description                                                                 |
| ------------ | ----------------- | --------------------------------------------------------------------------- |
| username     | fitness_dood_7    | The username to register with                                               |
| password     | doyouevenliftbro? | The password to register with                                               |
| isInstructor | true              | A true/false representation if the registered user is an instructor or not. |

<aside class="success">
/auth/register is up and running. 
</aside>

## Logging In

> Example Javascript code using axios:

```javascript
const axios = require("axios");

const body = {
  username: "fitness_dood_7",
  password: "doyouevenliftbro?"
};
axios
  .post("/auth/login", body)
  .then(res => {
    const token = res.data.token; //Token that was returned.
  })
  .catch(err => {
    //Handle errors/unsuccessful login.
  });
```

> Example JSON return body:

```json
{
  "message": "Welcome! here's your token",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```

This endpoint logs the user in on correct credentials.

### HTTP Request

`POST /auth/login`

### JSON Body Fields

| Field    | Description                |
| -------- | -------------------------- |
| username | The username to login with |
| password | The password to login with |

<aside class="success">
/auth/login is up and running. 
</aside>

# Classes

<aside class="notice">All class endpoints require Authorization</aside>

Some class endpoints require the user to be an instructor.

The token provided has all the information on the user accessing this route, so it will know if the user is an instructor or not.

If a non-instructor tries to access an instructor-only endpoint, it will throw a 403 Forbidden error code.

## Create a Class

> Example request body:

```json
{
  "name": "Fat 2 Fit",
  "type": "Cardio",
  "startTime": "2020-01-13T16:30:00.000Z",
  "duration": "1h",
  "intensity": 8,
  "location": "San Francisco",
  "maxSize": 10
}
```

> Example return body:

```json
{
  "id": 5,
  "instructor_id": 3,
  "name": "Fat 2 Fit",
  "type": "Cardio",
  "startTime": "2020-01-13T16:30:00.000Z",
  "duration": "1h",
  "intensity": 8,
  "location": "San Francisco",
  "maxSize": 10
}
```

<aside class="notice">Authorized user must also be an instructor</aside>

### HTTP Request

`POST /classes`

### JSON Body Fields

| Field     | Example Value            | Description                                                                               |
| --------- | ------------------------ | ----------------------------------------------------------------------------------------- |
| name      | Fat 2 Fit                | The name of the class                                                                     |
| type      | Cardio                   | The type of class                                                                         |
| startTime | 2020-01-13T16:30:00.000Z | An ISO 8601 format date time that represents the start time of the class                  |
| duration  | 1h                       | How long the class is                                                                     |
| intensity | 8                        | A value from 1-10 that determines how hard the class is                                   |
| location  | San Francisco            | The location of the class (Preferably in City only format? Will discuss with group later) |
| maxSize   | 10                       | The maximum seats the class can hold (ex: only 10 people can attend this class)           |

All JSON body fields are `required`

<aside class="success">
POST /classes is up and running. 
</aside>

## Get All Classes

Returns a list of all classes

> Example return body:

```json
[
  {
    "id": 4,
    "instructor_id": 3,
    "name": "Fat 2 Fit",
    "type": "Cardio",
    "startTime": "2020-01-13T16:30:00.000Z",
    "duration": "1h",
    "intensity": 8,
    "location": "San Francisco",
    "maxSize": 10
  },
  {
    "id": 5,
    "instructor_id": 3,
    "name": "Runnin' n' Gunnin' V2",
    "type": "Cardio",
    "startTime": "2020-01-13T16:30:00.000Z",
    "duration": "1h",
    "intensity": 8,
    "location": "San Francisco",
    "maxSize": 10
  }
]
```

### HTTP Request

`GET /classes`

<aside class="success">
GET /classes is up and running. 
</aside>

## Get Class By ID

> Example return body:

```json
{
  "id": 5,
  "instructor_id": 3,
  "name": "Fat 2 Fit",
  "type": "Cardio",
  "startTime": "2020-01-13T16:30:00.000Z",
  "duration": "1h",
  "intensity": 8,
  "location": "San Francisco",
  "maxSize": 10
}
```

### HTTP Request

`GET /classes/:id`

Replace `:id` with the id (integer only)

Example: `GET /classes/5`

Will throw a 404 if no class with the specified id exists.

<aside class="success">
GET /classes/:id is up and running. 
</aside>

## Update Class By ID

Will update any records in the database with the provided fields in the request body.

> Example request body:

```json
{
  "name": "Runnin' n' Gunnin' V2"
}
```

> Example return body:

```json
{
  "updatedRecords": 1
}
```

### HTTP Request

`PUT /classes/:id`

Replace `:id` with the id (integer only)

Example: `PUT /classes/5`

Will throw a 404 if no class with the specified id exists.

### Available fields to update

| Field     |
| --------- |
| name      |
| type      |
| startTime |
| duration  |
| intensity |
| location  |
| maxSize   |

<aside class="notice">
an http 500 error will be thrown with a SQLITE error message if you try to add a field that is not in the table above
</aside>

<aside class="success">
PUT /classes/:id is up and running. 
</aside>

## Delete Class By ID

<aside class="notice">
Must be the instructor of the class in order to delete it. 
</aside>

Will remove/delete the class by the id specified

> Example return body:

```json
{ "message": "Class deleted" }
```

### HTTP Request

`DELETE /classes/:id`

Replace `:id` with the id (integer only)

Example: `DELETE /classes/5`

Will throw a 404 if no class with the specified id exists.

<aside class="success">
DELETE /classes/:id is up and running. 
</aside>

## Get Class Attendees

Retrieves all the attendees of the specified class by id.

> Example return body

```json
[
  {
    "username": "devtesti",
    "id": 7
  },
  {
    "username": "attendee2",
    "id": 21
  }
]
```

### HTTP Request

`GET /classes/:id/attendees`

Example: `GET /classes/5/attendees`

<aside class="success">
GET /classes/:id/attendees is up and running. 
</aside>

## Add Class Attendee

Adds the authorized user to the list of class attendees.
No need for a body as the token provided has all the information to add the user.

> Example return body

```json
{
  "message": "User added to class"
}
```

<aside class="notice">
Will throw a 400 error code along with a message if the class is full.
</aside>

### HTTP Request

`POST /classes/:id/attendees`

Example: `POST /classes/5/attendees`

<aside class="success">
POST /classes/:id/attendees is up and running. 
</aside>

## Remove Class Attendee

Removes the authorized user from the list of class attendees.

> Example return body

```json
{
  "message": "User removed from class"
}
```

### HTTP Request

`DELETE /classes/:id/attendees`

Example: `DELETE /classes/5/attendees`

<aside class="success">
DELETE /classes/:id/attendees is up and running. 
</aside>
