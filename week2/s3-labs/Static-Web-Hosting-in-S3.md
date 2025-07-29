# 🚀 Make an S3 Bucket Publicly Accessible (Static Website Hosting)

We’ll demonstrate hosting a static website on Amazon S3 using two HTML files stored locally:

- `index.html`
- `error.html`

---

## 📁 Step 1: Prepare Your HTML Files

### `index.html`
```html
<!DOCTYPE html>
<html>
<head>
    <title>My S3 Static Website</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; background-color: #f4f4f4; }
        h1 { color: #333; }
        p { color: #666; }
        a { color: #007bff; text-decoration: none; }
        a:hover { text-decoration: underline; }
    </style>
</head>
<body>
    <h1>Welcome to My Static Website on S3!</h1>
    <p>This is my main page, served directly from an Amazon S3 bucket.</p>
    <p>Current time in Hyderabad, India: <strong>July 29, 2025 at 1:17:55 PM IST</strong></p>
    <p>Try visiting a <a href="non-existent-page.html">non-existent page</a> to see the custom error page.</p>
</body>
</html>
```

---

### `error.html`
```html
<!DOCTYPE html>
<html>
<head>
    <title>Error! Page Not Found</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; background-color: #f8d7da; color: #721c24; }
        h1 { color: #721c24; }
        p { color: #721c24; }
        a { color: #007bff; text-decoration: none; }
        a:hover { text-decoration: underline; }
    </style>
</head>
<body>
    <h1>404 - Page Not Found</h1>
    <p>Oops! The page you requested could not be found.</p>
    <p>Please check the URL or <a href="index.html">go back to the homepage</a>.</p>
</body>
</html>
```

---

## ☁️ Step 2: Create and Configure the S3 Bucket

### ✅ Create the Bucket
- Go to **S3 Console**.
- Click **Create Bucket**.
- Provide a **unique bucket name**.
- **Uncheck**: `Block all public access`.

> ⚠️ Important: If block public access is enabled, your site won't be publicly accessible.

---

## 📤 Step 3: Upload HTML Files
- Open the newly created bucket.
- Click **Upload**, add `index.html` and `error.html`, and upload them.

---

## 🔐 Step 4: Set Bucket Policy for Public Access

### Navigate to the **Permissions** tab:
1. Ensure **"Block all public access" is turned OFF**.
2. Attach the following **bucket policy**:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::your-s3-bucket-name/*"
        }
    ]
}
```

> 🔁 Replace `your-s3-bucket-name` with your actual bucket name.

---

## ⚙️ Step 5: Enable Static Website Hosting

1. Go to the **Properties** tab.
2. Scroll down to **Static Website Hosting**.
3. Click **Edit**.
4. Enable **Static Website Hosting**.
5. Set:
   - **Index document**: `index.html`
   - **Error document**: `error.html` (optional but recommended)
6. Save changes.

---

## 🌐 Step 6: Access the Website

After saving, you'll see a **"Bucket website endpoint"** URL.

> Click that URL to view your hosted website!

---

### ✅ Done!

You’ve successfully hosted a static website using S3 with public access and a custom error page 🎉
