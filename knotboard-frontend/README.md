# KnotBoard Frontend

A dependency-free single-page frontend for the KnotBoard Spring Boot backend.

## Run

1. Start the backend on `http://localhost:8080`.
2. From this folder, run the included static server on port 3000:

   ```powershell
   node serve.mjs
   ```

3. Open `http://localhost:3000`.

The backend CORS configuration currently allows `http://localhost:3000`, so this frontend uses that port by default.

## Features

- Login and registration with JWT persistence.
- Dashboard counts from `/api/dashboard`.
- Create and browse boards.
- Create, edit, and delete sticky notes.
- Edit and delete boards for `ADMIN` and `FACILITATOR` users.
- Admin user role management from `/api/users`.

To point the app at a different backend URL, run this in the browser console and refresh:

```js
localStorage.setItem("knotboard_api_base", "http://localhost:8080/api");
```
