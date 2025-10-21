# ⚙️ Automate EC2 Server Deployment & Manage Termination Protection

**Author:** *Venkatesh*
**Under the mentorship of:** *Solution Architect*
**Published:** 2025

---

## 🎯 Objective

To **automate the deployment of a web server** on an **Amazon EC2 instance** using a **User Data script** and demonstrate how to **enable and disable termination protection** for securing critical instances from accidental deletion.

---

## 🧩 Step 1: Launch a New EC2 Instance

1. Navigate to the **AWS Management Console → EC2 Dashboard → Launch Instance**.
2. **Instance Name:** `Automated-WebServer`
3. **Operating System:** Select **Amazon Linux 2 (Free Tier eligible)** — recommended for compatibility and performance.
4. **Instance Type:** Choose **t3.micro (Free Tier eligible)**.
5. **Key Pair (Login):**

   * Create a new key pair (e.g., `webserver-key.pem`) if you plan to connect from your local system.
   * Download and keep it securely for SSH access.

---

## ⚙️ Step 2: Configure Advanced Settings
<img width="1295" height="640" alt="image" src="https://github.com/user-attachments/assets/0e23dcfc-8588-44a1-9826-0a08b300c643" />


1. Expand **Advanced Settings** during instance setup.
2. Enable:

   > ✅ **“Enable Termination Protection”**

   This ensures your instance cannot be accidentally terminated.
3. In the **User Data** field, paste the following automation script:
<img width="1313" height="625" alt="image" src="https://github.com/user-attachments/assets/a0d590fa-9d5c-497e-9d83-c841a150ad53" />


```bash
#!/bin/bash
yum install httpd -y
service httpd start
chkconfig httpd on
echo "<h1>This is my first webserver</h1>" > /var/www/html/index.html
```

### 🧠 Script Purpose:

* Installs the **Apache HTTP web server**
* Starts the service automatically on boot
* Creates a simple HTML webpage served via your instance’s public IP

Click **Launch Instance** to deploy the server.

---

## ⚙️ Step 3: Configure Security Group

During setup or after launching:

1. Go to **Network Settings → Security Group**.
2. Add an **Inbound Rule** as shown below:

| Type | Protocol | Port | Source    | Description                        |
| ---- | -------- | ---- | --------- | ---------------------------------- |
| HTTP | TCP      | 80   | 0.0.0.0/0 | Allow web traffic from any browser |

Click **Save Rules** to apply.

---

## 🧩 Step 4: Verify the Web Server

<img width="1313" height="625" alt="image" src="https://github.com/user-attachments/assets/7651be84-f6ad-49f2-8adb-131d30d2f020" />


1. Wait until your instance shows **2/2 Status Checks Passed**.
2. Copy your instance’s **Public IPv4 Address**.
3. Open any browser and paste the IP.
4. You should see:

> **This is my first webserver**

✅ This confirms that your **User Data automation script** executed successfully.

---

## ⚙️ Step 5: Disable Termination Protection (When Needed)

<img width="1313" height="625" alt="image" src="https://github.com/user-attachments/assets/97b514e4-91ab-4014-b49f-2f5104deaed0" />


If you need to terminate the instance later:

1. Go to **EC2 → Instances**.
2. Click on the **Instance ID** of your running instance.
3. Navigate to:
   **Actions → Instance Settings → Change Termination Protection**
4. Uncheck **Enable Termination Protection → Save Changes.**
<img width="1313" height="625" alt="Screenshot from 2025-10-21 12-04-10" src="https://github.com/user-attachments/assets/096e0267-a37a-4b79-9a67-3e85a714ce8f" />


You can now safely terminate the instance when required.

---

## 🧠 Key Learnings

| Concept           | Description                                                     |
| ----------------- | --------------------------------------------------------------- |
| **Automation**    | User Data enables setup and configuration during instance boot. |
| **Security**      | Termination protection prevents accidental deletions.           |
| **Accessibility** | Security groups define inbound/outbound traffic rules.          |

---

## 🧰 Real-World Use Case

System administrators and DevOps engineers use **User Data scripts** to:

* Install software automatically during deployment
* Bootstrap CI/CD agents
* Configure monitoring tools
* Initialize web or application servers
---
💬 Interview Questions & Answers
🟢 1. What is the purpose of the User Data field in EC2?



Answer:
User Data allows you to run shell scripts or cloud-init directives when the instance is launched. It automates tasks such as software installation, configuration, and service setup during instance boot.

🟢 2. Why do we enable Termination Protection in EC2?



Answer:
Termination Protection prevents accidental deletion of critical EC2 instances. You must manually disable it before terminating the instance, ensuring data safety and operational stability.

🟢 3. What is the default web server directory in Amazon Linux?



Answer:
/var/www/html — this is the default root directory where Apache serves web pages from.

🟢 4. What is the difference between Security Groups and NACLs?



Answer:

Security Groups act as stateful firewalls at the instance level.
Network ACLs (NACLs) are stateless and apply at the subnet level.
Security Groups remember traffic states, while NACLs check both inbound and outbound rules for every request.
🟢 5. How do you connect to an EC2 instance from your local machine?



Answer:
Use SSH with your private key file:

ssh -i webserver-key.pem ec2-user@<public-ip>

🟢 6. How can you automate EC2 deployment without manual console actions?



Answer:
You can use:

AWS CLI commands
AWS CloudFormation templates
Terraform scripts
These allow Infrastructure as Code (IaC) for repeatable deployments.
🟢 7. How can you verify if termination protection is enabled using the AWS CLI?



Answer:
Run:

aws ec2 describe-instance-attribute --instance-id <id> --attribute disableApiTermination




If the value is true, termination protection is enabled.

🟢 8. Can User Data scripts run multiple times?



Answer:
By default, User Data scripts run only once at the first boot.
If you want it to run every time, modify the script or cloud-init config to re-enable execution.

🟢 9. What happens if the User Data script fails?



Answer:
The instance still launches, but the configured tasks (like Apache installation) won’t execute correctly. You can view logs at:

/var/log/cloud-init-output.log




to troubleshoot.

🟢 10. How would you secure a web server in production?



Answer:

Restrict SSH access using specific IPs
Use HTTPS with SSL/TLS
Enable CloudWatch for monitoring
Create IAM roles instead of hardcoding credentials
Apply least privilege security principles
🏁 Conclusion



By completing this automation project, you’ve learned how to:
✅ Launch and configure an EC2 instance
✅ Automate setup using User Data
✅ Enable & disable termination protection
✅ Configure networking for HTTP access
✅ Understand practical AWS interview concepts

---

## 🏁 Conclusion

By completing this automation setup, you’ve learned to:
✅ Launch an EC2 instance with predefined configuration
✅ Automate Apache installation using User Data
✅ Enable and disable termination protection
✅ Verify your hosted web page

---

**👨‍💻 Author:** *Venkatesh*
**🧭 Mentored by:** *Solution Architect*
**Category:** *AWS | DevOps | Automation | Cloud Fundamentals*
