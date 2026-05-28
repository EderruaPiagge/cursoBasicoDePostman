# Curso Básico de Postman - Fatec Araraquara
Materiais para o curso de Postman 


# Simple Books API #

API para reservar um livro.

A API está disponível no endereço `https://simple-books-api.glitch.me`

## Endpoints ##

### Status ###

GET `/status`

Retorna o status da API.

### Lista de Livros ###

GET `/books`

Retorna a lista de livros.

Query parameters opcionais:

- type: fiction ou non-fiction
- limit: número entre 1 e 20

### Consultar 1 Livro ###

GET `/books/:bookId`

Retorna informações sobre um livro em específico


### Criar Reservas ###

POST `/orders`

Reserva um livro em específico. Requer autenticação.

O request body tem que estar em formato JSON e ter as seguintes propriedades:

 - `bookId` - int - Obrigatório
 - `customerName` - String - Obrigatório

Exemplo
```
POST /orders/
Authorization: Bearer <TOKEN>

{
  "bookId": 1,
  "customerName": "Gil do Vigor"
}
```

A resposta conterá o token de acesso

### Lista de Reservas ###

GET `/orders`

Permite visualizar todas as reservas. Requer autenticação.

### Consulta 1 reserva ###

GET `/orders/:orderId`

Permite visualizar uma reserva em específico. Requer autenticação.

### Atualiza Reserva ###

PATCH `/orders/:orderId`

Atualiza uma ordem em específico. Requer autenticação.

O request body tem que estar em formato JSON e ter as seguintes propriedades:

 - `customerName` - String

 Exemplo
```
PATCH /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>

{
  "customerName": "Gil do Vigor"
}
```

### Remover Reserva ###

DELETE `/orders/:orderId`

Exclui uma reserva. Requer autenticação.

A requisição deve estar vazia.

 Example
```
DELETE /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>
```

## Criar Access Token ##

Para lidar com reservas, você precisará criar uma token de acesso.

POST `/api-clients/`

O request body tem que estar em formato JSON e ter as seguintes propriedades:

 - `clientName` - String
 - `clientEmail` - String

 Example

 ```
 {
    "clientName": "Gil do Vigor",
    "clientEmail": "gil@dovigor.com"
}
 ```

A resposta conterá o token de acesso.

## Testes de API ##

### Consultar 1 Livro ###
```
pm.test("verifica se Type é ficton ou non-fiction", function(){
    const responseJason = pm.response.json()
    pm.expect(responseJason.type).to.be.oneOf(["fiction", "non-fiction"])
});
```

### Lista de Livros ###
```
pm.test("verifica se o tempo de resposta é menor que 200ms", function(){
    pm.expect(pm.response.responseTime).to.be.below(200)
});
```

### Status ###
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
```
pm.test("Status retornou o texto OK", function () {
    const responseJason = pm.response.json();
    pm.expect(responseJason.status).to.eql("OK");
});
```
