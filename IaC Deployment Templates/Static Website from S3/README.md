# Static Website on S3 – CloudFormation Template

This CloudFormation template provisions an AWS S3 bucket configured to host a static website. It includes versioning, server-side encryption, public read access, and a website configuration block for index and error pages.

---

## What It Does

- Creates an **S3 bucket** with:
  - Static website hosting enabled
  - Versioning and AES-256 encryption
  - Bucket ownership and public access settings configured
- Applies a **Bucket Policy** to allow public read access
- Outputs the **website endpoint URL** after deployment

---

## Tech Stack

- **Service:** AWS S3  
- **Tool:** AWS CloudFormation (YAML)  
- **Security:** Public access (for website use), encrypted at rest (AES256)

---

## Parameters

| Name         | Type   | Description                                                                 |
|--------------|--------|-----------------------------------------------------------------------------|
| `BucketName` | String | Name of the S3 bucket (must be globally unique and follow S3 naming rules)  |

---

## Output
After deployment, CloudFormation will return the public WebsiteURL where your static site can be accessed.


##  Notes
- Make sure to upload your index.html and error.html files to the bucket manually after deployment.
- This setup assumes public access is acceptable (e.g., personal or marketing websites). For restricted content, adjust the bucket policy accordingly.

## Example Use Cases
- Personal portfolio websites
- Landing pages
- Documentation hubs
- Static single-page apps