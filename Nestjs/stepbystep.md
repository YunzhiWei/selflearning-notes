# Issues

* Primary column is required to have in all Entities.
* When using @nest/crud, a public member of 'service' must be defined in the controller


# Step by Step

1. Install nestjs cli

```
$ npm i -g @nestjs/cli
$ nest new nest6
```

2. Install database and TypeORM

```
$ yarn add -s @nestjs/typeorm typeorm pg
```

3. Install @nestjsx/crud

```
$ yarn add -s @nestjsx/crud @nestjsx/crud-typeorm class-transformer class-validator
```

4. Install @nestjs/swagger

```
$ yarn add -s @nestjs/swagger swagger-ui-express
```

5. Install GraphQL

```
$ yarn add -s @nestjs/graphql apollo-server-express graphql-tools graphql
$ yarn add -s type-graphql
```

# Reference

* [](https://graphql.cn)
* [](https://typegraphql.ml/)
* [](https://www.apollographql.com)