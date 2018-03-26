---
layout: default
---

# Dataflow

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


[back](../)

