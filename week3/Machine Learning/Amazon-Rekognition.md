# 🧠 Amazon Rekognition - Computer Vision Service

Amazon Rekognition is a **Computer Vision (CV)** service that can **analyze images and videos** to detect **objects, people, text, and activities** using **pre-trained deep learning models**.

---

## 🚀 Getting Started

**Navigation Path:**  
`Home > Machine Learning (Services) > Amazon Rekognition`  
_(This is a pre-built service, so there is no need to write any code.)_

---

## 📌 Project 1: Detect Labels in an Image 🖼️

This project demonstrates how Rekognition identifies **objects, scenes, and concepts** in an image.

### 🔹 Step-by-Step Instructions:

1. **Choose an Image**:  
   Have an image ready on your computer to upload. A picture of a **city street**, **park**, or **living room** works well.

2. **Navigate to "Detect labels"**:  
   In the Rekognition console, select **"Detect labels"** from the left-hand menu.

3. **Upload the Image**:  
   Click **"Upload"** or drag and drop your image into the console.

4. **View the Results**:  
   Rekognition will **immediately process the image** and display the results on the right side of the screen.  
   You'll see a list of **labels** (e.g., `Car`, `Building`, `Tree`), each with a **confidence score** indicating how certain the model is about its prediction.

---

## 🧾 My Observations

### 🟥 Case 1: STOP Sign/Symbol Image

**Results:**

| Label         | Confidence Score |
|---------------|------------------|
| **Symbol**     | 98.2%            |
| **Sign**       | 98.1%            |
| **Utility Pole** | 95.9%          |
| **Road Sign**  | 67.9%            |
| **City**       | 57%              |
| **Urban**      | 56.2%            |

🔍 Rekognition effectively identified **multiple related labels**, even distinguishing between **'Sign'**, **'Road Sign'**, and **'Utility Pole'**.

---

### 🚦 Case 2: Traffic Image with Cars and Vehicles

**Results:**

| Label           | Confidence Score |
|------------------|------------------|
| **Road**          | 100%             |
| **Transportation**| 99.3%            |
| **Truck**         | 99.3%            |
| **Vehicle**       | 99.3%            |
| **Car**           | 99.3%            |
| **Person**        | 98.4%            |

💡 Rekognition is capable of detecting **people inside the vehicles** as well, indicating **fine-grained object detection**.

---

### 🖱️ Hover Feature

You can **hover over individual parts of the image** in the Rekognition console to **view bounding boxes and labels for each detected object**, making it easy to visualize what the model has identified.

---

## 🧪 Project 2: Image Properties

This project demonstrates how **Amazon Rekognition** analyzes the **visual properties of an image**, such as **dominant colors** and **quality metrics** like **brightness, sharpness, and contrast**.

I uploaded the **same STOP sign image** as in Project 1.

---

### 🌄 Full Image Properties

#### 🎨 Dominant Colors:

| Color Code | RGB Value         | Percentage |
|------------|-------------------|------------|
| `#000000`  | RGB(0, 0, 0)       | 20.66%     |
| `#dcdcdc`  | RGB(220, 220, 220) | 20.66%     |
| `#a9a9a9`  | RGB(169, 169, 169) | 18.18%     |
| `#808080`  | RGB(128, 128, 128) | 16.19%     |
| `#2f4f4f`  | RGB(47, 79, 79)    | 11.91%     |

#### 📷 Image Quality:

- **Brightness**: `79.11`
- **Sharpness**: `88.44`
- **Contrast**: `91.42`

---

### 👤 Foreground Properties

#### 🎨 Dominant Colors:

| Color Code | RGB Value         | Percentage |
|------------|-------------------|------------|
| `#800000`  | RGB(128, 0, 0)     | 55.56%     |
| `#a9a9a9`  | RGB(169, 169, 169) | 16.16%     |
| `#696969`  | RGB(105, 105, 105) | 9.09%      |
| `#483d8b`  | RGB(72, 61, 139)   | 7.07%      |
| `#bc8f8f`  | RGB(188, 143, 143) | 7.07%      |

#### 📷 Image Quality:

- **Brightness**: `54.64`
- **Sharpness**: `94.76`

---

### 🌆 Background Properties

#### 🎨 Dominant Colors:

| Color Code | RGB Value         | Percentage |
|------------|-------------------|------------|
| `#dcdcdc`  | RGB(220, 220, 220) | 22.10%     |
| `#a9a9a9`  | RGB(169, 169, 169) | 17.84%     |
| `#2f4f4f`  | RGB(47, 79, 79)    | 17.71%     |
| `#808080`  | RGB(128, 128, 128) | 17.24%     |
| `#000000`  | RGB(0, 0, 0)       | 16.91%     |

#### 📷 Image Quality:

