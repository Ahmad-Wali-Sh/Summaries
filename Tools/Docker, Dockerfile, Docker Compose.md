#### Getting Started With Docker
`Summary: Ahmad Wali Sharify`

### Intro to Containers

Docker Fixed differences between local and production environment by standardizing the way we package and run apps.

`Standard Package: Image`
`Standard Way to Run Image: Container`

Packaging and Creating an image from existing application is called *containerizing*. it takes **source code**, and all **dependencies** and make it an `image`. then you can run it as a `container (isolated execution environment)`

> Steps: 
> 	1. Develop your app
> 	2. build the app and dependencies an image (Dockerfile)
> 	3. Ship the image to a registry (Docker Hub) (optional)
> 	4. Run it as a container

### Image

an image is a collection of layers that comprise the application and all dependencies.

building it using `Dockerfile` and `docker build`

*If you’re a developer, think of images and containers as similar to classes
and objects — we create containers from images in a similar way to
creating objects from classes.*

### Registries

Container registries are centralized places to store and retrieve images.
Sometimes we call them container registries, Docker registries, or OCI
registries. Like Docker Hub.

### The Open Container Initiative

The Open Container Initiative (OCI) is a governance body responsible
for developing and maintaining the core standards that have enabled the
container ecosystem to thrive.
It currently maintains three specifications:
• Image spec
• Runtime spec
• Distribution spec

### Monolithic vs Microservice Applications

`Monolithic`: application where every feature is developed, deployed, and managed as
a single complex app

`Microservices`: is a modern design pattern where every application feature
is developed, deployed, and managed as its own small independent
application

---

### Getting Docker
You Can use Docker Desktop or multipass

### Containerizing an Application

`docker init` is a relatively new command. It reads an existing application and produces a high quality Dockerfile that docker build can use to containerize the app. (for Docker Desktop)

`example for a Node js Application`

```dockerfile
ARG NODE_VERSION=20.8.0
FROM node:${NODE_VERSION}-alpine
ENV NODE_ENV production
WORKDIR /usr/src/app
RUN --mount=type=bind,source=package.json,target=package.json \
--mount=type=bind,source=package-lock.json,target=pack... \
--mount=type=cache,target=/root/.npm \
npm ci --omit=dev
USER node
COPY . .
EXPOSE 8080
CMD node app.js
```

`ARG` defines Variable in Dockerfile
`FROM` is for base layer of the new image
`ENV` is production mode
`WORKDIR` instruction to set the working directory for the rest of the instructions in the file.
`RUN` is for creating the image
`USER` as Node User
`COPY` will Copy all Files (ignore the `.dockerignore` file)
`EXPOSE` instruction documents the application’s network port
`CMD` instruction tells Docker which app the container should run

and then:
`docker build -t node-app .`

### Running Containers:

`docker ps` list all running containers.
`docker images` list all local images.

ex: `docker run -d --name test -p 5555:8080 nigelpoulton/gsd-book`

`docker run` is for running an image.
`-d` flag is for running it in the background (detach from terminal)
`-p` maps port 5555 to 8080
`docker stop test` to stop
`docker start test` to restart
`docker rm test -f` to delete

### Images and Registries

Registries are where you securely store container images. Lots of registries exist, and most comply with the OCI distribution-spec. 

To push to a registry, you need the information of account, repository in the name of the image to push it.

`docker tag node-app ahmadwalisharify/images`

and then: 
`docker push ahmadwalisharify/images`

`docker.io/ahmadwalisharify/image:latest`
first is registry, then account, then repo, and tag

### Multi-Architecture images

`docker build --platform` you can flag which platforms to support and build the image.

### Multi-container apps with Compose

most real-world apps are a lot more complicated and consist of many different containers.
we use docker compose for multi-containers.

you define a compose file (`compose.yaml`) and then add services to it (images).

