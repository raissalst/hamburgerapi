# API para receitas e avaliações das receitas

Este é o backend de uma aplicação para cadastro de um menu de uma hamburgueria. Apenas usuários logados poderão adicionar produtos da hamburgueria ao carrinho.

## Endpoints

A API tem um total de 7 endpoints, sendo que o usuário pode adicionar itens ao seu carrinho apenas quando logado.

O url base da API é https://apihamburgueria-raissalst.herokuapp.com/

### Cadastro

POST /register

### Login

POST /login

### Rotas que não precisam de autenticação

GET /menulist

Para pegar o menu da hamburgueria

### Rotas que precisam de autenticação

PATCH /cart/1
DELETE /cart/1
GET /cart?userId=1
POST /cart

### Criação de um usuário

POST /register - FORMATO DA REQUISIÇÃO

{
"email": "email@mail.com",
"password": "123456",
"name": "ClientName",
}

Caso dê tudo certo, a resposta será assim:(STATUS 201)
</br>

"user": {
"email": "email@mail.com",
"name": "ClientName",
"id": 1
}

</br>
Possíveis erros na criação:
A senha necessita de 4 caracteres no mínimo (Erro 400) </br>
Email já cadastrado (Erro 400)
</br>

### Entrando na área do usuário (Login)

Formato da requisição:</br>

{
"email": "email@mail.com",
"password": "123456"
}

Caso dê tudo certo, a resposta será assim: (STATUS 200)</br>
"user": {
"email": "email@mail.com",
"name": "ClientName",
"id": 1
}

### GET Consultando menu da hamburgueria (rota sem autenticação)

Pode-se acessar o menu pelo endpoint:
</br>
https://apihamburgueria-raissalst.herokuapp.com/menulist

Caso dê tudo certo, a resposta será assim: (STATUS 200)</br>

[
{
"name": "Hamburguer",
"section": "Sanduíches",
"price": 14,
"img": "https://cdn.pixabay.com/photo/2016/03/05/19/02/hamburger-1238246_960_720.jpg"
},
{
"name": "X-Burguer",
"section": "Sanduíches",
"price": 16,
"img": "https://cdn.pixabay.com/photo/2020/10/05/19/55/hamburger-5630646_960_720.jpg"
},
]

### POST Adicionando itens ao carrinho (rota com autenticação)

Formato da requisição:</br>

{
"name": "X-Burguer",
"price": 16.0,
"quantity": 1,
"userId": 1
}

Caso dê tudo certo, a resposta será assim: (STATUS 201)</br>

{
"name": "X-Burguer",
"price": 16,
"quantity": 1,
"userId": 1,
"id": 1
}

### GET Consultando o carrinho do usuário (rota com autenticação)

O usuário pode consultar seu carrinho pelo endpoint:
</br>
https://apihamburgueria-raissalst.herokuapp.com/cart?userId=1

Caso dê tudo certo, a resposta será assim: (STATUS 200)</br>
[
{
"name": "X-Burguer",
"price": 16,
"quantity": 1,
"userId": 1,
"id": 1
}
]

### PATCH Alterando quantidades dos itens do carrinho (rota com autenticação)

O usuário pode alterar quantidades dos itens em seu carrinho pelo endpoint:
</br>
https://apihamburgueria-raissalst.herokuapp.com/cart/2

Formato da requisição:</br>

{
"quantity": 10,
"userId": 1
}

Caso dê tudo certo, a resposta será assim: (STATUS 200)</br>
[
{
"name": "X-Burguer",
"price": 16,
"quantity": 10,
"userId": 1,
"id": 1
}
]

### DELETE Apagando itens do carrinho (rota com autenticação)

O usuário pode remover itens do seu carrinho pelo endpoint:
</br>
https://apihamburgueria-raissalst.herokuapp.com/cart/2

Formato da requisição:</br>

{}

Caso dê tudo certo, a resposta será assim: (STATUS 200)</br>
[
{}
]
