# Containers Lab - Docker
Gained hands-on experience with Docker. Perform various tasks related to Docker containers, such as listing and pulling images, running containers, and creating custom images. 

## Task 1: Container Management
Managed Docker containers and images.
1. **List Containers**:
List the Docker containers present in environment.

Command:
```sh
sudo docker ps -a
```

Output:

```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

There are no conainers in the environment.

2. **Pull Latest Ubuntu Image**:
Pull the latest Ubuntu image from the Docker registry.

Command:
```sh
sudo docker pull ubuntu:latest
```

Output:
```
latest: Pulling from library/ubuntu
Digest: sha256:dfc10878be8d8fc9c61cbff33166cb1d1fe44391539243703c72766894fa834a
Status: Image is up to date for ubuntu:latest
docker.io/library/ubuntu:latest
```

3. **Run Container**:
Run a container using the pulled Ubuntu image.

Command:
```sh
sudo docker run -it --name ubuntu_container ubuntu:latest
```

Relevant details:
- container name: `ubuntu_container`
- `-it`: 
  - `-i`: Keeps STDIN open for interactive command input.
  - `-t`: Allocates a pseudo-TTY, providing a terminal interface within the container.
- `exit` or  `Ctrl + D` should be used to exit the interactive shell.


4. **Remove Image**:
Attempt to remove the pulled Ubuntu image.

Command:

```sh
sudo docker rmi ubuntu:latest
```

Output:

```
Error response from daemon: conflict: unable to remove repository reference "ubuntu:latest" (must force) - container afc62d4cfca5 is using its referenced image 2b1b17d5e5a2
```

Got error because the image cannot be removed while it is used by a container.



## Task 2: Image and Container Operations
Performed operations on Docker images and containers.

1. **Create Image Archive**:
Pulled the latest Ubuntu image and created an archive file from it.

Command:
```sh
sudo docker save -o ubuntu_image.tar ubuntu:latest
```

Command:
```
sudo docker images ubuntu:latest
```

Output:
```
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    2b1b17d5e5a2   4 weeks ago   101MB
```

Command:

```
ls -lh ubuntu_image.tar
```

Output:
```
-rw------- 1 root root 99M Sep 26 14:42 ubuntu_image.tar
```

The size of the archive file is roughly the same as the size of the original image indicating that the archive closely represents the image. The small difference in size may be due to disk space allocation or some metadata.

2. **Run Nginx Container**:
Runned a container using the Nginx web server image.

```sh
sudo docker run -d -p 80:80 --name nginx_container nginx
```

Output:
```
2e933d175608a630fdaa97a9bff9a59aad922ebff94cca8cdbb510ffcfbac834
```

Verified that the web server is running and accessible from the local machine by visiting http://localhost

3. **Create HTML File**:
Created an HTML file `index.html` with the specified content:

```html
<html>
<head>
<title>The best</title>
</head>
<body>
<h1>website</h1>
</body>
</html>
```

Copied the HTML file to the container at the appropriate location to serve as an index file.

Command:
```sh
sudo docker cp index.html nginx_container:/usr/share/nginx/html/index.html
```

Output:
```
Successfully copied 2.05kB to nginx_container:/usr/share/nginx/html/index.html
```

4. **Create Custom Image**:
Created a custom Docker image from the running container and named it `my_website`.

Command:
```sh
sudo docker commit nginx_container my_website:latest
```

5. **Remove Original Container**:
Removed the original container (`nginx_container`) and verified that it has been successfully removed.

```sh
sudo docker rm -f nginx_container
sudo docker ps -a
```


Output:
```
CONTAINER ID   IMAGE           COMMAND       CREATED             STATUS                         PORTS     NAMES
afc62d4cfca5   ubuntu:latest   "/bin/bash"   About an hour ago   Exited (0) About an hour ago             ubuntu_container
```

6. **Create New Container**:
Created a new container using the custom image I've created.
Command:
```sh
sudo docker run -d -p 80:80 --name my_website_container my_website:latest
```

Output:
```
5986a1a4cfa15d995f05e4bb3dd1aa359ca68ab5f8be3c5e8ad3860bf0cd4b3c
```

7. **Test Web Server**:
Used the `curl` command to access the web server at `127.0.0.1:80`.

Command:
```sh
curl http://127.0.0.1:80
```

Output:
```
<html>
<head>
<title>The best</title>
</head>
<body>
<h1>website</h1>
</body>
</html>
```

8. **Analyze Image Changes**:
Used the `docker diff` command to analyze the changes made to the new image.

Command:
```sh
sudo docker diff my_website_container
```

Output:
```
C /run
C /run/nginx.pid
C /etc
C /etc/nginx
C /etc/nginx/conf.d
C /etc/nginx/conf.d/default.conf
```
The `docker diff` command output shows that the directories and files related to Nginx configuration, such as `/etc/nginx` and `/etc/nginx/conf.d/default.conf`, have been created  (`C`) in the container, indicating that the Nginx web server has been initialized.