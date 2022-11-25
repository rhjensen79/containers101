What is a Dockerfile ? Docker.com describes it like this "A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image"
So it's a file, with the name `Dockerfile` that contains the steps, on how to build the container. 

Sounds simple right ? Well that's because it is. 

Below is a sample of how a simple Dockerfile could look.

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

## Build

Now that we understand the Dockerfile, let's try to build a conainer from it. 

Take the content of the dockerfile, and save it into a file called `Dockerfile` in the root directory.

To build it, we need to run the command 

```bash
docker build -t container:1 .
```

Note the `.` in the end. It's important, and means that docker should look for a Dockerfile in the current directory, so don't forget it.
The `-t` is to give the container a tag, so we can request it.
A tag consist of a name:version 
You can use `latest` to get the lastest version, but it's considered best practice, to always describe the version, so you are sure what you are getting, and you are able to revert to an earlier version, if that is needed.
For now, our version is 1

After a bit of time, you should see output, that looks something like this.

```bash
=> exporting to image                                   1.4s
=> => exporting layers                                  1.3s
=> => writing image sha256:feb72bf5b3f05eace0f62414347  0.0s
=> => naming to docker.io/library/container:1           0.0s
```

This means that you have now created a container, with the name container:1 on your local system.

To run it, you simply you simply run 

```bash
docker run container:1
```

The container starts the Nginx process, and halts there, waiting for inputs.
You can, stop it, using `ctrl + c`

Some containers are build to keep running, like this webserver, and others are just running some commands, and exits after. Both is valid usecases.