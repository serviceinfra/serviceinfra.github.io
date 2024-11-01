---
layout: page
title: The Service Management API
---
API management starts with knowing what your APIs are, and the Service Management API is used to build a list and digest it into a form that allows API proxies to check and report API traffic.

The Service Management API manages descriptions of APIs, focusing on the service configurations that control their usage. Service Configuration is the central format of Service Management, and arose from Google internal API practice. It consists of the [Service](https://github.com/googleapis/googleapis/blob/d54f4e947e77b86ea2e0e243c92a174032098a54/google/api/service.proto#L47) proto and the messages that it contains. API designers provide it in YAML files that match the Protocol Buffer schema. Often developers only provide fragments of the full "service config" and tools fill in the rest.

### What's in the Service Configuration

An example full service config is in [stores.endpoints.bobadojo.cloud.goog.2024-10-18r0.json](/examples/stores.endpoints.bobadojo.cloud.goog.2024-10-18r0.json). Clearly this is not something that a developer would want to manually create! In practice, the service config is an intermediate internal format used by Cloud Endpoints. Developers instead provide fragments, like the one in [api_config.yaml](/examples/api_config.yaml), which contain only the parts of service config that can't be automatically derived from other known things.

### The Service Management API methods

The methods of the Service Management API are defined in [google/api/servicemanagement/v1/servicemanager.proto](https://github.com/googleapis/googleapis/blob/d54f4e947e77b86ea2e0e243c92a174032098a54/google/api/servicemanagement/v1/servicemanager.proto#L39).

-  rpc ListServices
-  rpc GetService
-  rpc CreateService
-  rpc DeleteService
-  rpc UndeleteService
-  rpc ListServiceConfigs
-  rpc GetServiceConfig
-  rpc CreateServiceConfig
-  rpc SubmitConfigSource
-  rpc ListServiceRollouts
-  rpc GetServiceRollout
-  rpc CreateServiceRollout
-  rpc GenerateConfigReport

#### List services

Try it.

`q servicemanagement list-apis`

#### Get details of a service

Try it.

`q servicemanagement get-api`

#### Create a service 

Try it.

What names are we allowed to use?

$ q servicemanagement create-service foo bobadojo
Error: Status { code: PermissionDenied, message: "Ownership for domain name 'foo' on project 'bobadojo' cannot be verified.", metadata: MetadataMap { headers: {"x-debug-tracking-id": "14599521392138793457;o=0", "content-type": "application/grpc", "date": "Sat, 13 Jul 2024 03:39:52 GMT", "alt-svc": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"} }, source: None }

$ q servicemanagement create-service foo.endpoints.bobadojo.cloud.goog bobadojo
service=Response { metadata: MetadataMap { headers: {"content-disposition": "attachment", "content-type": "application/grpc", "x-debug-tracking-id": "7176991653359097728;o=0", "date": "Sat, 13 Jul 2024 03:40:06 GMT", "alt-svc": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000", "grpc-status": "0"} }, message: Operation { name: "operations/services.foo.endpoints.bobadojo.cloud.goog-0", metadata: Some(Any { type_url: "type.googleapis.com/google.api.servicemanagement.v1.OperationMetadata", value: [10, 42, 115, 101, 114, 118, 105, 99, 101, 115, 47, 102, 111, 111, 46, 101, 110, 100, 112, 111, 105, 110, 116, 115, 46, 98, 111, 98, 97, 100, 111, 106, 111, 46, 99, 108, 111, 117, 100, 46, 103, 111, 111, 103, 34, 11, 8, 150, 238, 199, 180, 6, 16, 248, 207, 151, 118] }), done: false, result: Some(Response(Any { type_url: "type.googleapis.com/google.api.servicemanagement.v1.ManagedService", value: [18, 33, 102, 111, 111, 46, 101, 110, 100, 112, 111, 105, 110, 116, 115, 46, 98, 111, 98, 97, 100, 111, 106, 111, 46, 99, 108, 111, 117, 100, 46, 103, 111, 111, 103, 26, 8, 98, 111, 98, 97, 100, 111, 106, 111] })) }, extensions: Extensions }

$ q servicemanagement create-service foo.bobadojo.appspot.com bobadojo
service=Response { metadata: MetadataMap { headers: {"content-disposition": "attachment", "content-type": "application/grpc", "x-debug-tracking-id": "9253787921377858843;o=0", "date": "Sat, 13 Jul 2024 03:40:22 GMT", "alt-svc": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000", "grpc-status": "0"} }, message: Operation { name: "operations/services.foo.bobadojo.appspot.com-0", metadata: Some(Any { type_url: "type.googleapis.com/google.api.servicemanagement.v1.OperationMetadata", value: [10, 33, 115, 101, 114, 118, 105, 99, 101, 115, 47, 102, 111, 111, 46, 98, 111, 98, 97, 100, 111, 106, 111, 46, 97, 112, 112, 115, 112, 111, 116, 46, 99, 111, 109, 34, 11, 8, 166, 238, 199, 180, 6, 16, 136, 218, 150, 112] }), done: false, result: Some(Response(Any { type_url: "type.googleapis.com/google.api.servicemanagement.v1.ManagedService", value: [18, 24, 102, 111, 111, 46, 98, 111, 98, 97, 100, 111, 106, 111, 46, 97, 112, 112, 115, 112, 111, 116, 46, 99, 111, 109, 26, 8, 98, 111, 98, 97, 100, 111, 106, 111] })) }, extensions: Extensions }


This is because we get DNS service from Google at domains matching our service name.


https://cloud.google.com/endpoints/docs/openapi/cloud-goog-dns-configure

suggestions for using project names thoughtfully:

https://cloud.google.com/endpoints/docs/openapi/planning-cloud-projects

#### Delete (and undelete!) a service

Try it.

look at the stores service in endpoints

delete the stores Service

look now in endpoints -- it's gone!
the api calls don't work now either 

undelete the stores service 

look now in endpoints -- it's back 
the api calls might not work right away but they will after a few minutes.

#### List service configurations

Try it.
```
q service-management list-service-configs echo.endpoints.terminate-me.cloud.goog | jq .[].id
```
#### Get a service configuration

Try it.

#### Create a service configuration

There are two ways to do this.

Try it.

#### List service rollouts

Try it.

#### Get details of a service rollout

Try it.

#### Create a service rollout

Try it.

#### Review configuration changes

Try it.

q servicemanagement generate-config-report services/stores.endpoints.bobadojo.cloud.goog/configs/2024-07-13r0


#### Submit Config Source

q service-management submit-config-source stores.endpoints.bobadojo-0005.cloud.goog ./stores-demo/api_config.yaml  ./stores-demo/descriptor.pb 

q service-management get-operation operations/serviceConfigs.stores.endpoints.bobadojo-0005.cloud.goog:537024da-fdca-4c1c-8c33-5dbf1eb13e1a | jq .response.serviceConfig | head


#### Generate Config Report

q service-management generate-config-report services/stores.endpoints.bobadojo-0005.cloud.goog/configs/2024-07-19r3
