## CI/CD > Docker > Docker-Compose

[<- To Docker](./index.md)

#### ELI5:
Let's say you're building a cool LEGO spaceship, and it's made up of different parts like the cockpit, wings, and engines. Now, imagine Docker Compose as a magic instruction manual that helps you build your spaceship by putting all those LEGO parts together.

Here's how it works:

1. **Define Your Spaceship**: First, you write down what your spaceship should look like and what parts it needs in a special file called a "docker-compose.yml" file. You list all the different services your spaceship needs, like the cockpit, wings, and engines, and what each service requires, like which LEGO pieces to use.

2. **Get Your LEGO Pieces Ready**: Next, you gather all the LEGO pieces you need for each part of your spaceship. These pieces represent the software components your services require, like databases, web servers, or other applications.

3. **Follow the Instructions**: Then, you use Docker Compose to follow the instructions in your "docker-compose.yml" file. It reads the file and knows exactly how to assemble all the LEGO pieces together to build your spaceship. It connects all the services and sets up everything they need to work together.

4. **Launch Your Spaceship**: Finally, once Docker Compose has put everything together, your spaceship is ready to launch! All your services are up and running, connected, and working together smoothly, just like a well-built LEGO spaceship.

So, in simple terms, Docker Compose is like a magic instruction manual for building and running your software applications. It helps you define, organize, and launch all the different parts of your application with ease, making it simpler to manage complex software projects.

#### Proper Explaination
Docker Compose is a tool for defining and running multi-container Docker applications. It simplifies the process of managing complex applications composed of multiple services by allowing you to define them all in a single file and run them with a single command. Docker Compose uses a YAML configuration file to define the services, their dependencies, and various configuration options.

Here's how Docker Compose works:

1. **Define Services**: You create a `docker-compose.yml` file in your project directory to define all the services that make up your application. Each service is specified as a separate section in the YAML file and includes configuration options such as the Docker image to use, environment variables, ports to expose, volumes to mount, and dependencies on other services.

2. **Build or Pull Images**: Docker Compose can build Docker images for your services from a Dockerfile or pull pre-built images from a registry like Docker Hub. This allows you to easily use custom images or images from third-party sources.

3. **Manage Dependencies**: Docker Compose automatically handles dependencies between services. If one service depends on another, Docker Compose ensures that the dependent service is started first, allowing you to specify the order in which services should be started.

4. **Run Services**: Once you have defined your services and configured your `docker-compose.yml` file, you can use Docker Compose to start, stop, and manage your entire application with a single command. Docker Compose creates and manages Docker containers for each service, handling all the details of networking, volumes, and dependencies.

5. **Manage Lifecycle**: Docker Compose provides commands to manage the lifecycle of your application, including starting, stopping, rebuilding, and scaling services. It also supports logging and debugging features to help you monitor and troubleshoot your application.

Now, let's illustrate Docker Compose with a simple example of a web application composed of two services: a web server and a database.

Consider the following `docker-compose.yml` file:

```yaml
version: '3'

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    depends_on:
      - db

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: mydatabase
```

In this example:

- We have two services: `web` and `db`.
- The `web` service uses the `nginx:latest` image, exposes port 80, mounts a local directory `./html` into the container's `/usr/share/nginx/html` directory, and depends on the `db` service.
- The `db` service uses the `mysql:latest` image, sets environment variables for MySQL root password and database name.

To start this application, navigate to the directory containing the `docker-compose.yml` file and run:

```bash
docker-compose up
```

This command will start both services, creating Docker containers for each based on the specified images and configuration. You can access your web server at `http://localhost`, and your database will be available for use by the web service.