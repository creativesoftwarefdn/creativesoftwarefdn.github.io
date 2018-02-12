---
layout: default
---

# Weaviate [![Build Status](https://travis-ci.org/creativesoftwarefdn/weaviate.svg?branch=develop)](https://travis-ci.org/creativesoftwarefdn/weaviate/branches)

Weaviate is a decentralized, Semantic Graphql, RESTful Web of Things platform. With Weaviate you can create a graph of things. Regardless if it is a smart building 🏢, a crash of elephants 🐘 or a fleet of spaceships 🚀. With Weaviate you can create a time-based Web of Things Graph, and you can make relations cross-platform (i.e., relate an elephant to a spacecraft 😄👍).

## Index

- [Concept in a Nutshell](#concept-in-a-nutshell)
- [Creating a Custom Ontology](#creating-a-custom-ontology)
- [Setting Up a Database](#setting-up-a-database)
    - [Cassandra](#cassandra)
- [Run Weaviate](#run-weaviate)
    - [Download Binary](#download-binary)
    - [Compile from Source](#compile-from-source)
    - [Run with Docker](#run-with-docker)
- [Getting Started with Weaviate](#getting-started-with-weaviate)
- [Use the Weaviate RESTful API](#use-the-weaviate-restful-api)
- [Using GraphQL to explore Weaviate](#using-graphql-to-explore-weaviate)
- [Dataflow](#dataflow)
- [Create a Database Connector](#create-a-database-connector)

## Concept in a Nutshell

Weaviate is based on web semantics. Meaning

Additionally, you might want to read: [A Semantic Internet of Things](https://bob.wtf/semantic-internet-of-things-42811e1ca7a7) on [bob.wtf](https://bob.wtf).

## Creating a Custom Ontology

...

## Setting Up a Database

Currently, Weaviate only supports Cassandra, in the future, we want to support more wide-column databases, if you want to [request](https://github.com/creativesoftwarefdn/weaviate/issues) a database connector or if you want to [contribute](), please make sure to follow the links mentioned above.

#### Cassandra

You can run Weaviate on practically any Cassandra set up you want to. If you simply want to get started with Weaviate, you can run Cassandra with Docker.

```
docker run -it --name weaviate -e CASSANDRA_BROADCAST_ADDRESS=127.0.0.1 -p 7000:7000 -p 9042:9042 -v /Users/[YOUR-USERNAME]/cassandra:/var/lib/cassandra cassandra:3
```
_Make sure to change [YOUR-USERNAME] with the username of the current user._

## Run Weaviate

There are several ways to run Weaviate.

## Getting Started with Weaviate

...

#### Download Binary

> Note: We are working towards a first version.

Download Nightly Build

```
$ curl -o weaviate_bin https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_$(echo `uname`|tr '[:upper:]' '[:lower:]')_amd64.zip
$ chmod +x weaviate_bin
```

Download Nightly Builds

| OS and Architecture
| -------------------
| [weaviate_nightly_darwin_386.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_darwin_386.zip)
| [weaviate_nightly_darwin_amd64.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_darwin_amd64.zip)
| [weaviate_nightly_linux_386.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_386.zip)
| [weaviate_nightly_linux_amd64.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_amd64.zip)
| [weaviate_nightly_linux_arm.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_arm.zip)
| [weaviate_nightly_linux_mips.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_mips.zip)
| [weaviate_nightly_linux_mips64.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_mips64.zip)
| [weaviate_nightly_linux_mips64le.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_mips64le.zip)
| [weaviate_nightly_linux_mipsle.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_mipsle.zip)
| [weaviate_nightly_linux_ppc64.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_ppc64.zip)
| [weaviate_nightly_linux_ppc64le.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_linux_ppc64le.zip)
| [weaviate_nightly_windows_386.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_windows_386.zip)
| [weaviate_nightly_windows_amd64.zip](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_windows_amd64.zip)

[Checksum file](https://storage.cloud.google.com/weaviate-dist/nightly/weaviate_nightly_checksums.txt).

#### Compile from Source

Setup Go Releaser and compile from source.

```
$ go get github.com/goreleaser/goreleaser
$ goreleaser --rm-dist --snapshot --skip-validate
```

#### Run with Docker

```
$ curl https://git.io/vdwgr -sL | sudo bash
```

_Note: Make sure to install `jq`_.

## Use the Weaviate RESTful API

...

## Using GraphQL to explore Weaviate

...

## Dataflow

The data flow is visualized in the following diagram:

![Data Flow](/assets/img/data-flow.png)

These connector-functions are getting data from the database and this is where the Cassandra data model is based on.

Function | Description | Select | Where 1 | Where 2 | Limit | Order | Delete
-|-|-|-|-|-|-|-
Init() | Initialize database needs the current root key | count | type = ‘Key’ | properties.root = ‘true’ | 1 | - | -
GetThing() | Get a single thing based on uuid | * | uuid = uuid | - | 1 | timestamp | 1
GetThings() | Get batch of things based on uuid | * | uuid IN [uuid] | - | 1 per uuid | timestamp | 1
ListThings() | Get list of things based on key-uuid, sorted by most recent | * | owner = uuid | Search on class, search on property value (wildcard). | X | timestamp | 1
GetAction() | Get single action based on uuid | * | uuid = uuid | - | 1 | timestamp | 1
GetActions() | Get batch of actions based on uuid | * | uuid IN [uuid] | - | - | - | 1
ListAction() | Get list of actions based on key-uuid, sorted by most recent | * | properties.things.object.cref = ‘uuid’ | Search on class, search on property value (wildcard). | X | timestamp | 1
ValidateToken() | Validate token based on given property ‘token’ | * | type = ‘Key’ | properties.token = ‘uuid’ | 1 | - | 1
GetKey() | Get a single key based on uuid | * | uuid = uuid | - | 1 | - | 1
GetKeyChildren() | Get batch of keys based on parent key in properties | * | properties.parent.cref = ‘uuid’ | - | - | timestamp | -

## Create a Database Connector

...

[back](/)

