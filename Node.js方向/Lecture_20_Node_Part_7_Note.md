# Lecture 20 Node Part 7
## Description
本篇笔记为 Mason 老师的 Lecture 20 Node.js (Part 7) 随堂笔记
## Table of Content
- [1. CMS](#1-cms)
    - [1.1 ERD](#11-erd)
- [2. CMS Practice](#2-cms-practice)
## 1. CMS
Content Management System, for example:
- blog
- ecommerce
- school(CMS vs LMS)
  - CMS: admin to manage relation between teachers and students
  - LMS: manage learning content
### 1.1 ERD
Entity Relationshipn Diagram: relationship between data
> Tools for mongoDB ERM:
> - hackolade
> - moon modeler
> - lucid chart
> - draw.io (free)

> Draw a chart as a reference when the data relationship is complicated
## 2. CMS Practice
> Repo: [source code](https://github.com/LazeBear/jr-fullstack-notes-21/tree/8e5ef171225e46574986d9777f89ac69a29065d2/jr-cms)

Notes:
1. common controller file naming
    ```js
    // examples
    student.controller.js
    students.controllers.js
    students.js
    // 单复数都可以，但整个代码风格要一直
    ```
2. `index.js` under `routes/` folder to organse all routes imports
3. `.env` file
    - under root folder
    - should not be uploaded to git repo
4. `common/logger.js`
    - you can create a function to make Winston log the filename `__filename`
    - You can integrate Winston with Morgan, in which case we don't need filename.
    - You can add logging for the request ID.
    - Log entries are added in places prone to errors, rather than for every single request.
    - Log storage:
        - Backend file system (not recommended)
        - Database
        - Dedicated log management platforms, such as:
            - `Elasticsearch` + `Kibana`
            - `Transport` + plugins
            - Some deployment platforms support saving `console` output.
5. `common/morgan.js`
6. `middleware/formatResponse.middleware.js` formattedResponse middleware 
7. `middleware/notFound.middleware.js` 404 page and use `logger` to record unusual requests
8. `middleware/errorMiddleware/unkownError.middle.js`  Error Handling 
    - Pass for parameters
    - use `logger` to record：message \n, error stack, and others
9. Error handling in services：
    - You can return an error through `formattedResponse`.
    - Alternatively, you can throw a custom error class that inherits from ERROR, located in `common/exceptions/notFound.exception.js`, and handle it with `try{...} catch(e){ next(e) }`.
10. There is another type of error known as an application error, which differs from global errors. It's not widely used anymore because deployment environments can automatically restart the server and log errors.
11. Mongoose
    - Model: `models/student.model.js`
12. `common/utils/db.js` Connect to database
13. `timestamps: true`
14. While MongoDB does offer some method like `uppercase:true, lowercase:true`, it is recommended to handle these in your business logic for better maintainability.