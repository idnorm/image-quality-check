# Image Quality Check

This repository holds documentation on how to use and integrate the image quality check tool.

## Cloud SaaS

The extraction service is available as an API hosted on `iq.idnorm.com`. It implements RESTful and gRPC APIs one can use
for service integration.

## Hosting on-premise

Our extraction service can be hosted on your infrastructure. We provide two main deployment options
 - smaller scale and testing solutions can be effortlessly deployed using our prepared [docker-compose configuration](onprem/docker-compose).
 - for production purposes, where horizontal scaling is "a must", we release and maintain the helm chart package (Coming soon)

# API

Both Cloud SaaS and On-premise solutions use the same APIs. For integration
we offer gRPC and REST APIs you can use to communicate with the service.

## REST

REST is, arguably, still the most popular choice for building backend services APIs. Therefore, our ID extraction service comes with REST as well as gRPC API.

API documentation is maintained and shipped using Swagger.

**The latest version** of the swagger documentation can be found [here](https://iq.apidocs.idnorm.com).

In the documentation you can find all the details about available paths, expected request and response payloads, and different request configuration options.

### Example

Here we provide a simple bash script you can use to test out and send "one off" requests. To the
image quality check API REST endpoint.

If you want to use the Cloud SaaS endpoint, you need to provide your license key as an environment variable:

```bash
export IDNORM_LICENSE_KEY=<your license key here>
export ENDPOINT=https://iq.idnorm.com
./send-rest-request.sh
```

## gRPC

Focusing on performance, readability, and ease of code integration we recommend using gRPC whilst integrating our
extraction solution. Working with gRPC and protobuf for the first time can have a challenging learning curve.
To make working with gRPC enjoyable and easy we leverage [buf build tool](https://buf.build/docs/introduction). Here we will provide more information on how to use it to integrate our solution.

Simply put, Buf is a tool that helps configure and execute [protoc](https://grpc.io/docs/protoc-installation/) plugins to generate code you can then use to integrate our gRPC service with your codebase.

Buf also provides us with his [protobuf schema registry](https://buf.build/explore) where one can publish its gRPC/protobuf service schema definitions. You can think of it as a "git" for protobuf schema definitions.

On the bufs schema registry, we publish our service definitions.


### Image Quality Check schema

**The latest version** of our service schema can be found [here](https://buf.build/idnorm/iq/docs/main:proto.iq.v1).

There you can see detailed documentation on the available methods service defines, as well as input and output messages.
There you can find all information about input data requirements, what is the expected result the service will return, as well as
different options for request configurations.
