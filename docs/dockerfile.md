What is a Dockerfile ? Docker.com describes it like this "A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image"

Sounds simple right ? Well that's because it is. 

Below is a sample of how a Dockerfile could look like :

```yaml
FROM nginx:latest
WORKDIR usr/share/nginx/html
RUN apt-get update && apt-get upgrade -y
RUN echo "test"
COPY ./html /usr/share/nginx/html
EXPOSE 80
```

Let's look at it, line for line.

```yaml
FROM nginx:latest
```
Sets the source container, that we are building upon, to the latest Nginx container, from DockerHub.

```yaml
WORKDIR usr/share/nginx/html
```
Sets the working directory, inside the container, where all commands will be run from.

```yaml
RUN apt-get update && apt-get upgrade -y
```
Runs a simple update and upgrade, of all packages inside the container. The cammand reqires the container os, to be able to use apt as packagemanager. 

```yaml
RUN echo "test"
```
Runs another simple command. 

```yaml
COPY ./html /usr/share/nginx/html
```
Copys the files, from the source operating system, to the container.

```yaml
EXPOSE 80
```
Let's the admin know, that this container responds to port 80. Note it's only for information.