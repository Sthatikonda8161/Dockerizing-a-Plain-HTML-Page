# Dockerizing-a-Plain-HTML-Page

##
This Project aims to familiarize yourself with Docker and containerization by Dockerizing a simple HTML page using Nginx as the web server.

Install Docker on Ubuntu machine
```
sudo apt install docker.io -y
```
```
systemctl status docker
```



  ![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/092dbdf5-ea23-4f71-ab46-2ac115700221)

1. Basic HTML Page:

   - Create a plain HTML page named `index.html` with some content (e.g., "Hello, Docker!").
```  
<!DOCTYPE html>
<html>
<head>
    <title>Hello, Docker!</title>
</head>
<body>
    <h1>Hello, Docker!</h1>
    <p>This is a plain HTML page served by Nginx in a Docker container.</p>
</body>
</html>
```

2. Nginx Configuration:

   - Create an Nginx configuration file named `nginx.conf` that serves the `index.html` page.

   - Configure Nginx to listen on port 80.
```
events {}
http {
    server {
        listen 80;
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}

```





3. Dockerfile:

   - Create a `Dockerfile` to define the Docker image.

   - Use an official Nginx base image.

   - Copy the `index.html` and `nginx.conf` files into the appropriate location in the container.

   - Ensure that the Nginx server is started when the container is run.

```
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
COPY nginx.conf /etc/nginx/nginx.conf
```

![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/8bfc0848-7660-4120-8cd4-535fb1c70824)




4. Building the Docker Image:

   - Follow the below steps to build and run a docker image.
     


```
sudo docker build -t webserver:latest .

```
![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/1eba9fd5-5137-429b-8c26-8f9b10ebc5a2)


```
sudo docker images
```
![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/97c38849-9a31-4fe1-ac8e-f060eaf18e87)
```
sudo docker run -it -d -p 8080:80 webserver:latest
```
```
sudo docker ps
```
![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/f99e75ad-e7f1-41a1-8673-16f373e06787)


5. Hit the public IP of the EC2 instance along with port:80

![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/33d12bb6-3b76-4893-a70e-33415bf269de)

 6. Push the Image on ECR

   - Make the public repository to push Image on the ECR
   - Install AWS CLI

```
AWS Access Key ID:
AWS secret access key:
Default region name: ap-south-1
Default output format:
```
  - After configuring your AWS account with in the Ec2.
    
7. Push the Image we created to the ECR(Elastic Container Registry) using the push commands.
![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/e5e4505a-ac12-4627-9538-9d6445340c1d)

![image](https://github.com/Sthatikonda8161/Dockerizing_webserver/assets/136583514/74586157-4230-4e9e-a97c-13d14623604e)


Done.
