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

## Docker

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
This is sort "unzipping" of the container - all the contents will be released and downloaded to your machine.

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

### Change state of the container

`docker stop "container_id"`
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


## Running Node App Using Docker


```
cd /usr/share/nginx/html
```

docker run -d -p 3000:3000 ahskhan/sparta-app-dockerised:v1




