# API - HamburgerAPP :hamburger:

This is the back end of the hamburger app, developed to storage food data of the app, register new users and log users in. Only logged users can add items to cart.

Heroku link: https://hamburgerapprlst.herokuapp.com/

This is a fake-API built on JSON-Server (https://www.npmjs.com/package/json-server) and JSON-Server-Auth (https://www.npmjs.com/package/json-server-auth).

The original repo with the JSON-Server configuration is https://github.com/Kenzie-Academy-Brasil-Developers/json-server-base.

### Endpoints:

The API has 7 endpoints:

- /register -> new user register (POST)
- /login -> user login (POST)
- /menulist -> get menu items (GET)
- /cart?userId=:userId -> get user cart (GET) _need authentication_
- /cart -> add item to cart (POST) _need authentication_
- /cart/:itemId -> update quantity of item in cart or delete item _need authentication_

### Request body and expected answers:

<h3 align="center">Register new user</h3>

`POST /register`

```json
{
  "email": "email@mail.com",
  "password": "123456",
  "name": "Name"
}
```

In case everything works well, the answer shall be like:

`STATUS 201`

```json
{
  "user": {
    "email": "email@mail.com",
    "name": "Name",
    "id": 1
  }
}
```

_Possible errors:_

_1.- Password needs at least 4 characters (STATUS 400)_

_2.- E-mail already registered (STATUS 400)_

<h3 align="center">User login</h3>

`POST /login`

```json
{
  "email": "email@mail.com",
  "password": "123456"
}
```

In case everything works well, the answer shall be like:

`STATUS 200`

```json
{
  "user": {
    "email": "email@mail.com",
    "name": "Name",
    "id": 1
  }
}
```

<h3 align="center"> Get hamburger app menu items </h3>

`GET /menulist`

No request body needed.

In case everything works well, the answer shall be like:

`STATUS 200`

```json
[
  {
    "name": "menu item name",
    "section": "menu item section",
    "price": 20,
    "img": "image url"
  },
  {
    "name": "menu item name",
    "section": "menu item section",
    "price": 20,
    "img": "image url"
  }
]
```

<h3 align="center">Add items to cart <i>(need authentication)</i></h3>

`POST /cart`

```json
{
  "name": "menu item name",
  "price": 20,
  "quantity": 1,
  "userId": 1
}
```

In case everything works well, the answer shall be like:

`STATUS 201`

```json
{
  "name": "menu item name",
  "price": 20,
  "quantity": 1,
  "userId": 1,
  "id": 1
}
```

<h3 align="center">Get cart items <i>(need authentication)</i></h3>

The logged user can access his cart items through this endpoint.

`GET /cart?userId=:userId`

No request body needed.

In case everything works well, the answer shall be like:

`STATUS 200`

```json
[
  {
    "name": "menu item name",
    "price": 20,
    "quantity": 1,
    "userId": 1,
    "id": 1
  }
]
```

<h3 align="center">Update items' quantities in cart <i>(need authentication)</i></h3>

The logged user can change item's quantities in cart through this endpoint.

`PATCH /cart/:itemId`

```json
{
  "quantity": 10,
  "userId": 1
}
```

In case everything works well, the answer shall be like:

`STATUS 200`

```json
{
  "name": "menu item name",
  "price": 20,
  "quantity": 1,
  "userId": 1,
  "id": 1
}
```

<h3 align="center">Delete item from cart <i>(need authentication)</i></h3>

The logged user can delete items from cart through this endpoint.

`DELETE /cart/:itemId`

No request body needed.

In case everything works well, the answer shall be like:

`STATUS 200`

```json
[{}]
```
