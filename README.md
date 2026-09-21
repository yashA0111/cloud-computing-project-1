# AWS S3 Static Website — Project 1

## Live Website

**S3 Website URL:**  
http://yash-cloud-computing-project-1-aws-s3.s3-website-us-east-1.amazonaws.com

## GitHub Repository
https://github.com/yashA0111/cloud-computing-project-1


---

## Project Objective

Host a static portfolio website using **Amazon S3 Static Website Hosting** without provisioning a server.

The website source is maintained in GitHub, while the generated static files are uploaded to an Amazon S3 bucket.

---

## Deployment Procedure

### 1. Build the website

From the project directory:

```bash
npm install
npm run build
```

The production-ready static files are generated in:

```text
dist/
```

### 2. Create the S3 bucket

In the AWS S3 console:

**S3 → Create bucket**

Create a globally unique bucket name.

### 3. Upload the website

Upload the **contents of `dist/`** to the root of the S3 bucket.

The bucket should contain:

```text
index.html
404.html
_astro/
```

Do not upload the enclosing `dist/` directory itself.

### 4. Enable Static Website Hosting

Open:

**S3 Bucket → Properties → Static website hosting**

Enable:

**Host a static website**

Set:

```text
Index document: index.html
Error document: 404.html
```

### 5. Configure public access

For the website to be publicly accessible through the S3 website endpoint, configure the bucket for public object reads as required by the assignment.

Under:

**Permissions → Block public access**

disable **Block all public access** for this website bucket and acknowledge the warning.

### 6. Add the bucket policy

Under:

**Permissions → Bucket policy**

add a public-read policy for the website objects, replacing `YOUR-BUCKET-NAME` with the actual bucket name:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadForStaticWebsite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

### 7. Access the deployed website

Return to:

**Properties → Static website hosting**

Open the displayed **S3 website endpoint**.

That URL is the live website URL submitted for the project.

---

## Deployment Flow

```text
GitHub source
     ↓
npm run build
     ↓
dist/
     ↓
Upload static files to S3
     ↓
Enable Static Website Hosting
     ↓
Configure public object access
     ↓
S3 Website Endpoint
```

## Task Outcome

The completed project provides:

- a static portfolio website
- an Amazon S3 bucket containing the website files
- Static Website Hosting enabled
- public access configured for the website
- a live, shareable S3 website URL