```yaml
network:
	internal:
services:
	web: 
		build: .
		command: python app.py
		ports: 
		 - target: 8080
		   published: 5555
		networks:
		 - internal
	store:
		image: "redis:alpine"
		networks:
		 - internal
```

first, we define a network called `internal`, then we start defining `services`, for `web` service, we demand building from Dockerfile in the same directory, then attach it to network, and for `store`, we use `redis` image and attach it to internal network.

`docker compose` will use out `compose.yaml` file to build a multi-container and network.
### Manage the app

The `docker compose` command lets you perform lifecycle operations
such as stopping, starting, restarting, and deleting the app.

`docker compose ls` for detailing about multi-containers.

`docker compose stop` to stop

`docker compose restart` to restart

`docker compose up --pull always --detach` to update (any change in `compose.yaml`)

`docker compose down --rmi all` to delete

----

### Dockerfile Structure

Steps:
1. Determine your base image
2. Install application dependencies
3. Copy in any relevant source code and/or binaries
4. Configure the final image

| [`ADD`](https://docs.docker.com/reference/dockerfile/#add)                          | Add local or remote files and directories.                  |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| [`ARG`](https://docs.docker.com/reference/dockerfile/#arg)                          | Use build-time variables.                                   |
| [`CMD`](https://docs.docker.com/reference/dockerfile/#cmd)                          | Specify default commands.                                   |
| [`COPY`](https://docs.docker.com/reference/dockerfile/#copy)                        | Copy files and directories.                                 |
| [`ENTRYPOINT`](https://docs.docker.com/reference/dockerfile/#entrypoint)            | Specify default executable.                                 |
| [`ENV`](https://docs.docker.com/reference/dockerfile/#env)                          | Set environment variables.                                  |
| [`EXPOSE`](https://docs.docker.com/reference/dockerfile/#expose)                    | Describe which ports your application is listening on.      |
| [`FROM`](https://docs.docker.com/reference/dockerfile/#from)                        | Create a new build stage from a base image.                 |
| [`HEALTHCHECK`](https://docs.docker.com/reference/dockerfile/#healthcheck)          | Check a container's health on startup.                      |
| [`LABEL`](https://docs.docker.com/reference/dockerfile/#label)                      | Add metadata to an image.                                   |
| [`MAINTAINER`](https://docs.docker.com/reference/dockerfile/#maintainer-deprecated) | Specify the author of an image.                             |
| [`ONBUILD`](https://docs.docker.com/reference/dockerfile/#onbuild)                  | Specify instructions for when the image is used in a build. |
| [`RUN`](https://docs.docker.com/reference/dockerfile/#run)                          | Execute build commands.                                     |
| [`SHELL`](https://docs.docker.com/reference/dockerfile/#shell)                      | Set the default shell of an image.                          |
| [`STOPSIGNAL`](https://docs.docker.com/reference/dockerfile/#stopsignal)            | Specify the system call signal for exiting a container.     |
| [`USER`](https://docs.docker.com/reference/dockerfile/#user)                        | Set user and group ID.                                      |
| [`VOLUME`](https://docs.docker.com/reference/dockerfile/#volume)                    | Create volume mounts.                                       |
| [`WORKDIR`](https://docs.docker.com/reference/dockerfile/#workdir)                  | Change working directory.                                   |

---

### `docker-compose.yaml` Structure

Starts existing containers for a service.
`docker-compose start`

Stops running containers without removing them.
`docker-compose stop`

Pauses running containers of a service.
`docker-compose pause`

Unpauses paused containers of a service.
`docker-compose unpause`

Lists containers.
`docker-compose ps`

Builds, (re)creates, starts, and attaches to containers for a service.
`docker-compose up`

Stops containers and removes containers, networks, volumes, and images created by up.
`docker-compose down`

[Cheatsheet](http://devopscycle.com/wp-content/uploads/sites/4/2024/03/the-ultimate-docker-compose-cheat-sheet.pdf)