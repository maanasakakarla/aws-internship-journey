# 🗃️ S3 - Simple Storage Service

## Getting Started with Amazon S3

There are three primary ways to interact with S3:

1. **AWS Management Console**
2. **Command Line Interface (CLI)**
3. **AWS SDK**

> We'll start with the **AWS Management Console**. To proceed, you need an **IAM account** with S3 access permissions.

---

## 🛠️ Task 1: Creating an S3 Bucket

**Steps:**

- Go to **Services → Storage → S3 → Create bucket**

### ⚙️ Bucket Configuration:

- **Bucket Name**: Must be globally unique, in lowercase, 3–63 characters long. Can include lowercase letters, numbers, and hyphens.  
  _Example_: `my-first-s3-bucket-unique`

- **Object Ownership**:  
  - Use **ACLs Disabled (recommended)** for simplicity and better security.  
  - Use **ACLs Enabled** when multiple AWS accounts are uploading to the same bucket.

> **Access Control Lists (ACLs)** define specific permissions for individual S3 buckets and objects.

- **Block Public Access Settings**:  
  - Enable this to **prevent public access** (recommended for private data).
  - Disable if hosting public content like websites or static assets.

- **Bucket Versioning**:  
  - When **enabled**, uploading the same object multiple times creates **multiple versions** with unique keys.
  - When **disabled**, uploading the same object **overwrites** the previous one.

- **Tags**:  
  - Useful for organizing and searching buckets.
  - Can help with **cost tracking**, **automation**, and **scripting**.
  - Example use case: Start/stop or backup/delete resources based on tags.

---

## 📤 Uploading Files

1. Click the bucket name you just created.
2. Click **Upload → Add files/folders → Upload**.

---

## 🧰 Basic Operations on Uploaded Files

- View **Key**, **S3 URI**, **Object URL**
- **Download** the object
- **Delete** the object

---

## 🗑️ Deleting an S3 Bucket

> You **cannot delete** a bucket unless it's **empty**.

Steps:
1. Delete all the objects in the bucket.
2. Then, delete the bucket itself.

---
