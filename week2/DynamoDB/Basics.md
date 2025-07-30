# Amazon DynamoDB Overview

Amazon **DynamoDB** is a **serverless**, **NoSQL**, and **fully managed** database service that provides **single-digit millisecond performance** at any scale. It is designed to store **structured data** in **key-value format**, typically represented as a JSON object.

---

## 🔑 Key Features

- **Serverless**: No infrastructure management.
- **Key-Value Store**: Schema-less and flexible data model.
- **ACID Transactions**: Ensures Atomicity, Consistency, Isolation, and Durability.
- **Indexing Support**: Enables flexible and optimized queries.
- **Continuous Backup**: On-demand and point-in-time recovery (PITR) supported.

---

## 🧱 Key Concepts

### Primary Keys

Each item in DynamoDB is uniquely identified by a **Primary Key**. Two types:

1. **Simple Primary Key**  
   - Only a **Partition Key** (Hash Key).
   - Uniquely identifies items.

2. **Composite Primary Key**  
   - **Partition Key** + **Sort Key** (Range Key).
   - Enables one-to-many relationships and range-based queries.

### Key Definitions

- **Partition Key (Hash Key)**: Determines the logical partition where the item is stored.
- **Sort Key (Range Key)**: Orders items within a partition and supports range queries.

---

## ⚙️ Capacity Modes

1. **On-Demand Mode**
   - Automatically scales throughput.
   - Pay-per-request billing.
   - Best for unpredictable workloads.

2. **Provisioned Mode**
   - Pre-allocated read/write capacity.
   - Suitable for predictable workloads and stable performance.

---

## 🧩 Core Components

- **Table**: Collection of items (like a table in SQL).
- **Item**: A single row or record.
- **Attribute**: A field in an item (schema-less, like a column).

---

## 🔍 Indexes (for flexible querying)

- **Local Secondary Index (LSI)**  
  - Same partition key, different sort key.
  - Must be defined at table creation.

- **Global Secondary Index (GSI)**  
  - Different partition and sort keys from the base table.
  - Can be added later.

---

## 🧠 Common Use Cases

- Real-time dashboards and analytics
- IoT device data storage
- Shopping carts and session tracking
- Mobile/web user profile storage
- Serverless application backends

---

## 🧬 Supported Data Types

- **Scalar**: String, Number, Boolean, Null, Binary
- **Document**: List, Map
- **Set**: String Set, Number Set, Binary Set

---

## 🧠 Best Practices

- Use **Query** instead of **Scan** to reduce latency and cost.
- Use **GSIs** and **LSIs** for flexible, high-performance queries.
- Use **BatchGetItem** and **BatchWriteItem** for bulk operations.
- Set **Time to Live (TTL)** to automatically delete stale data.
- Keep item size under 400 KB to avoid failures.

---

## 🚀 Advanced Features

- **DAX (DynamoDB Accelerator)**: In-memory caching for microsecond reads.
- **DynamoDB Streams**: Triggers AWS Lambda for real-time change processing.
- **TTL (Time to Live)**: Auto-expiration of items after a specified time.
- **Encryption at Rest**: Supports AWS-managed and customer-managed KMS keys.
- **Global Tables**: Multi-region replication for high availability.

---

## 💰 Pricing Overview

- **On-Demand Capacity Mode**:
  - Billed per read/write request units.
- **Provisioned Capacity Mode**:
  - Billed based on allocated Read/Write Capacity Units (RCUs/WCUs).
- **Additional Charges**:
  - Global Tables
  - Indexes (LSI, GSI)
  - Streams
  - Backups and restore
  - Data transfer out

---

## 🛠️ Key Operations

- **GetItem**: Retrieves a single item using its primary key.
- **Query**: Retrieves items that share the same partition key, with optional filters on sort key.
- **Scan**: Retrieves all items in a table or index (can be expensive for large datasets).

---
