# Feature Tracker
The feature tracker application will serve as a centralized hub for product development teams and users 
to monitor the implementation status of features across multiple products, track their release cycles, 
and identify areas for improvement. Additionally, user feedback will be collected and analyzed to provide 
actionable insights on which features are most well-received by users.

## Prerequisites
You need to install the following software:

* JDK 21 or later
* Docker ([installation instructions](https://docs.docker.com/engine/install/))
* [IntelliJ IDEA](https://www.jetbrains.com/idea/)
* [Taskfile](https://taskfile.dev/)

## Application Architecture
The feature tracker application is being developed following Microservices Architecture.
This application has the following services:

* **feature-service**: Manages products, features, releases. [See more](https://github.com/feature-tracker/feature-service/blob/main/README.md)
* **user-service**: Manages users by interacting with Keycloak. [See more](https://github.com/feature-tracker/user-service/blob/main/README.md)
* **notification-service**: Handles events published by other services and sends notification emails. [See more](https://github.com/feature-tracker/notification-service/blob/main/README.md)
* **config-server**: Central Config server to store all the microservices configuration. [See more](https://github.com/feature-tracker/config-server/blob/main/README.md)
* **api-gateway**: API Gateway to store all the microservices. [See more](https://github.com/feature-tracker/api-gateway/blob/main/README.md)
* **feature-tracker-angular**: Frontend SPA for feature-tracker application. [See more](https://github.com/feature-tracker/feature-tracker-angular/blob/main/README.md)

## Getting Started
The application components are published as Docker images on DockerHub.
The Keycloak Identity Management System is used as an OAuth 2.0 server to secure the application.


> **IMPORTANT:**
> 
> Frontend application uses front-channel to login with Keycloak.
> Backend microservices uses back-channel to validate auth tokens.
> 
> To use the same host name for both scenarios, 
> add the host name `keycloak` to `/etc/hosts` file pointing to `127.0.0.1`.
>
> ```shell
> 127.0.0.1   keycloak
> ```
>

[Task](https://taskfile.dev/) is a task runner that we can use to run any arbitrary commands in an easier way.

Install [Task CLI](https://taskfile.dev/installation/).

```shell
$ brew install go-task
(or)
$ go install github.com/go-task/task/v3/cmd/task@latest

#verify task version
$ task --version
Task version: 3.35.1
```

Now, you can run the application locally using docker-compose as follows:

```shell
$ git clone https://github.com/feature-tracker/docker-infra.git
$ cd docker-infra
$ task start
```

You can access the Feature Tracker application at http://localhost:4200

## Local Development

**1.Clone the repositories**

```shell
$ git clone https://github.com/feature-tracker/docker-infra.git
$ git clone https://github.com/feature-tracker/api-gateway.git
$ git clone https://github.com/feature-tracker/config-server.git
$ git clone https://github.com/feature-tracker/feature-service.git
$ git clone https://github.com/feature-tracker/notification-service.git
$ git clone https://github.com/feature-tracker/user-service.git
$ git clone https://github.com/feature-tracker/feature-tracker-angular.git
```

**2. Build Docker images of all the components**

```shell
$ cd docker-infra
$ ./local-build.sh
```

**3.Start the entire application**

You can start all the components of the system and their dependent services(Keycloak, databases, message brokers, etc.) 
using Docker Compose by running the following command:

```shell
$ task start
```

Once all the services have been started, you should be able to invoke API endpoints via API Gateway.

Examples:

* `curl http://localhost:8989/features/api/products`

You can access the Feature Tracker application at http://localhost:4200

**4.Debugging/Running Microservices from IDE**

You may want to start the infra components as Docker containers and run specific microservice from IDE.

In that case, start all the infra components(Keycloak, databases, message brokers, etc.) as follows:

```shell
$ cd docker-infra
$ task start_infra
```

Now, you can run the individual microservices from the IDE.

## How to contribute?
* Run the application and let us know if you face any issue
* Review the code and add your review comments
