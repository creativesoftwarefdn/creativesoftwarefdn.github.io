---
layout: default
---

# Setting Up Weaviate

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

Or compile directly for your architecture.

```
$ git clone github.com/creativesoftwarefdn/weaviate
$ cd weaviate
$ go build -o weaviate ./cmd/weaviate-server/main.go
```

#### Configure Weaviate

[HAAL DIT UIT CONFIG_HANDLER.GO THERE IS A STRUCT THAT CONTAINS ALL THAT IS POSSIBLE]
 
#### Run with Docker

Make sure to have `weaviate.conf.json` in the same directory and to set the runtime variables in `docker-compose.yml`.

```
$ git clone github.com/creativesoftwarefdn/weaviate
$ cd weaviate
$ docker-compose up
```

#### Creating a Custom Ontology

[different classes with a prop (like: "location") needs to have the same datatype (int, string, etc). Reason: explain graphql and dbs]

[EXPLAIN CREF and HOW IT LOOKS. Is always edge to another node, can be cross platform (RESTful API used), can only be used in graphQL]

#### Understanding LOGs

[in the terminal, can also enable debug in config]

[back](../)