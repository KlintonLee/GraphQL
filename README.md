# GraphQL

## O que é GraphQL?
GraphQL é uma linguagem de queries, como o SQL, que tem como objetivo otimizar as chamadas API RESTful dando a eles o poder de perguntar exatamente o que eles precisam e nada mais.

## Porque utilizar o GraphQL?
Em alguns casos que precisamos de dados por exemplo, de usuário e de carros. Uma das alternativas é enviar duas requisições e receber dias informações, mas e se eu só precisasse apenas do nome do usuário e a marca do carro? Aí nos deparamos com `overfetching`, ou seja, mais dados do que precisamos foram trafegados. Trabalhar com GraphQL traz algumas vantagens, e claro, algumas desvantagens.

## Types e Schemas
O GraphQL utiliza types como modelagem de dados, e a partir deles formamos schemas (modelo). É a partir destes tipos que definimos os objetos podem ser associados e quais campos eles terão. Por exemplo:
```
type User {
  uuid: ID! // exclamação não permite nulo
  username: String!
  password: String!
  is_admin: Boolean!
  department: Department
}

type Department {
  name: String!
  office: [String!]!
  locale: String!
}
```
Note no exemplo que o User possui relacionamento com Departament.

## Query e Mutation
As consultas são realizadas no servidor a partir das `Queries` feitas pelo cliente. As operações de criação, atualização e exclusão são feitas pelas `Mutations`.
- Query para obter do usuário: (uuid, username, departament.office)
```
{
  user {
    uuid
    username
    department {
      office
    }
  }
}
```
- Mutation enviando dados para criar usuário e retornando apenas o uuid
```
mutation createUser(
  name: "Klinton",
  username: "klin",
  password: "123456"
  is_admin: false
) {
  uuid
}
```

## Resolvers
