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

The hosted base URL for the api is: `https://www.example.com`
Use this URL as a base for all routes,
example for registration:
`POST https://www.example.com/auth/register/`

# Authentication

Anywhere Fitness API requires a register/login process that will return a `token` to be used in the Authorization header.

Example header:
`Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

Protected API routes that require authentication will throw a 401 error followed with a message "Invalid Token".

<aside class="notice">
Do not use the token in the example.
</aside>

# Users

## Registration

This endpoint is used for registration.

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

> The above command returns JSON structured like this:

```json
{
  "id": 3, //The user ID
  "username": "fitness_dood_7", //username that was registered with.
  "role_id": 2 //The id of the role of the user. 2 is instructor, 1 is client.
}
```

This endpoint retrieves all kittens.

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

> The above command returns JSON structured like this:

```json
{
  "message": "Welcome! here's your token",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```

This endpoint logs the user in on correct credentials.

<aside class="warning">Do not use the token returned in the example JSON.</aside>

### HTTP Request

`POST /auth/login`

### JSON Body Fields

| Field    | Description                |
| -------- | -------------------------- |
| username | The username to login with |
| password | The password to login with |
