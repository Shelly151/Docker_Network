# **Networking Using Docker**  

Docker Networking allows you to create a network of Docker containers managed by a master node called the **manager**. Containers inside the Docker network can communicate by sharing packets of information.  

This guide covers essential **Docker Networking** commands to help you get started.

---

## **Table of Contents**
- [Types of Network Drivers](#types-of-network-drivers)
- [Installation & Prerequisites](#installation--prerequisites)
- [Understanding Docker Network Commands](#understanding-docker-network-commands)
- [Running Containers on a Docker Network](#running-containers-on-a-docker-network)
- [Networking Utilities](#networking-utilities)
- [Resources](#resources)
- [Contributing](#contributing)

---

## **Types of Network Drivers**  

1. **Bridge**  
   - The default network if no driver is specified.  
   - Containers can communicate with each other but are isolated from the host system.  

2. **Host**  
   - Removes network isolation between the container and the host machine.  
   - The container will use the host’s IP instead of its own.  

3. **None**  
   - No network is assigned to the container.  
   - The container is completely isolated.  

4. **Overlay**  
   - Enables networking across multiple Docker daemons.  
   - Used in **Docker Swarm** to allow different services to communicate.  

5. **Ipvlan**  
   - Provides complete control over both IPv4 and IPv6 addressing.  

6. **Macvlan**  
   - Allows containers to have their own **MAC addresses**, making them appear as physical devices on the network.  

---

## **Installation & Prerequisites**  

Ensure Docker is installed on your system and that you are signed into **Docker Hub** and **Docker Desktop**.  

### **Verify Docker Installation**
```sh
docker network ls
```

---

## **Understanding Docker Network Commands**  

### **1. Create a Docker Network**  
Creates a bridge network with a custom subnet and IP range.  
```sh
docker network create --driver bridge --subnet 172.20.0.0/16 --ip-range 172.20.240.0/20 net-bridge
```

### **2. Connect a Container to a Network**  
```sh
sudo docker network connect <network-name> <container-name or ID>
```

### **3. Inspect a Network**  
```sh
sudo docker network inspect <network-name>
```

---

## **Running Containers on a Docker Network**  

### **1. Run a Redis Container**
```sh
docker run -itd --net=net-bridge --name=cont_database redis
```

### **2. Retrieve Container’s IP Address**
```sh
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' cont_database2
```

### **3. Run a BusyBox Container**
```sh
docker run -itd --net=net-bridge --name=server-A busybox
```

### **4. Inspect Network Containers in JSON Format**
```sh
docker inspect --format='{{json .Containers}}' net-bridge | python -m json.tool
```

### **5. Inspect Network Settings of a Container**
```sh
docker inspect --format='{{json .NetworkSettings}}' server-B | python -m json.tool
```

### **6. Access a Running Container**
```sh
docker container exec -it <CONTAINER_ID> bash
```

---

## **Networking Utilities**  

### **1. Update Packages**
```sh
apt-get update
```

### **2. Install Ping Utility**
```sh
apt-get install iputils-ping
```

### **3. Test Network Connectivity**
```sh
ping <container-IP>
```

---

## **Resources**  

- [Docker Documentation](https://docs.docker.com/)  
- [Docker Networking Guide](https://docs.docker.com/network/)  

---

## **Contributing**  
Feel free to contribute by enhancing this README!  

**Thank you!** 🚀
