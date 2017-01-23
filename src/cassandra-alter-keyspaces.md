**Cassandra - Alter Keyspace**

**Alter Keyspace using Cqlsh**

ALTER KEYSPACE can be used to alter properties such as the number of replicas and the durable_writes of a KeySpace. Given below is the syntax of this command.

Syntax
```sql
ALTER KEYSPACE <identifier> WITH <properties>
```

i.e.
```sql
ALTER KEYSPACE “KeySpace Name”
WITH replication = {'class': ‘Strategy name’, 'replication_factor' : ‘No.Of  replicas’};
```

The properties of ALTER KEYSPACE are same as CREATE KEYSPACE. It has two properties: replication and durable_writes.

**Durable_writes**

Using this option, you can instruct Cassandra whether to use commitlog for updates on the current KeySpace. This option is not mandatory and by default, it is set to true.

Example

Given below is an example of altering a KeySpace.

* Here we are altering a KeySpace named TutorialsPoint.
* We are changing the replication factor from 1 to 3.

```sql
cqlsh.> ALTER KEYSPACE tutorialspoint
WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 3};
```

**Altering Durable_writes**

You can also alter the durable_writes property of a KeySpace. Given below is the durable_writes property of the test KeySpace.
```sql
SELECT * FROM system_schema.keyspaces;

  keyspace_name | durable_writes |                                       strategy_class | strategy_options
----------------+----------------+------------------------------------------------------+----------------------------
           test |          False | org.apache.cassandra.locator.NetworkTopologyStrategy | {"datacenter1":"3"}

 tutorialspoint |           True |          org.apache.cassandra.locator.SimpleStrategy | {"replication_factor":"4"}

         system |           True |           org.apache.cassandra.locator.LocalStrategy | { }

  system_traces |           True |          org.apache.cassandra.locator.SimpleStrategy | {"replication_factor":"2"}
(4 rows)
ALTER KEYSPACE test
WITH REPLICATION = {'class' : 'NetworkTopologyStrategy', 'datacenter1' : 3}
AND DURABLE_WRITES = true;
```

Once again, if you verify the properties of KeySpaces, it will produce the following output.
```sql
SELECT * FROM system.schema_keyspaces;
  keyspace_name | durable_writes |                                       strategy_class | strategy_options
----------------+----------------+------------------------------------------------------+----------------------------
           test |           True | org.apache.cassandra.locator.NetworkTopologyStrategy | {"datacenter1":"3"}

 tutorialspoint |           True |          org.apache.cassandra.locator.SimpleStrategy | {"replication_factor":"4"}

         system |           True |           org.apache.cassandra.locator.LocalStrategy | { }

  system_traces |           True |          org.apache.cassandra.locator.SimpleStrategy | {"replication_factor":"2"}

(4 rows)
Altering a Keyspace using Java API
```
