# Lecture 22 Node Part 8 Authentication & Authorization
## Description
本篇笔记为 Mason 老师的 Lecture 22 Node.js (Part 9) 随堂笔记
## Table of Content
- [Introduction](#introduction)
- [CMS Practice (Part 3)](#cms-practice-part-3)
## Introduction
- **Authentication**: who are you
   - Common authentication methods include identity verification protocols (such as OAuth, OpenID Connect), token-based authentication (such as JWT), and certificate authentication.
- **Authorization**: what can you do
  - Common authorization mechanisms include Role-Based Access Control (RBAC), Attribute-Based Access Control (ABAC), Policy-Based Access Control, and others.
## CMS Practice (Part 3)
> Continued from the previous course
> Repo: [source code](https://github.com/LazeBear/jr-fullstack-notes-21/tree/8e5ef171225e46574986d9777f89ac69a29065d2/jr-cms)
### `unique: required` 
- Unique, for example `username`
### Separate auth controller and user controller
- Auth controller includes business logic for register and login
- User controller includes CRUD operations for user data
### New user account
- Generally, CMS does not allow external user registration, usually new users are created by super administrators (create user in user controller).
### Error status codes
- `409 Conflict`: User already exists when creating a user
- `401 Unauthorized`: Username or password incorrect during login
### Encrypt and Decrypt
- Method One:
  - Hash encryption is non-reversible, it can only be used to compare hash passwords stored in the database with hash passwords entered by users.
  - Salt: Makes the hash encryption method random, but it results in plaintext storage.
  - Pepper: Results in non-plaintext storage, usually unnecessary.
- Method Two:
  - Mongoose provides Schema.method for custom methods to verify passwords. And call it in the controller.
  - Cannot use arrow functions because it needs to use `this`.
### Token vs Session and Cookie
#### Token
- header + payload + verify signature
- advantages:
  - stateless server (state in token)
  - cross origin/ cross domain
- disadvantages:
  - Once JWT token is issued, it remains valid until it expires
    - That means administrators cannot forcibly log out a particular account at any given moment.
#### session and cookie
- for server side rendering
- advantages:
  - CSRF
  - state server (state in session)
  - It can record some user information and behavior.
> Sometimes both `token` and `cookie` are used.
#### how to use token
- Typically, a secret is generated and managed by DevOps using scripts.
- Set expiration time.
- Access token and refresh token.
- `utils/jwt.js`: `jwt.sign()` and `jwt.verify()`
  - Use try{} catch(e){} when using `jwt.verify()`.
  - When parsing `token` using `jwt.verify`(), you can obtain the role and user's permissions.
- When to return a token:
  - After logging in.
  - Do not return a token after registration because it involves email verification (usually handled by third-party packages).
### Block a user account
- Add a "locked" attribute to user data to manage and modify the blocked status of the account.
  ```js
  {
    "_id": ObjectId("123456789012345678901234"),
    "username": "example_user",
    "email": "user@example.com",
    "password": "hashed_password",
    "locked": false
  }

  ```
### Permissions
- RBAC: Role-Based Access Control
  - Multiple roles
    - For example:
      - Admin: Add, Delete, Post, Put
      - User: Add, Post, Put
- ABAC - Attribute-Based Access Control (Same role, custom operation permissions)
- In large-scale projects, for easier management, authentication verification might be placed in controllers or services rather than using middleware.
### SSO: Single Sign-On Solution:
1. Establish and associate a third-party login database.
2. Alternatively, utilize existing third-party libraries.

