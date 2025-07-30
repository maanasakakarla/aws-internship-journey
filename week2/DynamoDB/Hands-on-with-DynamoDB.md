
# 🗂️ DynamoDB Hands-on Guide

## 📁 Step 1: Create a DynamoDB Table - **Products**

**AWS Console Navigation**:  
`Services > Databases > DynamoDB > Create table`

- **Table Name**: `Products`
- **Partition Key**: `ProductID` (Type: String)
- **Sort Key**: *(Optional, not used here)*
- **Default Settings**: ✅ (Leave as is)
- **Tags**: *(Optional)*

⏱️ **Monitor Creation**:  
Watch the status transition from `Creating` → `Active`.

---

## 📥 Step 2: Insert Items (Data) into the Products Table

**Path**:  
Select `Products` table → Click on `Explore Table Items` → `Create item`

### ✅ JSON Example 1

```json
{
  "ProductID": "P001",
  "ProductName": "Laptop",
  "Price": 1200,
  "InStock": true,
  "ColorsAvailable": ["Silver", "Black"],
  "Specifications": {
    "CPU": "Intel i7",
    "RAM": "16GB",
    "Storage": "512GB SSD"
  }
}
```

### ✅ JSON Example 2

```json
{
  "ProductID": "P002",
  "ProductName": "Wireless Mouse",
  "Price": 25,
  "Connectivity": "Bluetooth",
  "BatteryLifeHours": 50
}
```

---

## 🔍 Step 3: Querying the Table

**Retrieve by Partition Key**:
- **Partition key**: `ProductID`
- **Value**: `P001`
- Click **Run**

---

## 📁 Step 4: Create a Table with Sort Key - **OrderItems**

### Table Information:
- **Table Name**: `OrderItems`
- **Partition Key**: `OrderID` (String)
- **Sort Key**: `SK` (String)

After creation, go to `OrderItems` → `Explore Table Items` → `Create item`

### 📝 Insert Items

#### JSON 1

```json
{
  "OrderID": "ORD#123",
  "SK": "PRODUCT#A101",
  "ProductName": "Laptop Bag",
  "Quantity": 1,
  "Price": 50.00,
  "ItemStatus": "Shipped"
}
```

#### JSON 2

```json
{
  "OrderID": "ORD#123",
  "SK": "PRODUCT#B202",
  "ProductName": "Wireless Earbuds",
  "Quantity": 2,
  "Price": 75.00,
  "ItemStatus": "Processing"
}
```

#### JSON 3

```json
{
  "OrderID": "ORD#123",
  "SK": "PRODUCT#C303",
  "ProductName": "USB-C Hub",
  "Quantity": 1,
  "Price": 30.00,
  "ItemStatus": "Shipped"
}
```

#### JSON 4

```json
{
  "OrderID": "ORD#456",
  "SK": "PRODUCT#D404",
  "ProductName": "Monitor Stand",
  "Quantity": 1,
  "Price": 45.00,
  "ItemStatus": "Delivered"
}
```

---

## 🔍 Step 5: Querying with Partition and Sort Key

### ✅ Query 1: Get all items for a specific OrderID

- **Partition key**: `OrderID` = `ORD#123`
- **Sort Key**: *(Leave blank)*
- Click **Run**

**Result**: All three items belonging to `ORD#123`, sorted by SK (lexicographically)

---

### ✅ Query 2: Get a specific item

- **Partition key**: `OrderID` = `ORD#123`
- **Sort key condition**: `=`  
- **Value**: `PRODUCT#A101`
- Click **Run**

**Result**: Only "Laptop Bag" item (PRODUCT#A101)

---

### ✅ Query 3: Items with SK beginning with prefix

- **Partition key**: `OrderID` = `ORD#123`
- **Sort key condition**: `begins_with`
- **Value**: `PRODUCT#`
- Click **Run**

**Result**: All items for `ORD#123` (prefix match)

---

### ✅ Query 4: Items within a Sort Key range

- **Partition key**: `OrderID` = `ORD#123`
- **Sort key condition**: `between`
- **Value 1**: `PRODUCT#A101`
- **Value 2**: `PRODUCT#B999`
- Click **Run**

**Result**: "Laptop Bag" (PRODUCT#A101) and "Wireless Earbuds" (PRODUCT#B202)

---

✅ You now understand how to:
- Create tables with and without sort keys.
- Insert data using JSON.
- Query effectively using partition key and sort key conditions.
