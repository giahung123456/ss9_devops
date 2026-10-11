# Báo Cáo Kiểm Tra Cài Đặt Docker Engine - Bài 1

## 1. Kết quả kiểm tra phiên bản (docker version)
```text
Client: Docker Engine - Community
 Version:           27.x.x
 API version:       1.47
 Go version:        go1.22.x
 Git commit:        ...
 Built:             ...
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          27.x.x
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.x
  Git commit:       ...
  Built:            ...
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.7.x
 runc:
  Version:          1.1.x
 docker-init:
  Version:          0.19.0
```

## 2. Thông tin hệ thống Docker (docker info)
```text
Client: Docker Engine - Community
 Version:    27.x.x
 Context:    default
 Debug Mode: false

Server:
 Containers: 1
  Running: 0
  Paused: 0
  Stopped: 1
 Images: 1
 Server Version: 27.x.x
 Storage Driver: overlay2
  Backing Filesystem: extfs
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Operating System: Ubuntu ...
 OSType: linux
 Architecture: x86_64
 CPUs: 12
 Total Memory: ...
 Docker Root Dir: /var/lib/docker
 Live Restore Enabled: false
```

## 3. Khởi chạy Container Hello-World (docker run hello-world)
```text
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:535ced295843a89047713437cdcb9f19ef476a6cf9c8942b0ce80a823ee9b4be
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 [https://hub.docker.com/](https://hub.docker.com/)

For more examples and ideas, visit:
 [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)
```