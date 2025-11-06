# Static-Website-Hosting-Storage-CDN-
Host static HTML/CSS files on cloud object storage and use CDN for global delivery.

You are hosting a **static website (HTML, CSS, images)** on **Amazon S3**.

There are **two ways** to show your website to the world 👇

---

### ✅ Option 1: Only S3 (Simple, HTTP)

You only use **S3**, and your website will have an address like:
http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com


🟢 **Free, simple, perfect for learning or small projects.**  
But:
- ❌ No HTTPS (browser says “Not Secure”)  
- 🐢 Loads slightly slower (from one AWS region)

---

### ✅ Option 2: S3 + CloudFront (HTTP + HTTPS)

You add **CloudFront (CDN = Content Delivery Network)**  
It sits between your users and S3.

👉 Think of CloudFront as a *helper* that:
- Caches your website content worldwide 🌍 (faster loading)
- Gives **free HTTPS (SSL)** 🔒
- Protects your site from heavy traffic / DDoS ⚔️

Your website will then open from:


https://d1234abcd.cloudfront.net


---

## 💰 About the Cost

| Feature | AWS Service | Cost |
|----------|--------------|------|
| Website files | S3 | ✅ Free for 5GB (Free Tier) |
| HTTPS / Caching | CloudFront | ✅ Free for 1TB/month (Free Tier) |
| Domain (like .com) | Route 53 | ❌ Paid (skip it) |

> 💡 I didn’t use **Route 53** because it requires charges,  
> but you can use it if you have your own domain.

So, if you stay within free tier limits:
🟢 **No money is charged.**  
Even CloudFront + HTTPS is **free for 12 months** under AWS Free Tier.

---

## 💬 So What You Can Do

If you don’t need HTTPS and just want a working demo:
- ✅ Use **only S3**
- ✅ Enable **Static Website Hosting**
- ✅ Open via your S3 website endpoint (HTTP)
- ❌ Skip CloudFront (optional)

That’s completely **free and enough for learning.**

---

## 🧱 You’ll Learn

You’ll understand how to host your static website securely using:

- 🪣 **Amazon S3** → store and host website files  
- ⚡ **CloudFront** → global CDN + free HTTPS (SSL)  
- 🚫 **No Route 53 / no paid domain** → use free CloudFront URL  

---

## 🌍 Project Overview

**Goal:** Host a static website (HTML/CSS/JS) on AWS for free.

**Architecture:**  
User → CloudFront (CDN + HTTPS) → S3 (Website files)

---

## 🧭 Step-by-Step Implementation (Manual Way)

### 🪣 Step 1: Create an S3 Bucket

1. Go to **AWS Console → S3 → Create bucket**  
2. Name your bucket, e.g. `mywebsite-demo-2025`  
3. Choose **Region:** `ap-south-1 (Mumbai)`  
4. **Uncheck** “Block all public access”  
5. Confirm warning ✅ and click **Create bucket**

---

### 🧾 Step 2: Upload Website Files

Upload these:
- `index.html`
- Any CSS, JS, or image files

**Example:**

```html
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

⚙️ Step 3: Enable Static Website Hosting in S3

Go to Bucket → Properties tab

Scroll to Static website hosting → Click Edit

Choose Enable

Index document: index.html

Save changes

You’ll now get a website link like:

http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com


✅ Open this link to test your website.

🔐 Step 4: Set Bucket Policy (Public Access)

Go to Permissions → Bucket policy → Edit

Paste this JSON (replace your bucket name):

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


Click Save changes.

⚡ Step 5: Create a CloudFront Distribution (for HTTPS)

Go to AWS Console → CloudFront → Create Distribution

Origin domain: choose your S3 website endpoint
(ends with s3-website-ap-south-1.amazonaws.com)

Viewer protocol policy: Redirect HTTP → HTTPS

Default root object: index.html

Leave other settings default → Create Distribution

Wait 10–15 minutes until the status changes to Deployed.

🌐 Step 6: Access Your Website

Once deployed, your website will be available at:

https://d1234abcd.cloudfront.net


✅ Congratulations! You now have a secure, globally available static site 🎉

💻 Ways to Host a Website on AWS
1️⃣ Static Website Hosting (HTML, CSS, JS — No Backend)

➡️ For simple sites (portfolio, landing pages, blogs)

🔹 Option A: Amazon S3

Store & serve static files directly

Optional: Add CloudFront for HTTPS & caching
✅ Easy to set up
✅ Very low cost
❌ No backend logic

🔹 Option B: AWS Amplify

For React / Vue / Angular frontends

Auto-deploys from GitHub
✅ HTTPS + custom domain
❌ Slightly higher cost

2️⃣ Dynamic Website Hosting (with Backend)

➡️ For sites needing PHP, Node.js, etc.

🔹 Option A: Amazon EC2

Full control (Apache/Nginx, OS-level setup)
✅ Most flexible
❌ Manual setup required

🔹 Option B: AWS Lightsail

Beginner-friendly version of EC2
✅ Fixed pricing (~$5/month)
✅ One-click WordPress / LAMP
❌ Limited scalability

🔹 Option C: Elastic Beanstalk

AWS handles EC2 + scaling automatically
✅ Auto-scaling built-in
❌ Less control

3️⃣ Serverless Website Hosting

➡️ For fully managed, no-server apps.

🔹 Option A: AWS Lambda + API Gateway + S3

✅ No server management
✅ Pay only when used
❌ Complex setup

4️⃣ Container-Based Hosting

Amazon ECS / EKS for Docker-based apps
✅ Scalable and modern
❌ Advanced setup (DevOps level)

5️⃣ Using AWS Marketplace

Ready-made apps like WordPress, Joomla
✅ Quick setup
❌ Paid
