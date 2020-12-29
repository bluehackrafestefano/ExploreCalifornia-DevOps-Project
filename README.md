- Use CF template (N. Virginia) and spin up an EC2 instance which Docker is already installed, SSH and HTTP ports are open.

- Check if docker is active and running:

```bash
systemctl status docker
```

- Copy webpage content from on-prem to EC2 instance, under /webpage directory in out instance:

```bash
scp -i "pemname.pem" -r ./website ec2-user@ec2-18-212-68-212.compute-1.amazonaws.com:/home/ec2-user
```

#To move all files and folders to an upper folder in linux:

```bash
mv  -v ./* ../
```

- Create an nginx containter and bind mount newly created folder:

```bash
docker run -d --name explore-california -p 80:80 -v /home/ec2-user/webpage:/usr/share/nginx/html nginx
```

- This is manual (imperative) deployment of the webpage. Let's do it with declerative approach.

- Prepare Dockerfile
    * vim Dockerfile
    * To find out the image we need to write to FROM section; go to https://hub.docker.com/
    * Search an image which can run nginx, bcoz we need nginx to run our website.
    * See "Official build of Nginx."
    * Click that image and check that out
    * See all the supported images we can use on "Supported tags and respective Dockerfile links"
    * See "alpine" is enough for us, we use Amazon Linux
    * FROM nginx:alpine --> We use alpine image and nginx on top of it
    * MAINTAINER Rafe Stefano <email>  # This is optional
    * Copy the content of the website to the image: COPY webpage /webpage
    * Copy nginx config for prod: COPY nginx.conf /etc/nginx.conf
    * Look at the image documentation, how to use it! "How to use this image"
    * What port should be exposed: EXPOSE 80
    * :wq
    * Use Dockerfile Documentation for further querries: https://docs.docker.com/engine/reference/builder/

- Build the image:
    * For detailed info: docker build --help
    * docker build --tag website .

- Run the image:
    * docker run --publish 80:80 website