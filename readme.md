**Containers? So What? Docker 101 Explained - Computer Stuff They Didn't Teach You #8: https://www.youtube.com/watch?v=0oEsMwSxBsk** 

What happens if you have a machine (server) you want to deploy to? 

Originally, you'd have to manually configure that machine. As well as being tedious, nuances between machines can make this a nightmare. You might set it up perfectly on machine A, only for it to fail on machine B.

Virtual Machines are are great, but they're also resource expensive (CPU, memory).

Now we have containerisation technologies like Docker. Containers are fast and lightweight. Perfect. 

![containers-vs-virtual-machines](readme-img/containers-vs-virtual-machines.jpg)

---

**Installation**

- I'm on Windows 10
- I re-installed Ubuntu from the Microsoft App store and it updated to WSL2. I was previously running WSL1, which wasn't compatible with Docker.
- Installed https://www.docker.com/products/docker-desktop (with WSL2 option)
- I had to prepend `sudo` to commands to make things work the first time from the docker CLI. Don't know why.
- It should be possible to run this in PowerShell, but I haven't looked into that yet.

---

compile `helloworld.c` to your OS with: `gcc .\helloworld.c -static -o helloworld`

Create a `Dockerfile` and build it with: `docker build -t mytest:latest .`

![image-20201110121435997](/readme-img/image-20201110121435997.png)

Run Docker with: `docker run mytest:latest`

![image-20201110122025983](/readme-img/image-20201110122025983.png)

Use `docker build -it mytest:latest .` to have interactive prompt access (makes exiting the thing way easier too).

---

busybox is the smallest container. 

Let's try it out:

```dockerfile
#Dockerfile
FROM busybox:latest
```

build again with `docker build -t mytest:latest .`

And run:

![image-20201110123118525](/readme-img/image-20201110123118525.png)

^ This gives us a nice little sandbox where we can do stuff like creating files.

What happens if we restart the container? — `helloagain.txt` is not persisted!

---

```dockerfile
#Dockerfile
FROM busybox:latest
CMD ["echo", "Welcome to Docker"] #tell Docker to run some command within container
```

rebuild and run:

![image-20201110123524778](/readme-img/image-20201110123524778.png)

---

We can run our `helloworld` program with an ubuntu container instead of busybox:

```dockerfile
FROM ubuntu
COPY ./helloworld /helloworld
CMD ["/helloworld"]
```

![image-20201110134119943](/readme-img/image-20201110134119943.png)

---

Or we can just run ubuntu without the build step:

![image-20201110133932659](/readme-img/image-20201110133932659.png)

`--rm` = remove when done

It gets pulled down and cached for further uses. 

The caching of layers makes Docker very fast.

---

We can use https://hub.docker.com/ to find images to run on Docker

---

Trying out nginx web server:

*$ docker run --rm --name docker-nginx -p 81:80 nginx*

pulls down nginx and makes it accessible through localhost:81

![image-20201110135656511](/readme-img/image-20201110135656511.png)

---

Use `docker ps` to see which containers you have running

---

This was a quick intro to Docker. 

Go checkout some Dockerfiles to learn more!

