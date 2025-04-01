# GraphQL
> graphql
```javascript
mkdir client, server
```
> server
```javascript
npm init
```
```javascript
npm i express body-parser cors axios
```
## setup  Apollo Server
```javascript
npm install @apollo/server graphql
```
> index.js
```javascript
const express = require('express');
const { ApolloServer } = require("@apollo/server");
const { expressMiddleware } = require("@apollo/server/express4");
const bodyParser = require("body-parser");
const cors = require("cors");

async function startServer(){
  const app = express();
  const server = new ApolloServer({
    typeDefs: `
        type Todo{
            id: ID!
            title: string!
            completed: Boolean
        }

        type Query {
            getTodos: [Todo]
        }
    `
    resolvers:{
      query: {
        getTodos: () => [
          { id: 1, title: "something is here", completed: false },
        ]
    }
});

  app.use(bodyParser.json())
  app.use(cors{});

  await server.start()

  app.use("/graphql', expressMiddleware(server));

  app.listen(8000, () => console.log("server started at PORT 8000");
}

startServer();
```
- open ```localhost:8000/graphql```
> Operation
```javascript
query GetAllTodos {
  getTodos {
    title
  }
}
```
