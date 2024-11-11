# Feature Tracker
The feature tracker application will serve as a centralized hub for product development teams and users 
to monitor the implementation status of features across multiple products, track their release cycles, 
and identify areas for improvement. Additionally, user feedback will be collected and analyzed to provide 
actionable insights on which features are most well-received by users.

## Local Development
You need to install the following software:

* JDK 21 or later
* Docker ([installation instructions](https://docs.docker.com/engine/install/))
* [IntelliJ IDEA](https://www.jetbrains.com/idea/)
* [Taskfile](https://taskfile.dev/)

1. Clone the repositories
    ```shell
    $ git clone https://github.com/feature-tracker/docker-infra.git
    $ git clone https://github.com/feature-tracker/api-gateway.git
    $ git clone https://github.com/feature-tracker/feature-service.git
    ```
2. Start all the required services(Keycloak, databases, message brokers, etc.)
   ```shell
   $ cd docker-infra
   $ task start_infra
   ```
3. Run backend microservices.

   You can run the individual microservices from the IDE. 

   Alternatively, you can start all the microservices and their dependent services using Docker by running the following command:
   ```shell
   $ task start
   ```

## How to contribute?
* Run the application and let us know if you face any issue
* Review the code and add your review comments