- **Brightness**: `80.23`
- **Sharpness**: `87.85`

---

## 🧠 Key Takeaways:

- Rekognition provides **separate analysis** for the **entire image**, **foreground**, and **background**.
- It returns **dominant colors** with percentages to help understand visual distribution.
- Quality attributes like **brightness, sharpness, and contrast** help assess **image clarity and usability** for further AI/ML tasks.

---

## 👤 Project 3: Facial Analysis

In this project, Amazon Rekognition performs **facial analysis** to detect various facial attributes such as **emotion, age range, gender, facial features**, and **accessories**.

---

### 📷 Test 1: Face Image with Expression

I uploaded an image containing a **face with an expression**, and the following results were returned:

| Attribute                 | Result                        |
|---------------------------|-------------------------------|
| **Face Detected**         | ✅ 99.9% (Looks like a face)   |
| **Gender**                | Female – 99.6%                |
| **Estimated Age Range**   | 13 - 19 years old             |
| **Smiling**               | ❌ Not smiling – 98.8%         |
| **Emotion**               | Fear – 97.4%                  |
| **Wearing Glasses**       | ❌ Not wearing – 99.9%         |
| **Wearing Sunglasses**    | ❌ Not wearing – 99.9%         |
| **Eyes**                  | Closed – 87.1%                |
| **Mouth**                 | Open – 59.7%                  |
| **Mustache**              | ❌ No mustache – 98.2%         |
| **Beard**                 | ❌ No beard – 88.6%            |
| **Face Occlusion**        | ❌ Face not occluded – 99.6%   |

---

### 📷 Test 2: Image Without Any Face

When I uploaded an image **with no human face**, the result was:

> ❌ **No faces detected**

Rekognition accurately identifies the **absence of facial features**, ensuring minimal false positives.

---

### 👥 Test 3: Image With Multiple Faces

When uploading an image containing **multiple faces**, Rekognition provided a very **interesting feature**:

- It **analyzes each face individually**.
- You can **click on each detected face** in the image, and Rekognition displays the **detailed facial attributes** for that **specific face**.

This shows how Rekognition can be used in **group scenarios**, such as:
- Crowd analysis  
- Group photo insights  
- Public surveillance tools  
- Emotion detection in teams

---

## 🔍 Key Takeaways:

- Amazon Rekognition can **precisely detect facial attributes** even in crowded or expressive photos.
- Supports analysis for:
  - **Gender**
  - **Age range**
  - **Emotions**
  - **Facial hair**
  - **Eye and mouth state**
  - **Glasses/sunglasses**
- Provides **face-by-face analysis** for images with multiple people.

This project demonstrates Rekognition’s potential for applications in **emotion detection**, **demographic analysis**, and **real-time surveillance systems**.

---
## 🧑‍🤝‍🧑 Project 4: Face Comparison

In this project, **Amazon Rekognition** compares a **reference face** with one or more **target faces** to determine how similar they are.

---

### 📝 How It Works:

1. **Upload a Reference Image**:  
   This image contains the **face you want to compare against**.

2. **Upload Comparison Images**:  
   These are the images that will be **compared with the reference face**.

3. **Rekognition Analysis**:  
   Rekognition compares the faces and displays a **similarity score (in percentage)** to indicate how closely the faces match.

---

### 🧪 My Experiment:

- I uploaded a **real person's image as the reference**.
- Then I uploaded **various comparison images**, including:
  - A normal photo of the same person
  - An **animated/cartoon version** of the person

#### 📊 Sample Results:

- **Same person (real image)**:  
  ✅ Similarity score: `99.9%`  
  _(Very high match)_

- **Animated version of the same person**:  
  ❌ **No significant match**  
  _(Rekognition did not identify it as the same person)_

---

### ⚠️ Observation:

Rekognition is **highly accurate with real-life images**, but:
- It **does not work well with animated, cartoon, or stylized images**.
- This is likely because the **facial features in animated images** are **too abstract or exaggerated** to match real human features.

---

## ✅ Key Takeaways:

- Face Comparison is useful for:
  - **Identity verification**
  - **Authentication systems**
  - **Photo de-duplication**
- Works best with **clear, real-life human photos**.
- May not perform well with **artistic or animated versions** of faces.

---
## 🛡️ Project 5: Face Liveness Detection

**Face Liveness** detection is a security feature in Amazon Rekognition that checks whether a user being verified is **physically present in front of the camera**, rather than using a **spoof attempt** like:

- A printed photo  
- A digital image  
- A video replay  
- A deepfake animation

---

### 🧠 Purpose:

The goal is to **prevent identity fraud** in scenarios such as:

- **Online KYC verification**
- **Biometric authentication**
- **Access control systems**
- **Onboarding processes**

---

### 🔍 How It Works:

