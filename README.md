# Spotify Song Suggester API

## API BASE URL

[`https://bwft-spotify-song-suggester.herokuapp.com/`](https://bwft-spotify-song-suggester.herokuapp.com/)

### SERVER STATUS

**GET**: `/`

> When active, will respond with the following

```javascript
{
    "spotify_song_suggester": "API IS UP"
}
```

## Table of Contents

- [Register](#register-a-user) (POST)
- [Login](#login) (POST)
- [User Data](#get-all-users) (GET)
- [User Data by ID](#get-user-by-id) (GET)
- [Update User by ID](#update-user-information) (PUT)
- [Delete User](#delete-a-user) (DELETE)

# User Routes

### REGISTER A USER

**POST**: `/api/users/register`

#### Body

| Name       | Type   | Required | Description               |
| ---------- | ------ | -------- | ------------------------- |
| First Name | String | Yes      | User first name           |
| Last Name  | String | Yes      | User last name            |
| Username   | String | Yes      | Username (must be unique) |
| Password   | String | Yes      | Password                  |

#### Example

```javascript
{
    "first_name": "Test",
    "last_name": "Test",
    "username": "test",
    "password": "test"
}
```

#### Responses:

> Will receive a **201 (Created)** response along wtih the newly created user if registration is successful

```javascript
[
  {
    id: 1,
    first_name: "Test",
    last_name: "Test",
    username: "test",
  },
];
```

> Will receive a **400 (Bad Request)** response one of the following messages if any required information is missing from the body

```javascript
{
    "message": "Missing required field: first_name"
}
```

```javascript
{
    "message": "Missing required field: last_name"
}
```

```javascript
{
    "message": "Missing required field: username"
}
```

```javascript
{
    "message": "Missing required field: password"
}
```

> Will receive a **500 (Internal Server Error)** response if there is an issue with the API server

```javascript
{
  "errorMessage": "Server error information"
}
```

---

### LOGIN

**POST**: `/api/users/login`

#### Body

| Name     | Type   | Required | Description   |
| -------- | ------ | -------- | ------------- |
| Username | String | Yes      | Username      |
| Password | String | Yes      | User password |

#### Example

```javascript
{
  "username": "test",
  "password": "test"
}
```

#### Responses:

> Will receive a **200 (OK)** response with a welcome message and a valid token if the login request is successful

```javascript
{
  "message": "Welcome to the Spotify Song Suggester API!",
  "token": "Your token will be here"
}
```

> Will receive a **400 (Bad Request)** response if any required information is missing from the body

```javascript
{
    "message": "Please enter both a username and password"
}
```

> Will receive a **401 (Unauthorized)** response if credentials are invalid

```javascript
{
  "message": "Access Denied: Unauthorized"
}
```

> Will receive a **500 (Internal Server Error)** response if there is an issue with the API server

```javascript
{
  "errorMessage": "Server error information"
}
```

---

### GET ALL USERS

**GET**: `/api/users`

#### Responses:

> Will receive a **200 (OK)** response with an array of users if the request is successful

```javascript
[
  {
    id: 1,
    username: "test",
    first_name: "Test",
    last_name: "Test",
  },
  {
    id: 2,
    username: "test2",
    first_name: "Test2",
    last_name: "Test2",
  },
];
```

> Will receive a **400 (Bad Request)** response if connecting client does not have an Authorization token in its headers

```javascript
{
    "message": "Please log in"
}
```

> Will receive a **401 (Unauthorized)** response if credentials are invalid or expired

```javascript
{
    "message": "Token invalid. Please log in and get a new token"
}
```

> Will receive a **500 (Internal Server Error)** response if there is an issue with the API server

```javascript
{
  "errorMessage": "Server error information"
}
```

---

### GET USER BY ID

**GET**: `/api/users/:id`

#### Responses:

> Will receive a **200 (OK)** response with an object containing the requested user

```javascript
{
    "id": 1,
    "first_name": "Test",
    "last_name": "Test",
    "username": "test"
}
```

> Will receive a **400 (Bad Request)** response if connecting client does not have an Authorization token in its headers

```javascript
{
    "message": "Please log in"
}
```

> Will receive a **401 (Unauthorized)** response if credentials are invalid or expired

```javascript
{
  "message": "Token invalid. Please log in and get a new token"
}
```

> Will receive a **404 (Not Found)** response if parameter ID is invalid

```javascript
{
  "message": "User ${id} could not be found"
}
```

> Will receive a **500 (Internal Server Error)** response if there is an issue with the API server

```javascript
{
  "errorMessage": "Server error information"
}
```

---

### UPDATE USER INFORMATION

**PUT**: `/api/users/:id`

#### Body

| Name       | Type   | Required | Description               |
| ---------- | ------ | -------- | ------------------------- |
| First Name | String | Yes      | User first name           |
| Last Name  | String | Yes      | User last name            |
| Username   | String | Yes      | Username (must be unique) |
| Password   | String | Yes      | User password             |

#### Example

```javascript
{
    "first_name": "Test",
    "last_name": "Test",
    "username": "test",
    "password": "test"
}
```

#### Responses:

> Will receive a **200 (OK)** response with the updated user object if the request is successful

```javascript
{
    "id": 1,
    "first_name": "Test",
    "last_name": "Test",
    "username": "test",
}
```

> Will receive a **400 (Bad Request)** response and one of the following messages if connecting client does not have an Authorization token in its headers or if any required information is missing from the body

```javascript
{
    "message": "Please log in"
}
```

```javascript
{
    "message": "Missing required field: first_name"
}
```

```javascript
{
    "message": "Missing required field: last_name"
}
```

```javascript
{
    "message": "Missing required field: username"
}
```

```javascript
{
    "message": "Missing required field: password"
}
```

> Will receive a **401 (Unauthorized)** response if credentials are invalid or expired

```javascript
{
  "message": "Token invalid. Please log in and get a new token"
}
```

> Will receive a **404 (Not Found)** response if parameter ID is invalid

```javascript
{
  "message": "User ${id} could not be found"
}
```

> Will receive a **500 (Internal Server Error)** response if there is an issue with the API server

```javascript
{
  "error": "Server error information"
}
```

---

### DELETE A USER

**DELETE**: `/api/users/:id`

#### Responses:

> Will receive a **200 (OK)** response if the user is deleted successfully

```javascript
{
    "message": "The user was successfully deleted"
}

```

> Will receive a **400 (Bad Request)** response if connecting client does not have an Authorization token in its headers

```javascript
{
    "message": "Please log in"
}
```

> Will receive a **401 (Unauthorized)** response if credentials are invalid or expired

```javascript
{
  "message": "Token invalid. Please log in and get a new token"
}
```

> Will receive a **404 (Not Found)** response if parameter ID is invalid

```javascript
{
  "message": "User ${id} could not be found"
}
```

> Will receive a **500 (Internal Server Error)** response if there is an issue with the API server

```javascript
{
  "error": "Server error information"
}
```

---
