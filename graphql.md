# GraphQL

## What is GraphQL

- GraphQL is an open-source query language and API standard "as REST" developed by Facebook.
- GraphQL is a query language for APIs - not databases.
- It uses declarative data fetching, while REST uses resource endpoints.
- It exposes only one endpoint while REST exposes mutliple endpoints.
- You write the data that you want, and you get exactly the data that you want. No more over-fetching of information as we are used to with REST "Performance Advantage over REST".

## Why GraphQl

### GraphQL Advantanges vs REST

- REST is an older standard to structure your api.
- API using REST has a lot of endpoints "one for each resource action".
- It’ll be much harder for developers to learn and understand your API.
- Overfetching "fetching unneccessary data" and Underfetching Problem "data is not enough so we need to send another request, usually called n + 1 requests problem".
- Rapid product iterations. You don't need to change the api each time you change the client.

- GraphQL uses strong types
- All the types that are exposed in an API are written down in a schema using the GraphQL Schema Definition Language ```SDL```. This schema serves as the contract between the client and the server to define how a client can access the data.
