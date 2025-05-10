# Nginx Using Docker on a Kali Linux VM and Accessing It from Host Machine

This guide shows how to install Docker on Kali Linux, run an Nginx container, and access the Nginx web server from your host machine using a **bridged network**.

---

## Prerequisites

- VirtualBox VM with **Kali Linux**
- Internet access inside VM
- Docker installed inside Kali
- VM network set to **Bridged Adapter**

---

## Step 1: Install Docker on Kali Linux

```bash
sudo apt update
sudo apt install docker.io -y
```
Enable and start the Docker service:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```
Verify Docker is running:

```bash
sudo systemctl status docker
```
## Step 2: Run Nginx Container
Pull and run the Nginx container:

```bash
sudo docker run -d --name mynginx -p 80:80 nginx
```
Explanation:

-d: run in detached mode

--name mynginx: name your container

-p 80:80: map VM port 80 to container port 80

## Step 3: Check Nginx Status
Check that the container is running:

```bash
sudo docker ps
```
You should see a running container with nginx image and port 80->80.

## Step 4: Access Nginx Inside the VM
Open a browser inside the Kali VM and go to:

```bash
http://localhost
```
You should see the default Nginx welcome page.

## Step 5: Get the VM IP Address
In the Kali terminal, run:

```bash
ip a
```
Look for an IP address like 192.168.1.X under eth0 or enp0s3.

## Step 6: Set Network to Bridged Adapter (If Not Already)
Power off the VM

In VirtualBox > Settings > Network, change:

Attached to → Bridged Adapter

Start the VM again

## Step 7: Access Nginx from Host Machine
Option 1: Browser
On your host machine, open a browser and visit:
```
http://<VM_IP>
```
Example:
```
http://192.168.1.6
```
You should see the Nginx page served by the Docker container.

Option 2: Terminal (curl)
```bash
curl http://<VM_IP>
```
You should see the HTML output of the Nginx homepage.

### Success!
You have successfully:

Installed Docker on Kali Linux

Deployed Nginx in a Docker container

Accessed the Nginx server from your host machine via bridged networking
