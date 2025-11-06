# 🌐 Static Website Hosting on AWS (S3 + CloudFront)

Host static **HTML / CSS / JS** files on **Amazon S3** and use **Amazon CloudFront (CDN)** for global, fast, and secure delivery.  

---

## 🧭 Overview

You are hosting a **static website (HTML, CSS, images)** on **Amazon S3**.

There are **two ways** to make your website available to the world 👇

---

### ✅ Option 1: Only S3 (Simple, HTTP)

You only use **S3**, and your website will have an address like:


🟢 **Free, simple, and perfect for learning or small projects.**  

But:
- ❌ No HTTPS (browser says “Not Secure”)  
- 🐢 Slightly slower loading (only from one AWS region)

---
http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com
### ✅ Option 2: S3 + CloudFront (HTTP + HTTPS)

You add **CloudFront (CDN = Content Delivery Network)** — a global caching service that sits between your users and S3.

👉 **Think of CloudFront as a helper** that:
- Caches your website content worldwide 🌍 (faster loading)
- Provides **free HTTPS (SSL)** 🔒
- Protects your site from DDoS & heavy traffic ⚔️

Your website will open from:https://d1234abcd.cloudfront.net

---

## 💰 Cost Overview

| Feature | AWS Service | Cost |
|----------|--------------|------|
| Website files | S3 | ✅ Free for 5GB (Free Tier) |
| HTTPS / Caching | CloudFront | ✅ Free for 1TB/month (Free Tier) |
| Domain (Route 53) | Route 53 | ❌ Paid (optional) |

> 💡 This project skips **Route 53** to stay 100% free.  
> You can use it later for a custom domain if needed.

🟢 **If you stay in AWS Free Tier limits:**  
You won’t be charged — even CloudFront HTTPS is free for 12 months.

---

## 💬 What You Can Do

If you just want a **working free demo**:
- ✅ Use **only S3**
- ✅ Enable **Static Website Hosting**
- ✅ Access via **S3 website endpoint (HTTP)**
- ❌ Skip CloudFront (optional)

---

## 🧱 You’ll Learn

You’ll understand how to host a website securely using:

- 🪣 **Amazon S3** → Store and host static files  
- ⚡ **Amazon CloudFront** → Global CDN + free HTTPS  
- 🚫 **No Route 53** → Use CloudFront’s free domain  

---

## 🌍 Project Architecture

**Goal:** Host a static website (HTML/CSS/JS) on AWS Free Tier.

**Architecture Flow:**  
🧑‍💻 User → 🌐 CloudFront (CDN + HTTPS) → 🪣 S3 (Website files)

---

## 🧭 Step-by-Step Implementation

### 🪣 Step 1: Create an S3 Bucket

1. Go to **AWS Console → S3 → Create Bucket**  
2. Name: `mywebsite-demo-2025`  
3. Region: `ap-south-1 (Mumbai)`  
4. **Uncheck** “Block all public access”  
5. Confirm the warning ✅ and click **Create Bucket**

---

### 🧾 Step 2: Upload Website Files

Upload these files to your bucket:
- `index.html`
- Any CSS, JS, or image files

**Example index.html:**


<!DOCTYPE html>
<html>
<head>
  <title>My AWS Website</title>
  <style>
    body { background-color: #f0f0f0; font-family: Arial; text-align: center; padding: 100px; }
    h1 { color: #0066cc; }
  </style>
</head>
<body>
  <h1>Welcome to My AWS Hosted Website!</h1>
  <p>This site is hosted using Amazon S3 and CloudFront.</p>
</body>
</html>


🌐 Step 3: Enable Static Website Hosting in S3

Go to Bucket → Properties tab

Scroll to Static website hosting → Edit

Choose Enable

Index document: index.html

Click Save changes

You’ll now get a website link like:

http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com


✅ Open this link in your browser to test your site.

🔐 Step 4: Set Bucket Policy (Public Access)

Go to Permissions → Bucket Policy → Edit

Paste this JSON policy (replace your bucket name if needed):

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


Click Save Changes.

⚡ Step 5: Create a CloudFront Distribution (for HTTPS)

Go to AWS Console → CloudFront → Create Distribution

Origin Domain: mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com

Viewer Protocol Policy: Redirect HTTP → HTTPS

Default Root Object: index.html

Leave other options default

Click Create Distribution

Wait 10–15 minutes for the status to show Deployed

🌍 Step 6: Access Your Website via CloudFront

Once deployed, your website is available at:

https://d1234abcd.cloudfront.net


✅ Congratulations! You now have a secure, global static website 🎉

💻 Other AWS Website Hosting Options
1️⃣ Static Website Hosting (HTML, CSS, JS — No Backend)

➡️ For simple sites like portfolios or blogs.

🔹 Option A: Amazon S3

Stores & serves static files

Add CloudFront for HTTPS
✅ Easy setup | ✅ Cheap | ❌ No backend logic

🔹 Option B: AWS Amplify

For React / Vue / Angular

Auto-deploys from GitHub
✅ Built-in HTTPS | ❌ Slightly higher cost

2️⃣ Dynamic Website Hosting (with Backend)

🔹 Option A: EC2

Full server control (Apache / Nginx)
✅ Flexible | ❌ Manual setup

🔹 Option B: Lightsail

Beginner-friendly EC2
✅ Fixed pricing (~$5/month) | ❌ Limited scaling

🔹 Option C: Elastic Beanstalk

AWS handles EC2 + auto-scaling
✅ Easy | ❌ Less control

3️⃣ Serverless Website Hosting

🔹 Option A: AWS Lambda + API Gateway + S3
✅ No server management | ❌ Complex setup

4️⃣ Container-Based Hosting

🔹 Amazon ECS / EKS
✅ Highly scalable | ❌ Advanced setup

5️⃣ AWS Marketplace

🔹 WordPress, Joomla, Drupal (pre-configured images)
✅ Quick setup | ❌ Paid

🏁 Final Output
Layer	Service	Role
Storage	Amazon S3	Host website files
CDN / SSL	CloudFront	Global caching + HTTPS
Optional Domain	Route 53	Custom domain mapping

🎯 End Result:
A fast, free, secure, globally available website hosted entirely on AWS 🚀


---

Would you like me to generate this as a **downloadable `README.md` file** (ready f

