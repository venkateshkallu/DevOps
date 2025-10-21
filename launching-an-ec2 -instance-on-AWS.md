# 🚀 Step-by-Step Guide to Launching an EC2 Instance on AWS

**Author:** *Venkatesh*
**Under the mentorship of:** *Solution Architect*
**Published:** 2025

---

## 🧩 Overview

Amazon EC2 (Elastic Compute Cloud) is a key AWS service that allows you to launch and manage virtual servers in the cloud.
This guide provides a **step-by-step walkthrough** to create, configure, and connect to your first EC2 instance — followed by essential **interview questions** to strengthen your AWS fundamentals.

---

## ⚙️ Step 1: Log in to the AWS Management Console

1. Navigate to the [AWS Management Console](https://aws.amazon.com/console/).
2. Enter your credentials to access the dashboard.

---

## ⚙️ Step 2: Access the EC2 Dashboard

1. In the AWS search bar, type **EC2** and select it from the dropdown.
2. You’ll be directed to the **EC2 Dashboard**.

---

## ⚙️ Step 3: Launch a New Instance

1. From the left-hand menu, click **Instances**.
2. On the right side, click **Launch Instances**.

---

## ⚙️ Step 4: Configure Your Instance

* **Name Your Instance:** `My-Website`
* **Choose AMI:** Select **Amazon Linux 2** (recommended for beginners).
* **Instance Type:** `t3.micro` (Free Tier eligible).

---

## ⚙️ Step 5: Configure Instance Details

* Keep default settings unless you have specific requirements.
* Click **Next: Add Storage.**

---

## ⚙️ Step 6: Add Storage

* Default **8 GB General Purpose SSD (gp2)** is sufficient.
* Click **Next: Add Tags.**

---

## ⚙️ Step 7: Add Tags

Tags are optional but useful for organizing and managing your resources.
Click **Next: Configure Security Group.**

---

## ⚙️ Step 8: Configure Security Group

Create a new Security Group named `My-Security-Group`.

| Type | Protocol | Port Range | Source    | Description         |
| ---- | -------- | ---------- | --------- | ------------------- |
| SSH  | TCP      | 22         | My IP     | Secure shell access |
| HTTP | TCP      | 80         | 0.0.0.0/0 | Allow web traffic   |

Click **Review and Launch.**

---

## ⚙️ Step 9: Review and Launch

1. Review all configurations.
2. Click **Launch**.
3. Create a new key pair named `My-KeyPair`.
4. Download the `.pem` file and store it safely — you’ll need it to connect to your instance.

---

## ⚙️ Step 10: Access Your Instance

Once your instance state is **Running**, note the **Public IPv4 DNS** or IP.

### 🔹 For Linux / macOS (SSH Connection)

```bash
chmod 400 /path/to/My-KeyPair.pem
ssh -i /path/to/My-KeyPair.pem ec2-user@<Public-IP>
```

Replace:

* `/path/to/` → actual path to your `.pem` file
* `<Public-IP>` → instance public IP address

### 🔹 For Windows (Using PuTTY)

1. **Convert `.pem` to `.ppk`:**

   * Open PuTTYgen → Load your `.pem` file → Click **Save Private Key** → Save as `.ppk`.

2. **Open PuTTY:**

   * Host Name: `ec2-user@<Public-IP>`
   * Connection Type: SSH

3. **Add Private Key:**

   * Go to *Connection → SSH → Auth → Browse* → Select `.ppk` file.

4. **Connect:**

   * Click **Open**, accept host key → You’re now connected.

---

## 🌐 Optional: Host a Simple Website

To install and run a basic Apache web server, run:

```bash
sudo yum install httpd -y
sudo service httpd start
sudo chkconfig httpd on
echo "<h1>This is my first webserver</h1>" | sudo tee /var/www/html/index.html
```

Open a browser → Enter your EC2 public IP → You should see your webpage.

---

## 💡 Common EC2 Interview Questions (2025)

### 🔹 **Basic Understanding**

**1. What is Amazon EC2?**
Amazon EC2 provides resizable compute capacity in the cloud. It lets you run virtual servers (instances) on demand.

**2. What are the different instance types?**
Compute-optimized, memory-optimized, storage-optimized, and general-purpose instances.

**3. What’s the difference between on-demand, reserved, and spot instances?**

* **On-Demand:** Pay-as-you-go, no commitment.
* **Reserved:** Discounted pricing with 1–3 year commitment.
* **Spot:** Use spare capacity at a lower price (can be interrupted).

---

### 🔹 **Scenario-Based Questions**

**4. You launched an EC2 instance but can’t SSH into it. Why?**

* Security group not allowing port 22
* Wrong key pair
* Instance missing a public IP
* Incorrect username

**5. How can you automate software installation on startup?**
Use **User Data scripts** during launch to install packages and set up services automatically.

**6. How can you secure your EC2 instances?**

* Restrict network access with Security Groups
* Apply IAM roles for permissions
* Use SSH key pairs
* Regularly patch and update
* Enable CloudWatch for monitoring

---

### 🔹 **Advanced Topics**

**7. What is Auto Scaling in EC2?**
Auto Scaling automatically adjusts the number of EC2 instances based on demand — ensuring high availability and optimized cost.

**8. What is Elastic Load Balancing (ELB)?**
ELB distributes traffic across multiple EC2 instances to improve fault tolerance and availability.

---

## 📚 Further Reading & References

* [NetCom Learning – 90+ AWS Interview Questions (2025)](https://www.netcomlearning.com/)
* [DataCamp – Top 50 AWS Interview Questions (2025)](https://www.datacamp.com/)
* [Medium – AWS EC2 Interview Guide (2025)](https://medium.com/)
* [InterviewBit – AWS Interview Questions (2025)](https://www.interviewbit.com/)

---

## 🗣️ Sample Interview Answer (Conversational Style)

> “To launch an EC2 instance, I first log in to the AWS Console, search for EC2, and click **Launch Instance**.
> I name the instance, choose **Amazon Linux 2**, select **t3.micro**, and create a security group with SSH and HTTP rules.
> Then I generate a key pair to connect securely, launch the instance, and connect using SSH.
> Optionally, I can install Apache using a User Data script to host a simple webpage.”

---

## 🏁 **Conclusion**

You’ve now learned how to:

* Launch and configure an EC2 instance from scratch
* Connect via SSH or PuTTY
* Deploy a basic web server
* Prepare for EC2 interview questions

---

**👨‍💻 Author:** *Venkatesh*
**🧭 Mentored by:** *Solution Architect*
**Category:** *AWS | DevOps | Cloud Fundamentals*
