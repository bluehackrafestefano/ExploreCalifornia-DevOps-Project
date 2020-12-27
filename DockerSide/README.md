1. Use CF template and spin up an EC2 instance which Docker is being installed.
2. Test it with: docker run hello-world
3. Prepare Dockerfile
    * vim Dockerfile
    * To find out the image we need to write to FROM section; go to https://hub.docker.com/
    * Search an image which can run nginx, bcoz we need nginx to run our website.
    * See "Official build of Nginx."
    * Click that image and check that out
    * See all the supported images we can use on "Supported tags and respective Dockerfile links"
    * See "alpine" is enough for us, we use Amazon Linux
    * FROM nginx:alpine --> We use alpine image and nginx on top of it
    * MAINTAINER Rafe Stefano <email>
    * Copy the content of the website to the image: COPY website /website
    * Copy nginx config for prod: COPY nginx.conf /etc/nginx.conf
    * Look at the image documentation, how to use it! "How to use this image"
    * What port should be exposed: EXPOSE 80
    * :wq
    * Use Dockerfile Documentation for further querries: https://docs.docker.com/engine/reference/builder/
4. Run the image:
    * For detailed info: docker build --help
    * docker build --tag website .