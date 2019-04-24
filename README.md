This repo contains all the  materials for the course MongoDB for Java Developers, in order to run a MongoDb in a docker container, import provided data, connect to the created atlas cluster and complete the tickets.

## Docker

The docker-compose materials is located at [docker](docker/) folder, they contain:
- The docker-compose.yml file which runs the latest mongodb database

### Running the container

To run the container go to the [docker](docker/) folder and then run the following command in a CLI:

```bash
$ docker-compose up
```

Or to run in detached mode (background):

```bash
$ docker-compose up -d
```

After successfully run the container, run the following command and copy the CONTAINER ID:

```bash
$ docker container ls
```

### Connecting to my Atlas cluster

Now run the following command to connect to the Atlas cluster:

```bash
$ docker exec -it [REPLACE_WITH_CONTAINER_ID] mongo "mongodb+srv://mflix-qkurq.mongodb.net/test" --username m220student --password [REPLACE_WITH_PASSWORD]
 ```

 To get the password go to the protected link https://thinfi.com/9jsj and copy the password provided in the step 7.

 ### Importing provided data to Atlas cluster

After connect to Atlas cluster, run the following commands to import the data to the Atlas cluster:

```bash
$ cd handouts/mflix-java
$ docker cp data/ [REPLACE_WITH_CONTAINER_ID]:/
 ```

 Check if the ```data``` folder is in the correct path using the command:

 ```bash
$ docker diff [REPLACE_WITH_CONTAINER_ID]
 ```

And then use ```mongorestore``` to import the data:

```bash
$ docker exec -it [REPLACE_WITH_CONTAINER_ID] mongorestore --drop --gzip --uri mongodb+srv://m220student:m220password@mflix-qkurq.mongodb.net data
 ```

 ### Running the Application

 In the mflix-java/src/main/resources directory you can find a file called ```application.properties```.

Open this file and enter your Atlas SRV connection string as directed in the comment. This is the information the driver will use to connect. Make sure not to wrap your Atlas SRV connection between quotes:

```yml
spring.mongodb.uri=mongodb+srv://m220student:[REPLACE_WITH_PASSWORD]@mflix-qkurq.mongodb.net
```

Run the application with maven:

 ```bash
$ cd handouts/mflix-java
$ mvn spring-boot:run
 ```

 And then point your browser to http://localhost:5000/.