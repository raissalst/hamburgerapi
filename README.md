# API - HamburgerAPP :hamburger:

This is the back end off the hamburger app, developed to storage food data of the app, register new users and log users in. Only logged users can add items to cart.

Heroku link: https://apihamburguerapp-raissalst.herokuapp.com/

### Endpoints:

The API has 7 endpoints:

- /register -> new user register (POST)
- /login -> user login (POST)
- /menulist -> get menu items (GET)
- /cart?userId=:userId -> get user cart (GET) _need authentication_
- /cart -> add item to cart (POST) _need authentication_
- /cart/:itemId -> update quantity of item in cart or delete item _need authentication_

### Request body and expected answers:

<h3 align = "center"> Register new user </h3>

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

- User login
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

- Get hamburger app menu items
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

- Add items to cart (_need authentication_)
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

- Get cart items (_need authentication_)
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

- Update items' quantities in cart (_need authentication_)
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

- Delete item from cart (_need authentication_)
  The logged user can delete items from cart through this endpoint.
  `DELETE /cart/:itemId`
  No request body needed.

In case everything works well, the answer shall be like:
`STATUS 200`

```json
[{}]
```
