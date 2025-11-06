# 🌩️ AWS Static Website Hosting Project (S3 + CloudFront)

## ☁️ Overview

This project demonstrates how to **host a static website (HTML, CSS, images)** on **Amazon S3**, with optional integration of **Amazon CloudFront** for **HTTPS** and **global content delivery (CDN)**.

---

## 🚀 Project Goal

Host a **secure, globally available static website** on AWS for **free** using:

- 🪣 **Amazon S3** → store and host website files  
- ⚡ **Amazon CloudFront** → global CDN + free HTTPS (SSL)  
- 🚫 **No Route 53 / no paid domain** → use free CloudFront URL  

**Architecture:**

User → CloudFront (CDN + HTTPS) → S3 (Website files)

yaml
Copy code

---

## 💡 Hosting Options

### ✅ Option 1: Only S3 (Simple, HTTP)

Use **only Amazon S3** for static website hosting.

**Example URL:**
http://mywebsite-demo-2025.s3-website-ap-south-1.amazonaws.com

yaml
Copy code

**Pros:**
- 🟢 Free and simple  
- 🟢 Perfect for learning or small projects  

**Cons:**
- ❌ No HTTPS (browser shows “Not Secure”)  
- 🐢 Slightly slower (served from one AWS region)

---

### ✅ Option 2: S3 + CloudFront (HTTP + HTTPS)

Add **CloudFront (CDN)** in front of your S3 bucket for better performance and security.

**Example URL:**
https://d1234abcd.cloudfront.net

php-template
Copy code

**Benefits:**
- 🌍 Global caching (faster load times)
- 🔒 Free HTTPS (SSL certificate)
- ⚔️ DDoS protection and traffic management

---

## 💰 AWS Free Tier Cost Breakdown

| Feature | AWS Service | Cost |
|----------|--------------|------|
| Website files | Amazon S3 | ✅ Free up to 5GB |
| HTTPS / CDN | Amazon CloudFront | ✅ Free up to 1TB/month |
| Custom Domain | Route 53 | ❌ Paid (optional) |

> 💡 Stay within free tier limits → **No charges for 12 months**

---

## 🧱 Step-by-Step Implementation

### 🪣 Step 1: Create an S3 Bucket
1. Go to **AWS Console → S3 → Create bucket**  
2. Name your bucket, e.g. `mywebsite-demo-2025`  
3. Choose **Region:** `ap-south-1 (Mumbai)`  
4. **Uncheck** “Block all public access”  
5. Confirm warning ✅ and click **Create bucket**

---

### 🧾 Step 2: Upload Website Files

Upload your files:
- `index.html`
- `style.css`
- `script.js`
- Any image files

**Example `index.html`:**

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
Go to Permissions → Bucket Policy → Edit, then paste:

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
Save the policy ✅

⚡ Step 5: Create a CloudFront Distribution (for HTTPS)
Go to CloudFront → Create Distribution

Origin domain: choose your S3 website endpoint
(ends with s3-website-ap-south-1.amazonaws.com)

Viewer protocol policy: Redirect HTTP → HTTPS

Default root object: index.html

Leave other settings default → Create Distribution

Wait for 10–15 minutes until the status becomes Deployed.

🌐 Step 6: Access Your Website
After deployment, access your site at:

arduino
Copy code
https://d1234abcd.cloudfront.net
🎉 Congratulations! Your website is now secure, fast, and globally available!

💻 Other AWS Website Hosting Methods
Type	Description	AWS Services	Pros	Cons
Static Website	Only HTML/CSS/JS	S3 + CloudFront	Easy, Free	No backend
Frontend Hosting	React/Vue/Angular	AWS Amplify	Auto-deploy, HTTPS	Slightly higher cost
Dynamic Website	Backend apps (PHP, Node.js)	EC2 / Lightsail / Beanstalk	Full control, scalable	Paid
Serverless	Pay-per-use functions	Lambda + API Gateway + S3	No servers, cheap	Complex
Containers	Dockerized apps	ECS / EKS	Scalable, modern	Advanced setup
Pre-built Apps	WordPress, Joomla	AWS Marketplace	Quick setup	Paid

🧠 You’ll Learn
By completing this project, you’ll understand:

How to host a static site using Amazon S3

How to add HTTPS and CDN using CloudFront

AWS permissions, policies, and website configurations

The difference between various AWS hosting options

📦 Final Architecture Diagram
sql
Copy code
      +--------------------+
      |     CloudFront     |
      |  (CDN + HTTPS)     |
      +---------+----------+
                |
                ↓
      +--------------------+
      |       S3 Bucket    |
      |  (Static Website)  |
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
