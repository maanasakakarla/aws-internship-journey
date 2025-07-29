# ⚙️ AWS Lambda - Serverless Function Documentation

## 📌 What is AWS Lambda?

**AWS Lambda** is a **serverless** compute service that lets you run code without provisioning or managing servers. Simply upload your code, and Lambda takes care of everything required to run and scale it.

---

## ✅ Benefits of AWS Lambda

- **No Server Management**: No need to provision or maintain servers.
- **Pay-per-Execution**: You are billed only for the time your code runs.
- **Automatic Scaling**: Scales automatically depending on the number of requests.

---

## 🔑 Key Features of Lambda Functions

| Feature                  | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| Environmental Variables  | Store configuration values outside your code (e.g., keys, default values). |
| Versions                 | Maintain multiple versions of your Lambda function.                         |
| Layers                   | Share common dependencies across multiple functions.                        |
| Code Signing             | Ensure that only trusted code is deployed and run.                          |

---

## 🛠️ Task: Creating a Lambda Function

### Step-by-Step Instructions:

1. Navigate to:  
   `AWS Console > Services > Compute > Lambda > Create Function`

2. **Create Function**:  
   - Choose: **Author from scratch**

3. **Basic Information**:  
   - **Function Name**: `myFunctionName`  
   - **Runtime**: Select the latest version of Python (e.g., Python 3.13)  
   - **Architecture**: `x86_64` (default)  
   - **Permissions**:  
     - Select **"Create a new role with basic Lambda permissions"**  
     - *(For advanced use, create a custom IAM policy and select "Use an existing role")*

4. Click **Create Function**

---

## 🧠 Add Lambda Code

Once the function is created, a code editor appears. Replace the existing code with the following:

```python
import os
import json

def lambda_handler(event, context):
    """
    Greets a user. The name can be provided in the event or retrieved
    from an environment variable.

    Args:
        event (dict): Event data (e.g., {"name": "User Name"})
        context (object): Lambda context (not used here)

    Returns:
        dict: Greeting message and status code
    """
    name = event.get('name')

    if not name:
        name = os.environ.get('DEFAULT_GREETING_NAME', 'Guest')
        print(f"Name not found in event. Using name from environment variable: {name}")
    else:
        print(f"Using name from event: {name}")

    greeting_message = f"Hello, {name}! Welcome to your Lambda function."

    return {
        'statusCode': 200,
        'body': json.dumps(greeting_message)
    }
