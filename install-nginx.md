## Installing and Accessing Nginx on a Kali Linux Virtual Machine

This guide will walk you through installing Nginx on a Kali Linux VM and accessing the web server from your **host machine**.

---

### Prerequisites

- Virtual Machine with **Kali Linux** running
- VirtualBox installed
- Nginx installed and running inside the VM
- Network set to **Bridged Adapter** in VM settings

---

###  Step 1: Start Kali Linux VM

Start your VirtualBox VM with Kali Linux.

---

###  Step 2: Install Nginx on Kali

Open the terminal inside the Kali VM and run:

```bash
sudo apt update
sudo apt install nginx -y
```
 ### Step 3: Start and Enable Nginx
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```
### Step 4: Check Nginx Status
```bash
sudo systemctl status nginx
``` 
Look for active (running) in green text.

### Step 5: Test Nginx Inside the VM
Open Firefox or any browser inside the VM and go to:

```arduino
http://localhost
```
You should see the default Nginx welcome page.

### Step 6: Get the VM's IP Address
In the terminal, run:

```bash
ip a
```
Look for an IP like 192.168.1.4 under eth0 or enp0s3.

### Step 7: Set VM Network to Bridged Adapter
Power off your VM

Go to VirtualBox > Settings > Network

Change "Attached to" from NAT to Bridged Adapter

Start the VM again

### Step 8: Access Nginx from Host Machine
Open a browser on your host machine and go to:

```cpp

http://<VM_IP>
```
Example:

```cpp

http://192.168.1.4
```
You should see the same Nginx welcome page.

Optional: Test with curl from Host Terminal
If you prefer the terminal:

```bash

curl http://192.168.1.4
```
You should see HTML output of the Nginx page.