1. The user is prompted to **record a short selfie video**.
2. Amazon Rekognition analyzes the video to determine:
   - **Real human presence**
   - **Natural head movements**
   - **Blinking, eye movement, or subtle facial dynamics**
3. It returns a **liveness score** (Pass/Fail) based on whether the face is **genuine** or **spoofed**.

---

### ✅ Key Features:

- Protects against **spoofing attacks**
- Uses **deep learning** models for video-based analysis
- Provides **real-time feedback** during verification
- **No additional hardware** is required — just a camera

---

### ⚠️ Notes:

- Works only with **video input**, not still images  
- Requires **good lighting and clear visibility** of the user's face  
- Best used in **high-security environments**

---

## 🧾 Summary:

Amazon Rekognition's **Face Liveness Detection** enhances facial verification systems by ensuring the person in front of the camera is **alive and real**, helping to build **trust and security** in identity-based applications.

---

## 🌟 Project 6: Celebrity Recognition

**Amazon Rekognition** offers a powerful feature to automatically detect and recognize **celebrities** in images and videos. This project demonstrates how the service can match faces in media against a database of well-known personalities.

---

### 🧠 Purpose:

Celebrity recognition is useful for applications like:

- **Media and entertainment** tagging
- **News content indexing**
- **Event coverage and metadata extraction**
- **Social media analysis**

---

### 🔍 How It Works:

1. Upload an **image or video** containing **one or more faces**.
2. Rekognition compares the detected faces against its **pre-trained celebrity database**.
3. If a match is found, it provides:
   - **Celebrity name**
   - **Confidence score**
   - A **link to more information** (e.g., IMDb profile)

---

### 🧪 My Experiment:

- I uploaded an image of a **well-known celebrity**.
- Rekognition returned results like:

| Attribute         | Result                     |
|-------------------|----------------------------|
| **Celebrity Name** | Emma Watson                |
| **Match Confidence** | 99.8%                   |
| **Info Link**      | [IMDb Profile](https://www.imdb.com) |

- When an image does **not contain a celebrity**, Rekognition simply returns:
  > ❌ **No celebrities recognized**

---

### ✅ Key Features:

- Recognizes thousands of **internationally known public figures**
- Returns **detailed metadata**, including links to external databases
- Supports **both images and videos**

---

### ⚠️ Limitations:

- Only works for **well-known celebrities** listed in Rekognition's celebrity database.
- Does **not recognize local or lesser-known personalities**.
- Requires **clear, high-quality images** for accurate results.

---

## 🧾 Summary:

Amazon Rekognition's **Celebrity Recognition** feature is ideal for identifying popular public figures in images and videos. It's especially useful in the **media industry**, where automated tagging and metadata generation are crucial for organizing and distributing content efficiently.

---

## 📝 Project 7: Text in Image (Text Detection)

**Amazon Rekognition** can detect and extract **text from images**, specifically **printed English text**. This project demonstrates how the service identifies and returns **individual words, lines, or blocks of text** from uploaded images.

---

### 🧠 Purpose:

This feature is useful in applications like:

- **Document processing**
- **License plate detection**
- **Reading signs in images**
- **Text-based filtering and indexing**

---

### 🔍 How It Works:

1. Upload an image that contains visible **English text**.
2. Rekognition analyzes the image and returns:
   - **Detected text strings**
   - **Confidence scores**
   - **Bounding boxes** showing where each piece of text appears

---

### 🧪 My Experiment:

I uploaded an image containing printed text like **STOP**, **CAUTION**, and **SPEED LIMIT**, and Rekognition returned results such as:

| Detected Text  | Confidence Score |
|----------------|------------------|
| **STOP**       | 99.9%            |
| **SPEED LIMIT**| 98.7%            |
| **CAUTION**    | 97.4%            |

You can hover over each detected word/line in the console to see its exact position in the image.

---

### 🔤 Text Types Detected:

- ✅ **Printed English text**
- ❌ **Other languages are not supported**
- ❌ **Handwritten text** is not reliably detected
- ✅ **Numbers, symbols, and alphanumeric strings** (in English context)

---

### ✅ Key Features:

- Extracts text from **natural scenes and signs**
- Returns **line-wise** and **word-wise** results
- Provides **bounding box coordinates** for layout understanding

---

### ⚠️ Limitations:

- Only **English** is supported for text detection
- Detection quality drops in:
  - Blurry or low-resolution images
  - Highly stylized or decorative fonts
  - Overlapping or obstructed text

---

## 🧾 Summary:

Amazon Rekognition's **Text in Image** detection is best suited for applications that involve **printed English text**. It's ideal for building lightweight OCR systems, signage readers, or indexing tools — but it currently lacks support for **multi-language or handwritten text detection**.

---
