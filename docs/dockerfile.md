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

