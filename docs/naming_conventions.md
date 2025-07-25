The platform impose several constraints with regards to the naming of the persistence elements (files, databases, tables and collections). Such constraints, and the way the different storages solve them, must be had into account when designing the data model of the solution running on top of the platform.

# Global character set and size limitations
Globally, the platform impose certain rules when defining the data model. These rules directly come from Orion Context Broker [constraints](https://github.com/telefonicaid/fiware-orion/blob/master/doc/manuals/orion-api.md#general-syntax-restrictions) regarding the character set used for entity and attribute names and their types:

* The following charaters are forbidden: `<`, `>`, `"`, `'`, `=`, `;`, `(` and `)`.
* The following ones should also be avoided: white space, `?`, `/`, `%` and `&`.

Additionally, Orion Context Broker imposes the following restrictions:

* The [FIWARE-service](https://github.com/telefonicaid/fiware-orion/blob/master/doc/manuals/orion-api.md#multi-tenancy) must be a string of alphanumeric characters including the underscore, whose maximum length is 50 characters.
* The [FIWARE-servicePath](https://github.com/telefonicaid/fiware-orion/blob/master/doc/manuals/orion-api.md#service-path) must be a string defining a Unix-like path starting with slash and having maximum 10 levels; being each level a string of alphanumeric characters including the underscore, whose maximum lenght is 50 characters. Nevertheless, the platform currently only allows a single level.

All these limitations imposed by Orion Context Broker are propagated to the storages via Cygnus connectors with PostgreSQL and MongoDB.

# PostgreSQL character set and size limitations
Persisting context data in [PostgreSQL](https://fiware-cygnus.readthedocs.io/en/master/cygnus-ngsi/flume_extensions_catalogue/ngsi_postgresql_sink.html) implies creating databases and tables, whose names are constrained to 63 character strings of alphanumerics and underscore:

* Databases: `<FIWARE-service>`
* Tables: `<FIWARE-servicePath>_<entityID>_<entityType>`.

Any other character within the FIWARE-service, FIWARE-servicePath, entity ID and type different than alphanumerics and underscore is replaced by underscore.

# MongoDB character set and size limitations
Persisting context data in [MongoDB](https://fiware-cygnus.readthedocs.io/en/master/cygnus-ngsi/flume_extensions_catalogue/ngsi_mongo_sink.html) implies creating databases and collections:

* Databases: `<FIWARE-service>`.
* Collections: `<FIWARE-servicePath>`.

Whose names are constrained this way by [MongoDB](https://docs.mongodb.com/manual/reference/limits/#naming-restrictions):

* `/`, `\`, `.`, `"` and `$` are not accepted in the database names. Database names cannot be empty and must have fewer than 63 characters.
* `$`, the empty string and the null character are not accepted in the collection names. In addition, collections cannot start with the `.system` prefix. The maximum length of the collection namespace, which includes the database name, the dot separator, and the collection name (i.e. `<database>.<collection>`), is 113 bytes.

Nevertheless, the above restrictions do not affect the platform because of the limitations imposed to the FIWARE-service and the FIWARE-servicePath.

