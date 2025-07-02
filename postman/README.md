You can get Postman here: https://www.getpostman.com/

In order to use the Postman collection included in this directory (https://github.com/telefonicaid/thinking-cities/blob/master/postman/ThinkingCities%20APIs%20Basic%20Ops.postman_collection.json), you need to define the following variables in your environment:

* **PROTOCOL**: protocol used for the APIs (https or http)
* **ENDPOINT_CB**: the host:port for context broker requests
* **ENDPOINT_KEYSTONE**: the host:port for keystone requests
* **ENDPOINT_IOTAM**: the host:port for iot agent manager. Used for provision requests
* **ENDPOINT_IOTA_UL_HTTP**: the host:port for sending UL mesaures
* **ENDPOINT_IOTA_JSON_HTTP**: the host:port for sending JSON measures
* **ENDPOINT_CEP**: the host:port for CEP requests
* **ENDPOINT_CKAN**: the host:port for CKAN requests
* **CKAN_APIKEY**: apikey used for CKAN authetication
* **SERVICE**: service to use in `Fiware-Service` header
* **SUBSERVICE**: subservice to use in the `Fiware-ServicePath` header
* **USER**: user (used by the "Get auth token" operation)
* **PASSWORD**: password (used by the "Get auth token" operation)
* **JSON_APIKEY**: API key used for IOTA JSON requests
* **UL_APIKEY**: API key used for IOTA JSON requests

In addition, note that a TOKEN global variable is automatically added to your environment once you execute the "Get auth token (service)" request or "Get auth token (subservice)" request using the `x-subject-token` header in the response. This is the token used for the `X-Auth-Token` header in the requests requiring so.
