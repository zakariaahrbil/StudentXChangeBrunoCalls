# How to use this Bruno collection

This folder is a Bruno collection for testing the StudentXChange backend API.

Official Bruno site: https://www.usebruno.com/

## 1) Open the collection in Bruno
- Install Bruno from https://www.usebruno.com/
- Open Bruno
- Click "Open Collection"
- Select this folder:
  `/home/lenovo/Documents/bruno/StudentXChange`

## 2) Set the environment
The collection contains an environment file:
- `environments/local.yml`

Update the variables there:

```yaml
vars:
  baseUrl: http://localhost:8080
  accessToken: ""
  refreshToken: ""
  userId: ""
```

Set:
- `baseUrl` to your backend URL
- `accessToken` from the login response
- `refreshToken` from the login response
- `userId` when testing admin user lookup

## 3) Run the requests in order
Recommended order:
1. `Auth/Register.yml`
2. `Auth/Login.yml`
3. `Auth/RefreshToken.yml`
4. `Users/GetMe.yml`
5. `Admin/GetAllUsers.yml` (admin)
6. `Admin/GetUserById.yml` (admin)

## 4) Request format used in Bruno
Each request file is a YAML file with this structure:

```yaml
info:
  name: Login
  type: http
  seq: 2

http:
  method: POST
  url: "{{baseUrl}}/api/auth/login"
  auth: inherit
  headers:
    Content-Type: application/json
  body:
    type: json
    data: |-
      {
        "email": "student1@example.com",
        "password": "Password123!"
      }

settings:
  encodeUrl: true
  timeout: 0
  followRedirects: true
  maxRedirects: 5
  forwardAuthorizationHeader: false
```

## 5) Notes
- The backend should be running locally on `http://localhost:8080`
- For protected routes, the request uses the `Authorization: Bearer {{accessToken}}` header
- If Bruno shows a variable not found warning, fill the missing value in `environments/local.yml`

## 6) Example flow
- Register a user
- Login using the same email/password
- Copy `accessToken` and `refreshToken` from the login response into the environment
- Call `Get Me` and admin endpoints
