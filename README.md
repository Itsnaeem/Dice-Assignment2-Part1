# Dice-Assignment2-Part1
This part will test the understanding of Docker networking and how to use it to connect Docker containers.

● Create a new Docker network named "my_network" using the bridge driver

```bash
docker network create my_network
```

● Create a new Docker container using the "nginx" image and connect it to the "my_network" network. Name the container "nginx_container"

```bash
docker pull nginx
```

docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
2f44b7a888fa: Pull complete 
8b7dd3ed1dc3: Pull complete 
35497dd96569: Pull complete 
36664b6ce66b: Pull complete 
2d455521f76c: Pull complete 
dc9c4fdb83d6: Pull complete 
8056d2bcf3b6: Pull complete 
Digest: sha256:4c0fdaa8b6341bfdeca5f18f7837462c80cff90527ee35ef185571e1c327beac
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview nginx



● Verify that the "nginx" default page is accessible on your host machine at http://localhost:8080.


```bash
docker run --name nginx --network my_network -p 8080:80 -d nginx
```

20d7a14d324bdc25c27c346f763c08d73ecbb3e423c1a2fe76dd7208c13e0f6f

Yes the default nginx page with this url is working "http://localhost:8080/"

● Create a new Docker container using the "httpd" image and connect it to the
"my_network" network. Name the container "httpd_container". (4 marks)
● Verify that the "httpd" default page is accessible on your host machine at
http://localhost:8081.

```bash
docker pull httpd
```
Using default tag: latest
latest: Pulling from library/httpd
2f44b7a888fa: Already exists 
5abb3599da34: Pull complete 
4f4fb700ef54: Pull complete 
fa608a886227: Pull complete 
afe6bbf00437: Pull complete 
fd0ef2a49677: Pull complete 
Digest: sha256:7765977cf2063fec486b63ddea574faf8fbed285f2b17020fa7ef70a4926cdec
Status: Downloaded newer image for httpd:latest
docker.io/library/httpd:latest

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview httpd

```bash
docker run --name httpd --network my_network -p 8081:80 -d httpd
```

docker run --name httpd --network my_network -p 8081:80 -d httpd
Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
2f44b7a888fa: Already exists 
5abb3599da34: Pull complete 
4f4fb700ef54: Pull complete 
fa608a886227: Pull complete 
afe6bbf00437: Pull complete 
fd0ef2a49677: Pull complete 
Digest: sha256:7765977cf2063fec486b63ddea574faf8fbed285f2b17020fa7ef70a4926cdec
Status: Downloaded newer image for httpd:latest
000e525e0d32c8a9321d569b81f1940144121b94eb5c173325d2275799f32681

Yes the default httpd page with this url is working "http://localhost:8081/"


● Use the "docker network inspect" command to display information about the
"my_network" network. Document your findings in the README.md file. 

```bash
docker network inspect my_network
```
[
    {
        "Name": "my_network",
        "Id": "e0c0e676a19e1983b20d8daeee08059a3f417e4ed41a1c90616e796cb1d10b7e",
        "Created": "2024-01-22T06:22:46.656265044Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "000e525e0d32c8a9321d569b81f1940144121b94eb5c173325d2275799f32681": {
                "Name": "httpd",
                "EndpointID": "d31b2efa60d2b61dbae662448cd1c144f65f357ae77b0dffe8f084ad0099d429",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "b5d700da833e8aeb767dd1dd8d72608528d5644ea91f7e3563f86d5121c60b41": {
                "Name": "nginx",
                "EndpointID": "c32038585e4b3e70656ee243bf40b09a8128cefb096b4b73505be709725778c1",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]


● Stop and remove the "nginx_container" container.

First 
```bash
docker ps
```
Output is:

docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                  NAMES
000e525e0d32   httpd     "httpd-foreground"       7 minutes ago   Up 7 minutes   0.0.0.0:8081->80/tcp   httpd
b5d700da833e   nginx     "/docker-entrypoint.…"   9 minutes ago   Up 9 minutes   0.0.0.0:8080->80/tcp   nginx

```bash
docker stop b5d700da833e
```
b5d700da833e

```bash
docker rm nginx
```

nginx

● Create a new Docker container using the "nginx" image and connect it to the "my_network" network. Name the container "nginx_container_2"

I create the new container of nginx with tag name and new port. using below command

```bash
docker run --name nginx_container_2 --network my_network -p 8082:80 -d nginx
```
acea36204011ccff33eb37f06f2f25aabd23479190b2a2e85caa625c34c34a77


● Verify that the "nginx" default page is accessible on your host machine at http://localhost:8082.

Yes this url is working & default nginx pas is showing.

● Use the "docker container ls" command to display information about all running
containers. Document your findings in the README.md file.

```bash
docker container ls
```

the output is below:

CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                  NAMES
acea36204011   nginx     "/docker-entrypoint.…"   2 minutes ago    Up 2 minutes    0.0.0.0:8082->80/tcp   nginx_container_2
000e525e0d32   httpd     "httpd-foreground"       13 minutes ago   Up 13 minutes   0.0.0.0:8081->80/tcp   httpd

● Stop and remove all containers

```bash
docker ps -a -q
```
acea36204011
000e525e0d32

to stop all the container using below command.

```bash
docker stop $(docker ps -a -q)
```
acea36204011
000e525e0d32


to remove all the container using below command.

```bash
docker rm $(docker ps -a -q)
```
acea36204011
000e525e0d32

● Cleanup: Remove the "my_network" network.

Remove network using below command.

```bash
docker network rm my_network 
```

my_network


● Create a README.md file and document your findings for each command. For each command, provide a brief description of what it does, followed by the output and logs generated by the command. Ensure that the README.md file is well-organized, easy to read, and contains all necessary information. 

In this Docker Assignment I create a repo on git hub account and write all the outputs of commands with step by step.


● Push the codebase for the sample application to your GitHub repository (create a new one for this part)

I create the repo on github account with name of `Dice-Assignment2-Part1` its a public repo.



