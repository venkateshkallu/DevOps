#  Setting Up Multiple VMs on VirtualBox and Running Web Servers on Kali, Fedora, and CentOS

##  Overview

As part of my learning journey in virtualization and DevOps, I used **VirtualBox** to create virtual machines with different Linux operating systems. On each VM, I successfully installed and tested **web servers (Apache and Nginx)**. This guide documents the steps I followed, official sources, and commands I used.

---

## Tools & Technologies Used

| Category | Tool / OS |
|----------|-----------|
| Virtualization Software | [Oracle VirtualBox](https://www.virtualbox.org/) |
| OS (ISO downloads) | Kali Linux, Fedora, CentOS |
| Web Servers | Apache HTTP Server, Nginx |
| Terminal | Linux Terminal / Bash |

---

## 1. Downloading and Installing VirtualBox

Download VirtualBox for your platform from the official website:

**VirtualBox Download**: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

Install the latest version suitable for your OS (Windows/Linux/macOS).

---

## 2. OS ISO Downloads

Below are the official links I used to download the ISOs:

- **Kali Linux**: [https://www.kali.org/get-kali/](https://www.kali.org/get-kali/)
- **Fedora Workstation**: [https://getfedora.org/en/workstation/download/](https://getfedora.org/en/workstation/download/)
- **CentOS Stream**: [https://www.centos.org/download/](https://www.centos.org/download/)

Each ISO was added to VirtualBox while creating a new VM with:
- Type: Linux
- Version: 64-bit
- RAM: Min 2048 MB
- Storage: Min 20 GB

---

## 3. Setting Up VMs

I created **3 separate VMs** in VirtualBox for the following:

| VM Name | OS | Servers Installed |
|---------|----|-------------------|
| Kali_VM | Kali Linux | Apache, Nginx |
| Fedora_VM | Fedora | Apache, Nginx |
| CentOS_VM | CentOS | Nginx |

---

## 4. Installing Apache & Nginx on Each VM

Below are the commands I used to install and run web servers on each distribution.

---

###  A. **Fedora VM**

Install and start **Apache**:
```bash
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
Install and start **Nginx**:

```bash
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```
Test in browser :
```bash
http://localhost
```
### B. Kali Linux VM
Install and start Apache:

```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```
Install and start Nginx:
```bash
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```
Check server output:

```bash
curl http://localhost
```
## C. CentOS VM
Install and start Nginx:
```bash
sudo yum install epel-release -y
sudo yum install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```
- Apache was not installed on CentOS in this setup.

### 5. Testing the Servers
For each VM, I verified the installation by:

Checking with ```curl http://localhost```

Opening ```http://localhost``` in the VM’s browser

Verifying services using:

```bash
sudo systemctl status nginx
sudo systemctl status apache2  # or httpd in Fedora
```
