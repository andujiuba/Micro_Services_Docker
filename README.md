# Micro-Services

- Web application in container
- Isolated --> more secure and uses up less resources
- Lightweight and user friendly
- Scalable

![image](https://user-images.githubusercontent.com/88186581/134932707-feeb9f85-0f48-41e3-bad9-ad4033391085.png)

Each microservice works independant to each other

![image](https://user-images.githubusercontent.com/88186581/134933334-fd80d3dd-0795-41fa-8ddb-0800565fc7b4.png)
![image](https://user-images.githubusercontent.com/88186581/134933388-ba3c4971-e4df-4044-8e84-4d15a7ee1b1d.png)

Ideal use for monolithicarchitecture: smaller systems and light-weight applications, smal businesses or local school websites
 
People w bigger scalable interfaces are using micro-services and containerisation platforms, such as Docker

---

### Hardware

RAM
CPU
Motherboard

### Software

![image](https://user-images.githubusercontent.com/88186581/134934358-a9ff81f0-4164-4c95-88b5-96ee6218517f.png)

need to scale up hardware to support software

### Virualisation

![image](https://user-images.githubusercontent.com/88186581/134934491-dcab706b-3b36-4bd1-943d-578e8d7084e7.png)4

servers have evolved
scale out and in
virtaulisation w 3 VM in vagrant slows down laptop speed and takes 50% of resources

---

# Docker

## In the map of automation (LINK), Docker container will host the static website. EC2 will push the public IP. Jenkins pushes manual changes to DockerHub then pulls from DockerHub to the EC2 instance.

- shares resources, makes it lightweight
- has its own network

![image](https://user-images.githubusercontent.com/88186581/134934927-649a0df2-6ce9-446c-9833-9ebbde5232cb.png)

### Containerisation

### Architecture

### VMs vs Docker

layers in OS:

![image](https://user-images.githubusercontent.com/88186581/134935553-e4c5d225-42e8-453f-8ffb-382be8e3b81f.png)

- layers slow down system
- top 2 ayers in Docker not used

![image](https://user-images.githubusercontent.com/88186581/134935772-3c67cd1a-318f-4206-98af-66e74dbf6f5d.png)

![image](https://user-images.githubusercontent.com/88186581/134936141-08d9f0f1-7067-4f9e-a299-8644dd2cb15f.png)

### Docker is Trending

![image](https://user-images.githubusercontent.com/88186581/134936478-3f0ad583-ba91-40a7-9ba8-86e8c53f739c.png)

## Installation

https://docs.docker.com/desktop/windows/install/

```bash
docker
docker version
```
If everything is correctly installed, then this should be what you see:

![image](https://user-images.githubusercontent.com/88186581/135101175-93bbd1c0-754f-4067-acd6-09b12db35cfd.png)

## Commands

`docker pull "image_name"`

`docker run "image_name"`

`docker push "image_name"`

### Naming convention for images

`"acount_name"/"image_name": tag`

### See all running images

`docker images`

![image](https://user-images.githubusercontent.com/88186581/135104643-84955f26-5085-49ea-9146-3b3bd00008ee.png)

### Remove image
`docker rmi -f "image_name"`

### Creating containers

```
docker run -d -p "container_id":"container_id" "name"
```
This is sort "unzipping" of the container - all the contents will be released and downloaded to your machine. <br>
The `ID:ID` section is the **port mapping**, showing the path from the first port to the second port.

We will practice using the `Ghost` container:

```
docker run -d -p 2368:2368 ghost
```

### Show container

`docker ps`
`docker ps -a`

<br>
<details>
<summary>For `Ghost`, this is the resulting output:</summary>
<br>
 
```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                       NAMES
a807d8be43d9   ghost     "docker-entrypoint.s…"   19 seconds ago   Up 14 seconds   0.0.0.0:2368->2368/tcp, :::2368->2368/tcp   wonderful_visvesvaraya
```
</details>

### View image

Go to `localhost:"container_id"` in web browser

<details>
<summary>In our case, we will search for `localhost:2368`</summary>
<br>
 
![image](https://user-images.githubusercontent.com/88186581/135109378-cc9b49a4-f6f8-4596-a1dc-d966ed26d79b.png)
</details>

### Checking state of the container

```
docker logs "container_id"
```

### Change state of the container

```
docker stop "container_id"
```
`-stop`, `-start`, `-rm`

*STOP* - still holds same data available <br>
*REMOVE* - deletes it completely

### Interacting with a running container

```
alias docker="winpty docker"
docker exec -it "container_id" sh
```

Now you are inside the container where all the code is located

```docker
# apt-get update
# apt-get nano install
```
To leave the container, just enter

```docker
exit
```

### Delete all containers

```
docker rm -f $(docker ps -a -q)
```

## Documentation

To access documentation for Docker, then run in the terminal:
```
docker run -d -p 4000:4000 docs/docker.github.io
```

And search in the browser: `localhost:4000`

![image](https://user-images.githubusercontent.com/88186581/135111967-9f95b034-40b2-4571-8dba-5bf3f769767d.png)


## Running NGINX

We need to download the `nginx` image using `docker run`. We know NGINX runs on **port 80** so we use the port mapping code `80:80`. This should be what you see if you `docker ps`
```
CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS          PORTS                                               NAMES
08f7a31ada06   nginx                   "/docker-entrypoint.…"   50 seconds ago   Up 29 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp                   kind_keller
```
We then `ssh` into the machine using `docker exec`. We find the `index.html` file that represents the main page of the app. You can change the index.html file to change the appearance of the page.
<br>
<details>
<summary>Here is the complete code:</summary>
<br>
 
 ```
 docker run -d -p 80:80 nginx
 docker exec -it "container_id" sh
 ```
 If there are errors running the second line of code, then the *alias* hasn't been set. Run `alias docker="winpty docker"`.
 Once inside the container:
 ```docker
 # apt-get update
 # apt-get nano install
 # cd /usr/share/nginx/html
 # nano index.html
 ```
</details>

If `docker stop "container_id"` is run then the container is started again, the last version of the image will still be there. However, if the container is removed and rerun, then the image resets itself to its original state.

### Running a containerised version of the node app

If port 80 is already allocated, you have to remove the container that is occupying it.
```
docker run -d -p 80:3000 ahskhan/sparta-app-dockerised:v1
docker logs "container_id"
```
If you don't want to change port 80, then code instead:
```
docker run -d -p 3000:3000 ahskhan/sparta-app-dockerised:v1
```
If the container was set up successfully, you should see (when you run `docker logs`)

![image](https://user-images.githubusercontent.com/88186581/135217787-df335a62-560a-4aa8-9570-c7f987c83a4a.png)

Go to `localhost` and you should see the page:

![image](https://user-images.githubusercontent.com/88186581/135218713-9e4e080a-99f1-4476-941f-948579bfd6f9.png)

---

**TASKS:**
- Create a container with NGINX image --> globally available
- Create an index.html file on localhost
- Copy the index.html file to default location inside of NGINX container /usr/share/nginx/html
- Commit the changes to the images
- Build you own images called "account_id"/sre_customised_nginx
- docker run -d -p "your_image_name"

<br>
<details>
<summary> *SudoCode* </summary>
<br>
 
```bash
# Choose the image you want to build from 

# Create a container

# Make changes to index.html -- copy from host machine to container  

# Portmap the container -- port 80

# CMB to launch the NGINX web server
```
</details>

<br>
<details>
<summary> ### 1. Create a `Dockerfile` </summary>
<br>

 ```bash
 # BUILDING OUR OWN IMAGE
 # Choose the image you want to build from

 FROM nginx

 LABEL MAINTAINER=andujiuba@spartaglobal.com
 # OPTIONAL -- tells who the author is

 # Make changes to index.html -- copy from host machine to container

 COPY index.html /usr/share/nginx/html/index.html

 # Portmap the container -- port 80

 EXPOSE 80

 # CMB to launch the NGINX web server

 CMD ["nginx", "-g", "daemon off;" ]
 # makes NGINX global
 ```
 
 CMD is always the **last command**
</details>

### 2. Build the image

```
docker build -t akunduj/sre_customised_nginx:v1 .
```
![image](https://user-images.githubusercontent.com/88186581/135223134-ae5c366a-4675-4382-88dc-42fffc0a165a.png)

Image should be there when `docker images` is run

### 3. Run the container

```
docker run -d -p 80:80 akunduj/sre_customised_nginx:v1
```
![image](https://user-images.githubusercontent.com/88186581/135223399-7857e1ac-be1c-4779-bcac-ca4f4d4b6e70.png)

### 4. Push to DockerHub

```
docker login
docker push "image_name":"tag"
```

![image](https://user-images.githubusercontent.com/88186581/135225057-2d4f015b-393c-4930-90d5-164a6e458aed.png)

![image](https://user-images.githubusercontent.com/88186581/135225245-bb696ae3-fdfd-4632-a6cb-8cf7d56fbfea.png)
