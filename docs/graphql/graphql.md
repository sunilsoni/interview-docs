---
title: GraphQL
has_children: true
nav_order: 2
resource: true
desc: "GraphQL interview questions and answers."
categories: [GraphQL]
---

---

# GraphQL
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## GraphQL

GraphQL is a query language for APIs that was developed by Facebook. It allows clients to define the structure of the data that they require from an API, and the server will return exactly that data, and only that data. Here are some of the key components of GraphQL:

###  Queries

Queries are used by clients to request data from a GraphQL API. A query is a hierarchical set of fields and sub-fields that define the data that the client is requesting. Here is an example of a GraphQL query:

```scss
query {
user(id:123) {
  name
  email
  posts {
    title
    content
  }
}
}
```

This query is requesting the name and email of a user with an ID of 123, as well as the titles and content of all of that user's posts.


###  Mutations

Mutations are used by clients to modify data in a GraphQL API. A mutation is similar to a query, but it is used to make changes to the data, such as adding or deleting an object. Here is an example of a GraphQL mutation:

```scss
mutation {
addUser(name: "John Doe", email: "john@example.com") {
  id
  name
  email
}
}


```
This mutation is adding a new user to the API with a name of "John Doe" and an email of "john@example.com", and it is requesting the new user's ID, name, and email.

###  Types

Types are used by GraphQL to define the shape of the data that is available in the API. Types can be simple scalar types like strings and numbers, or they can be more complex object types that have their own fields and sub-fields. Here is an example of a GraphQL type:

```scss

type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post!]!
}

```

This type defines a User object that has an ID, name, email, and a list of posts. The exclamation marks indicate that these fields are required.

###  Resolvers
Resolvers are functions that are used by a GraphQL server to fetch data from a data source and return it to the client. Each field in a query or mutation has its own resolver function that is responsible for fetching the data for that field. Here is an example of a resolver function:


```scss
function getUserById(id) {
  // fetch user from database
  return {
    id: user.id,
    name: user.name,
    email: user.email,
    posts: getPostsByUserId(user.id),
  };
}


```

This resolver function takes an ID as an argument and fetches a user from a database, along with that user's posts. It then returns an object that matches the shape of the User type.


