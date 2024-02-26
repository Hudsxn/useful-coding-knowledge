## CI/CD > Docker > Dockerfile

[<- To Docker](./index.md)

#### ELI5:
Let's imagine you're baking a cake. You have a recipe that tells you what ingredients you need and what steps to follow to make the cake. A Dockerfile is like a recipe for building a cake, but instead of baking ingredients, it specifies what your software needs and how to set it up.

In a Dockerfile:

Base Image: You start with a base ingredient, like flour for a cake. This is an existing image that provides a basic environment, like an operating system (e.g., Linux) or a programming language (e.g., Java).

Instructions: You then add instructions to the Dockerfile, just like adding steps to a recipe. These instructions tell Docker how to build your software environment. For example, you might need to install some software, copy files into the image, or set up configuration.

Build Process: Once you have your Dockerfile ready, you use it to build your Docker image. This is like following the recipe to mix the ingredients and bake the cake. Docker reads the instructions in the Dockerfile and creates a custom image according to those instructions.

Result: The final Docker image is like your finished cake. It contains everything your software needs to run, packaged up in a neat, portable package. You can then use this image to run your software in containers, just like you can slice and serve your cake to enjoy!

So, in simple terms, a Dockerfile is like a recipe for building a software environment, specifying what ingredients (software packages, files, configurations) are needed and how to put them together to create a custom Docker image.

#### Proper explaination

A Dockerfile is a text file that contains instructions for building a Docker image. It specifies the environment and configuration of the image, including the base image to use, any dependencies to install, and commands to run when the image is created.

Here's an example of a Dockerfile for setting up Apache Kafka:

```Dockerfile
# Use a base image with Java installed
FROM openjdk:8-jre-alpine

# Set up environment variables
ENV KAFKA_VERSION=2.8.1
ENV SCALA_VERSION=2.13
ENV KAFKA_HOME=/opt/kafka

# Download and install Kafka
RUN wget -qO- "https://downloads.apache.org/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz" | tar -xzf - -C /opt \
    && mv /opt/kafka_$SCALA_VERSION-$KAFKA_VERSION $KAFKA_HOME

# Set Kafka configuration
WORKDIR $KAFKA_HOME
COPY server.properties $KAFKA_HOME/config/server.properties

# Expose Kafka port
EXPOSE 9092

# Start Kafka server
CMD ["bin/kafka-server-start.sh", "config/server.properties"]
```

Explanation of each section:

1. `FROM openjdk:8-jre-alpine`: Specifies the base image to use. In this case, we're using the official OpenJDK 8 image based on Alpine Linux.

2. `ENV`: Sets environment variables for Kafka version, Scala version, and Kafka home directory.

3. `RUN`: Downloads and installs Kafka using `wget` and extracts it to the `/opt` directory. We then rename the extracted directory to `kafka`.

4. `WORKDIR`: Sets the working directory to the Kafka home directory.

5. `COPY`: Copies the Kafka server properties file (you need to provide this file separately, as it contains the Kafka server configuration) into the Docker image.

6. `EXPOSE`: Exposes port 9092, which is the default port used by Kafka for client connections.

7. `CMD`: Specifies the command to run when the container starts. Here, we start the Kafka server using the provided server properties file.

To build a Docker image using this Dockerfile, save the above code in a file named `Dockerfile`, and place your Kafka `server.properties` file in the same directory. Then, run the following command in the terminal:

```
docker build -t kafka:latest .
```

After the image is built, you can run a Kafka container using the following command:

```
docker run -d -p 9092:9092 --name kafka kafka:latest
```

This will start a Kafka container named `kafka` in detached mode (-d) and expose port 9092 on the host machine, allowing external clients to connect to Kafka.