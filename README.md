

# 🌩️ AWS Static Website Hosting Project (S3 + CloudFront)

## ☁️ Overview

This project demonstrates how to **host a static website (HTML, CSS, images)** on **Amazon S3**, with optional **Amazon CloudFront** for **HTTPS** and **global content delivery (CDN)**.

---

## 🚀 Project Goal

Host a **secure, globally available static website** on AWS for **free** using:

- 🪣 **Amazon S3** → store and host website files  
- ⚡ **Amazon CloudFront** → CDN + free HTTPS (SSL)  
- 🚫 **No Route 53 / no paid domain** → use free CloudFront URL  

**Architecture:**


User → CloudFront (CDN + HTTPS) → S3 (Website files)


---

## 💡 Hosting Options

### ✅ Option 1: Only S3 (Simple, HTTP)

Use **only S3** for website hosting.

**Example URL:**


http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com


**Pros:**  
- 🟢 Simple & free  
- 🟢 Great for learning  

**Cons:**  
- ❌ No HTTPS (Not Secure)  
- 🐢 Slightly slower from one AWS region

---

### ✅ Option 2: S3 + CloudFront (HTTP + HTTPS)

Add **CloudFront (CDN)** for better performance and security.

**Example URL:**


https://d1234abcd.cloudfront.net


**Benefits:**
- 🌍 Global caching (faster load times)  
- 🔒 Free HTTPS (SSL certificate)  
- ⚔️ DDoS protection & scaling  

---

## 💰 AWS Free Tier Cost Breakdown

| Feature | AWS Service | Cost |
|----------|--------------|------|
| Website files | Amazon S3 | ✅ Free (5GB) |
| HTTPS / CDN | CloudFront | ✅ Free (1TB/month) |
| Custom Domain | Route 53 | ❌ Paid (optional) |

💡 **Stay within free tier → No charges for 12 months**

---

![Screenshot 2025-11-06 091733](https://github.com/user-attachments/assets/f99ed0f0-996d-4571-88ca-89e61204eab3)
<p align="center">
  <img src="https://github.com/user-attachments/assets/f99ed0f0-996d-4571-88ca-89e61204eab3" alt="Screenshot 2025-11-06 091733" width="700">
</p>



## 🧱 Step-by-Step Implementation

### 🪣 Step 1: Create an S3 Bucket

1. Go to **AWS Console → S3 → Create bucket**  
2. Bucket name: `mywebsite-demo-2025`  
3. Region: `ap-south-1 (Mumbai)`  
4. **Uncheck** “Block all public access”  
5. Confirm the warning and click **Create bucket**

---

### 🧾 Step 2: Upload Website Files

Upload these files:
- `index.html`
- `style.css`
- `script.js`
- Images (optional)

---
## 🧩 Example `index.html` File

```html
<!DOCTYPE html>
<html>
<head>
  <title>My AWS Website</title>
  <style>
    body {
      background-color: #f0f0f0;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 100px;
    }
    h1 {
      color: #0066cc;
    }
  </style>
</head>
<body>
  <h1>Welcome to My AWS Hosted Website!</h1>
  <p>This site is hosted using Amazon S3 and CloudFront.</p>
</body>
</html>
---

⚙️ Step 3: Enable Static Website Hosting
Go to Bucket → Properties → Static website hosting → Edit

Choose Enable

Enter:

Index document: index.html

Save changes

You’ll get a website endpoint like:

arduino
Copy code
http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com
✅ Open this link to test your website.

🔐 Step 4: Set Bucket Policy (Public Access)
Go to Permissions → Bucket Policy → Edit

Paste the following JSON (replace your bucket name):

json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mywebsite-demo-2025/*"
    }
  ]
}
✅ Save the policy.

⚡ Step 5: Create a CloudFront Distribution (for HTTPS)
Go to CloudFront → Create Distribution

Origin domain: Choose your S3 website endpoint (ends with s3-website-ap-south-1.amazonaws.com)

Viewer protocol policy: Redirect HTTP → HTTPS

Default root object: index.html

Leave other settings default → Create Distribution

⏳ Wait 10–15 minutes until Status = Deployed

🌐 Step 6: Access Your Website
Once deployed, your CloudFront URL will look like:

arduino
Copy code
https://d1234abcd.cloudfront.net
🎉 Congratulations!
You now have a secure, fast, and globally available static website.

💻 Other AWS Website Hosting Methods
Type	Description	AWS Services	Pros	Cons
Static Website	Only HTML/CSS/JS	S3 + CloudFront	Easy, Free	No backend
Frontend Hosting	React/Vue/Angular	AWS Amplify	Auto-deploy, HTTPS	Slightly higher cost
Dynamic Website	Backend apps (PHP, Node.js)	EC2 / Lightsail / Beanstalk	Full control	Paid
Serverless	Pay-per-use	Lambda + API Gateway + S3	No servers, cheap	Complex
Containers	Dockerized apps	ECS / EKS	Scalable	Advanced setup
Pre-built Apps	WordPress, Joomla	AWS Marketplace	Quick setup	Paid

🧠 You’ll Learn
By completing this project, you’ll understand:

How to host a static website using Amazon S3

How to enable HTTPS and caching using CloudFront

AWS permissions, policies, and hosting configuration

Differences between various AWS hosting services

📦 Architecture Diagram
sql
Copy code
      +--------------------+
      |     CloudFront     |
      |  (CDN + HTTPS)     |
      +---------+----------+
                |
                ↓
      +--------------------+
      |     S3 Bucket      |
      | (Static Website)   |
      +--------------------+
🧩 Tech Stack
Frontend: HTML, CSS

AWS Services: S3, CloudFront

Security: IAM, Bucket Policies, HTTPS

Region: ap-south-1 (Mumbai)

🏁 Result
✅ Website hosted successfully on AWS
✅ HTTPS enabled via CloudFront
✅ Completely free under AWS Free Tier
✅ Great performance and global reach

![Screenshot 2025-11-06 091733](https://github.com/user-attachments/assets/f99ed0f0-996d-4571-88ca-89e61204eab3)
<p align="center">
  <img src="https://github.com/user-attachments/assets/f99ed0f0-996d-4571-88ca-89e61204eab3" alt="Screenshot 2025-11-06 091733" width="700">
</p>


