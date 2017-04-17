# General Notes

## GraphQL
How To Get Started With GraphQL ([Video](https://www.youtube.com/watch?v=xBAJ5nQkeiM))

A Brief Introduction to GraphQL ([Video](https://www.youtube.com/watch?v=7RoyXJ_Rm0Q))

A GraphQL query is a string that is sent to server to be interpreted and fulfilled, which then returns JSON back to the client. (via https://code.facebook.com/posts/1691455094417024/graphql-a-data-query-language/)

GraphQL allows you to bundle data requirements for your qury o it can be servedby one end point.

### Query Document

A GraphQL query document describes a complete file or request string received by a GraphQL service.

Example:
```
{
  me {
    name
  }
}
```
would return:
```json
{
  "me": {
    "name": "Laura Artiles"
  }
}
```
