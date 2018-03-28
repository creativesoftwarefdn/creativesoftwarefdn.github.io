---
layout: default
---

# Using Weaviate

This page is about using the Weaviate API's. If you want to setup and run Weaviate, or create an ontology, please read [this page](/weaviate/setting-up-weaviate).

## Using Weaviate Keys

Weaviate has two keys. A key and a token. The key functions as a loginname and a token as a password. The key is stored as plaintext in the UUID format and the token is stored using the [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt) hash function.

A token kan be refreshed, a key can't.

#### Working With Keys

Weaviate works with API keys which are set in the header (`X-API-KEY: [[apiKey]]` & `X-API-TOKEN: [[apiToken]]`) and are formatted as a UUID; every key is related to a request if you create a thing or action, the key that you use will be attached to this object. You can create as many keys and children of keys, creating a new key automatically makes the key a child of the request key.

The rules for keys within Weaviate are:

1. A new key created by a request key will make the new key a child of the request key.
2. A parent key always has access to a child key.

Requesting information about the current key can be done like this:

```
curl -X GET -H "X-API-KEY: [[apiKey]]" -H "X-API-TOKEN: [[apiKey]]" "https://localhost/weaviate/v1/keys/me"
```

Requesting an overview of children of a key can be done like this:

```
curl -X GET -H "X-API-KEY: [[apiKey]]" -H "X-API-TOKEN: [[apiKey]]" "https://localhost/weaviate/v1/keys/me/children"
```

A child key can be created like this:

```
curl -X POST -H "X-API-KEY: [[apiKey]]" -H "X-API-TOKEN: [[apiKey]]" "https://localhost/weaviate/v1/keys"
```

And information from a specific child key can be requested like this:

```
curl -X GET -H "X-API-KEY: [[apiKey]]" -H "X-API-TOKEN: [[apiKey]]" "https://localhost/weaviate/v1/keys/{keyId}"
```

## Using the Weaviate RESTful API

Weaviate can be accessed directly through the RESTful API's. This is handy to create or update single things or actions. In case you want to crawl the graph, it is advised to use the GraphQL endpoint.

A complete overview of the RESTful API endpoints can be found [here](#), a Swagger document is available [here](https://github.com/creativesoftwarefdn/weaviate/tree/master/swagger).

In the [examples](/weaviate/examples) directory, you can find [RESTful API examples](#) based on the demo dataset.

## Using GraphQL to explore Weaviate

...

## Using MQTT

...

[back](../)

