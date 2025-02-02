# Apache Iceberg

[Apache Iceberg](https://iceberg.apache.org/) is an Apache Software Foundation project that provides a rich, relatively new
table format. It provides:

* Single table ACID transactions
* Scalable metadata
* Appends via file addition
* Updates, deletes and merges via single record operations

## Iceberg Extension Points

Iceberg exposes two primary classes for working with datasets. These are Catalog and
TableOperations. Nessie implements each. These classes are available in the
the [Iceberg source code](https://github.com/apache/iceberg/tree/master/nessie/src/main/java/org/apache/iceberg/nessie)
and are available directly in Iceberg releases (eg `spark-runtime`, `spark3-runtime`, `flink-runtime`).

## Iceberg Snapshots

Iceberg supports the concept of snapshots. Snapshots are point in time versions of
a table and are managed as part of each commit operation. Snapshots are limited to
single table versioning. Nessie versions and commits provide a broader set of snapshot
capabilities as they support multiple tables. Nessie is happy to
coexist with Iceberg Snapshots. When working with Nessie, Iceberg snapshots will also
be versioned along the rest of Iceberg metadata within the Nessie commit model.

### Automatic Snapshot Import

We are exploring the [creation of a tool](https://github.com/projectnessie/nessie/issues/126) where a
user can import table snapshots across multiple Iceberg tables into a single Nessie
repository to capture historical data snapshots (interleaved across time).
