## Docker Desktop — Kali — Web GUI

```jsx
docker run -d --name=kali-linux --security-opt seccomp=unconfined -e PUID=1000 -e PGID=1000 -e TZ=Etc/UTC -e SUBFOLDER=/ -e TITLE="Kali Linux" -p 3010:3000 -p 3009:3001 --device /dev/dri:/dev/dri --shm-size="1gb" --restart unless-stopped lscr.io/linuxserver/kali-linux:latest 
```

I recently watched this [YouTube video](https://www.youtube.com/watch?v=RUqGlWr5LBA&t=1199s), which inspired me to set up Kali in a WSL Docker environment. My Surface Pro 7+ had issues running VMware smoothly (I’ll troubleshoot that later), so I looked into alternatives. Thanks to YouTube’s algorithm and Network Chuck, I discovered I could run Kali in Docker via WSL—much more efficient!


This article will not explain docker's capability. This will be purely focused on how to setup docker Kali. 

### 1. Installing WSL

First, make sure WSL is installed by following Microsoft’s [WSL installation guide](https://learn.microsoft.com/en-us/windows/wsl/install). To install, run:

```bash
wsl --list --online
wsl --install -d Debian
```
![](https://i.imgur.com/1p5JFaO.png)

![](https://i.imgur.com/eEN3BWt.png)


Then, ensure it’s set to WSL 2 with:

```bash
wsl --set-default-version 2
```

Now, you can install your preferred Linux distribution (e.g., Kali, Ubuntu, Debian).  I have not tried Debian distro, so I installed Debian. This will be a fun journey. 


In order to manage Docker efficiently, you’ll also need Docker Desktop, which you can download [here](https://www.docker.com/products/docker-desktop). 

![](https://i.imgur.com/w6MyiQG.png)


> **Tip:** WSL allows you to use Linux on Windows seamlessly, and Docker Desktop lets you manage Docker containers easily from your desktop.



### 2. Installing Docker in Debian
The next goal is installing Docker in Debian. 
The official Docker website already has an instruction, hence no reason to repeat twice.
https://docs.docker.com/engine/install/debian/

For convenience, here are commands. 
```bash

 for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done


# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update


sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world

```


At the end, you want to see `Hello from Docker!`
![](https://i.imgur.com/W1v0PxL.png)


We can see the `Hello from Docker` container on Docker Desktop. 
![](https://i.imgur.com/H92CeX6.png)


### 3. Setting Up Kali in Docker

After installing WSL and Docker Desktop, it’s time to set up Kali! You can use the following command (inspired by Network Chuck's video) to start a Kali container from WSL!

![](https://i.imgur.com/IomixRt.png)


```jsx
docker run -d --name=kali-linux --security-opt seccomp=unconfined -e PUID=1000 -e PGID=1000 -e TZ=Etc/UTC -e SUBFOLDER=/ -e TITLE="Kali Linux" -p 3010:3000 -p 3009:3001 --device /dev/dri:/dev/dri --shm-size="1gb" --restart unless-stopped lscr.io/linuxserver/kali-linux:latest --cap-add=NET_ADMIN --cap-add=SYS_ADMIN
```

### 4. Breakdown of the Docker Command

Here’s a brief explanation of some parameters in the command:

1. **--name**: Sets the name of the container.
2. **--security-opt seccomp=unconfined**: Disables certain security restrictions, allowing broader functionality within the container.
3. **PUID/PGID**: Sets the user and group IDs for permissions.
4. **TZ**: Sets the time zone to UTC.
5. **-p**: Maps ports, allowing access to the web service (running on port 3000 inside the container) through port 3010.


This is kinda confusing. The most important thing is that you can access the Kali Container via webpage or command line. 


### 5. Checking the Kali Container’s IP Address

To check the IP address of your Kali container, you can either:

- Use Docker Desktop’s GUI, where the IP is displayed.
- Run this command in PowerShell:

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' kali-linux
```

### 6. Running and Accessing the Kali Container

Ensure Docker is running by checking active containers:
![](https://i.imgur.com/I8XFxQJ.png)


```bash
docker ps
```

To access the Kali container’s terminal, use:

```bash
docker exec -it kali-linux /bin/bash
```


![](https://i.imgur.com/KXOLQYG.png)



Alternatively, access the web GUI at [http://localhost:3010](http://localhost:3010). From within the Kali container, open the GUI with:

```bash
firefox http://localhost:3010
```
![](https://i.imgur.com/ngqcTsb.png)



### Extra : Let's run Obsidian 
```
docker run -d --name=obsidian --security-opt seccomp=unconfined -e PUID=1000 -e PGID=1000 -e TZ=Etc/UTC -p 3020:3000  -p 3025:3001 -v /home/tester/Docker/Obsidian/config:/config --device /dev/dri:/dev/dri --shm-size="1gb"  --restart unless-stopped  lscr.io/linuxserver/obsidian:latest

```

### Extra: Let's run Firefox
```
docker run -d --name=firefox --security-opt seccomp=unconfined -e PUID=1000 -e PGID=1000 -e TZ=Etc/UTC -e FIREFOX_CLI=https://www.linuxserver.io/ -p 3030
:3000 -p 3035:3001 -v /home/tester/Docker/Firefox/config:/config --shm-size="1gb" --restart unless-stopped lscr.io/linuxserver/firefox:latest 
```