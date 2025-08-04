The ThinkingCity is a [powered by FIWARE platform](http://marketplace.fiware.org/pages/solutions/c5940dbbdfbcf694f6cdf6ec)
which allows you to connect devices and receive data, integrating all device protocols
and connectivity methods, understanding and interpreting relevant information.
It combines Telefónica components with FIWARE Generic Enablers and isolates data
processing and application service layers from the device and network complexity,
in terms of access, security and network protocols.

These are the main benefits of ThinkingCity platform:

\- Simple sensor data integration

\- Device-independent APIs for quick app development \& lock-in prevention

\- Modular

\- Scalable. High available

\- Open \& standards based. FIWARE compliant

## APIs available

ThinkingCity provides the following APIs:

\- [Authentication API](authentication_api.md): manages tokens for APIs usage.

\- [Authorization with grants API](authorization_api.md): manages grants.

\- [Device API](device_api.md): allows managing devices, sending data from the device to the cloud and receiving commands.

\- [Data API](data_api.md): allows querying and subscribing to data stored at the cloud.

\- [CEP API](cep_api.md): allows analyzing data from your IoT device and triggering actions.

\- [Management API](management_api.md): allows creating new services and users to provide a multi-tenant environment.

## Multitenancy

ThinkingCity multitenancy model is described [in this section](multitenancy.md).

## Data persistence

FIWARE IoT Data capabilities go far beyond querying the current context data or the short-term history. ThinkingCity provides means for storing hitorical data in third-party components; the following ones:

\- [PostgreSQL](http://www.postgresql.org/), the well-know relational database manager.

\- [MongoDB](https://www.mongodb.org/), the NoSQL document-oriented database.

## FIWARE Components

ThinkingCity is based on the following [FIWARE components](walkthrough.md) in order to provide its functionality:

The following components used by ThinkingCity have been contributed as open source to FIWARE and can be found within the [FIWARE Catalogue](https://github.com/Fiware/catalogue/):

\- IoTAgents (IoTA)

\- Context Broker (Orion)

\- Connector Framework (Cygnus)

\- Complex Event Processing (Perseo)

The platform also includes the following additional component, which is not part of FIWARE (but still remains open source):

\- IoT Orchestrator

The ThinkingCity platform does not use the Identity Management (IDM), Policy Enforcement Point (PEP) and
Access Control (AC) from the FIWARE Catalogue. The platform contains its own bespoke security components conforming
with the same GE specifications (see [this clarification](https://ask.fiware.org/question/1/what-is-a-fiware-ge-and-a-gei/) about GE, GEi and GEri terms).

## FIWARE Datamodels

ThinkingCity recommends the use of the standard
FIWARE data models which can be found [here](https://github.com/smart-data-models).

