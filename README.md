<h1 align="center"><strong>Hamburgueria 2.0 - API</strong></h1>

Está é uma fake API criada utilizando as bibliotecas json-server e json-server-auth, para que usuários possam se cadastrar e fazer login, visualizar produtos, adicionar e remover produtos do carrinho de compras, bem como visualizar os produtos presentes no carrinho.

<br/>
<br/>

<h2 align="center"><strong>Endpoints</strong></h2>

Esta API possui um total de 6 endpoints destinados a cadastro e login de usuários, listar os produtos presentes no banco de dados, adicionar e remover produtos ao carrinho de compras, e listar os produtos adicionados ao carrinho.

<br/>
<br/>

<h2 align="center">Endpoints que não necessitam de autenticação</h2>

## _Criação de usuário_

-> POST /signup - Formato da requisição:

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "johndoe@mail.com",
  "password": "123456"
}
```

-> Status code 201 - Formato da resposta:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvaG5kb2VAbWFpbC5jb20iLCJpYXQiOjE2NDI2OTEzMDUsImV4cCI6MTY0MjY5NDkwNSwic3ViIjoiMyJ9.N9ganD_bsI8eqT4Qg8dCs11YSdzhPnAMy0k64bIvyus",
  "user": {
    "email": "johndoe@mail.com",
    "firstName": "John",
    "lastName": "Doe",
    "id": 3
  }
}
```

-> Possíveis erros

- "Email already exists" -> Email já cadastrado;
- "Email and password are required" -> Caso o campo de email ou senha não esteja presente no campo da requisição.

<br/>
<br/>

## _Login_

-> POST /login - Formato da requisição:

```json
{
  "email": "johndoe@mail.com",
  "password": "123456"
}
```

-> Status code 200 - Formato da resposta:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvaG5kb2VAbWFpbC5jb20iLCJpYXQiOjE2NDI2OTIzODQsImV4cCI6MTY0MjY5NTk4NCwic3ViIjoiMyJ9.cElHg0CvBZx_aCyw1Utuqp7AXjcQUXyLpjE6UvQ0NCw",
  "user": {
    "email": "johndoe@mail.com",
    "firstName": "John",
    "lastName": "Doe",
    "id": 3
  }
}
```

-> Possíveis erros

- "Cannot find user" -> Email não cadastrado ou digitado incorretamente;
- "Incorrect password" -> Senha digitada incorretamente.

<br/>
<br/>

## _Listagem de produtos_

-> GET /products - Formato da requisição:

-> Status code 200 - Formato da resposta:

```json
[
  {
    "id": 1,
    "name": "X-Burguer",
    "category": "Sanduíches",
    "price": 10,
    "img": "Sanduiches/cheeseburger.png"
  },
  {
    "id": 2,
    "name": "X-Bacon",
    "category": "Sanduíches",
    "price": 13,
    "img": "Sanduiches/cheesebacon.png"
  }
]
```

<br/>
<br/>

<h2 align="center">Endpoints que necessitam de autenticação</h2>

<br/>
<br/>

## _Adicionar produtos ao carrinho de compras_

-> POST /carts - Formato da requisição:

```json
{
  "userId": 2,
  "productId": 3
}
```

-> Status code 201 - Formato da resposta:

```json
{
  "userId": 2,
  "productId": 3,
  "id": 10
}
```

<br/>
<br/>

## _Remover produtos do carrinho de compras_

-> DELETE /carts/:cartId - Formato da requisição:

-> Status code 200 - Formato da resposta: Sem corpo

<br/>
<br/>

## _Listar produtos presentes no carrinho_

-> GET /users/:userId?\_embed=carts - Formato da requisição: sem corpo

-> Status code 200 - Formato da resposta:

```json
{
  "email": "johndoe@mail.com",
  "password": "$2a$10$SNreM1hQJJLXpzpnh3E6zeK2NsL1idMyTO3hKD9Z.wUrpERSoVjyW",
  "firstName": "John",
  "lastName": "Doe",
  "id": 3,
  "carts": [
    {
      "userId": 3,
      "productId": 3,
      "id": 11
    }
  ]
}
```
