---
layout: default
title: User /api/user
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/user
nav_order: 6
---

# User /api/user
{: .no_toc }
**Base route**: `/api/user`
{: .fs-6 .fw-300 }

| 📚 Read more about Authentication and Session in the [Back-end Server Architecture Authentication & Session](/docs/dashboard/backend/authentication) documentation.|

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# /createUser

| <b>Description</b>    | Create a new user. |
| <b>HTTP Verb</b>      | POST |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 500 server error |

### Request Schema
```
{
    "email": string,
    "password": string
}
```

### Sample Schema

```
{
    "email": "yvrUser@xyz.com",
    "password": "yvrPassword!1"
}
```

### Success Response Schema
```
{
    "_id": string,
    "email": string,
    "password": string, // password is hashed
    "role": string,
}
```

### Success Sample Schema
```
{
    "_id": "1234eigh89b02749e3a41c34",
    "email": "yvrUser@xyz.com",
    "password": "$8z$80$3Qx5XB.VtrpqLQTRfu2bquJZ2AZIA39O4BrkTlUfqN3dhiJ3yT49W",
    "role": "User",
}
```

### Failure Response Schema
```
{ "message": string }
```

### Failure Response Sample
```
{ "message": <MESSAGE_GIVEN_CONDITION>}
```

| Condition     | Message           |
| ---           | ---               |
| If missing email or password.   | "Invalid request: email and password are required."  |
| If another error occurs (ex. passing the wrong data type in the body).   | "There was an error with the request."  |


# /validateUser

| <b>Description</b>    | Validate a user for login. |
| <b>HTTP Verb</b>      | POST |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 500 server error |

### Request Schema
```
{
    "email": string,
    "password": string
}
```

### Sample Schema

```
{
    "email": "yvrUser@xyz.com",
    "password": "yvrPassword!1"
}
```

### Success Response Schema
```
{
    "_id": string,
    "email": string,
    "password": string,
    "role": string,
}
```

### Success Sample Schema
```
{
    "_id": "1234eigh89b02749e3a41c34",
    "email": "yvrUser@xyz.com",
    "password": "$8z$80$3Qx5XB.VtrpqLQTRfu2bquJZ2AZIA39O4BrkTlUfqN3dhiJ3yT49W",
    "role": "User",
}
```

### Failure Response Schema
```
{ "message": string }
```

### Failure Response Sample
```
{ "message": <MESSAGE_GIVEN_CONDITION>}
```

| Condition     | Message           |
| ---           | ---               |
| If missing email or password.   | "Invalid request: email and password are required."  |
| Invalid login credentials.   | "User with this email and password combination does not exist."  |
| If another error occurs (ex. passing the wrong data type in the body).   | "There was an error with the request."  |
