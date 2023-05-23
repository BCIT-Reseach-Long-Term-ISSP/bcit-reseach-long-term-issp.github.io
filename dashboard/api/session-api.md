---
layout: default
title: Session /api/session
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/session
nav_order: 5
---

# Session /api/session
{: .no_toc }
**Base route**: `/api/session`
{: .fs-6 .fw-300 }

| 📚 Read more about Authentication and Session in the [Back-end Server Architecture Authentication & Session](/docs/dashboard/backend/authentication) documentation.|

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# /createSession

| <b>Description</b>    | Create a new session for the user. |
| <b>HTTP Verb</b>      | POST |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 500 server error |

### Request Schema
```
{
    userID: string;
}
```

### Sample Request
```
{
    userID: "1234eigh89b02749e3a41c34";
}
```

### Response Schema
```
{
    userId: string;
    sessionExpiry: string;
    sessionId: string;
}
```

### Sample Success Response
```
{
    "text": {
        "userId": "1234eigh89b02749e3a41c34",
        "sessionId": "2866326a-e164-48db-b994-74eae1181e81",
        "sessionExpiry": "2023-04-26T21:15:48.297Z",
        "_id": "644978647264e8b5dfe190a9",
        "__v": 0
    }
}
```

### Fail Response
```
{
    "message": <MESSAGE GIVEN CONDITION>
}
```

| Condition     | Message           |
| ---           | ---               |
| If userId isn’t in the body.   | "Invalid request: user ID is required in the request body."  |
| If another error occurs (ex. passing the wrong data type in the body).   | "There was an error with the request."  |

# /validateSession

| <b>Description</b>    | Validate a session and update its expiration time if it’s valid. |
| <b>HTTP Verb</b>      | POST |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |

### Request Schema

Request expects no body. Request expects a cookie named sessionCookie which is generated when `/createSession` is called. The cookie should be formatted like so:

```
{
    sessionId: string,
    expires: string,
    domain: string
}
```

### Sample Request

Request expects no body. A valid cookie (shown above) must be sent. This cookie is automatically generated when you call `/createSession`.

### Response Schema
```
{
    email: string,
    userId: string,
    role: string
}
```

### Sample Success Response
```
{
    “message”: “Session is not expired”,
    “data”: {
        “email”: “sample@email.com”,
        “userId”: “63ded2f901770f255dff8d04”,
        “role”: “Admin”
    }
}
```

### Fail Response
```
{
    "message": <MESSAGE GIVEN CONDITION>
}
```

| Condition     | Message           |
| ---           | ---               |
| If no cookie is sent.   | "Invalid request: session cookie is required."  |
| If session cookie is expired.   | "Invalid request: session cookie is expired. Please create a new session."  |
| Some other error occurs (ex. unexpected database error).   | "There was an error validating the session."  |


# /deleteSession

| <b>Description</b>    | Delete a session and set the user’s cookie to be expired. |
| <b>HTTP Verb</b>      | POST |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |

### Request Schema

Request expects no body. Request expects a cookie named sessionCookie which is generated when `/createSession` is called. The cookie should be formatted like so:
```
{
    sessionId: string,
    expires: string,
    domain: string
}
```

### Sample Request

Request expects no body. A valid cookie (shown above) must be sent. This cookie is automatically generated when you call `/createSession`.

### Response Schema

No data is given to the user, only a success or failure message (shown below).

```
{
    "message": <MESSAGE GIVEN CONDITION>
}
```

| Condition     | Message           |
| ---           | ---               |
| Success.   | "Session deleted."  |
| Failure: If no cookie is sent.   | "Invalid request: session cookie is required."  |
| Failure: If sessionId is not present in the cookie.   | "Invalid request: session ID is required."  |
| Failure: If there is some other unexpected error with the request.   | "There was an error with the request."  |
