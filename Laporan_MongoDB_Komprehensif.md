# LAPORAN MATERI PEMBELAJARAN
## DATABASE NoSQL - MongoDB & Integrasi dengan Aplikasi Web

---

**Disusun Oleh:**  
[Nama Mahasiswa]

**NIM:**  
[NIM]

**Mata Kuliah:**  
Pemrograman Web / Database Management

**Dosen Pengampu:**  
[Nama Dosen]

---

**Program Studi:**  
[Program Studi]

**Fakultas:**  
[Fakultas]

**Universitas:**  
[Nama Universitas]

---

**Tahun Akademik:**  
2026

---

<div style="page-break-after: always;"></div>

# DAFTAR ISI

## I. PENGENALAN DATABASE NoSQL
- 1.1 Definisi dan Konsep Dasar
- 1.2 Perbandingan SQL vs NoSQL
- 1.3 Kelebihan MongoDB
- 1.4 Kekurangan MongoDB
- 1.5 Karakteristik MongoDB

## II. INSTALASI & SETUP
- 2.1 Install MongoDB
- 2.2 Setup Node.js Environment
- 2.3 Konfigurasi Mongoose
- 2.4 Testing Connection

## III. INTEGRASI DENGAN NODE.JS
- 3.1 Koneksi MongoDB Driver
- 3.2 Koneksi dengan Mongoose
- 3.3 Schema & Model Definition
- 3.4 Middleware & Hooks

## IV. CRUD OPERATIONS
- 4.1 Create Operation
- 4.2 Read Operation
- 4.3 Update Operation
- 4.4 Delete Operation
- 4.5 Query Operators & Filtering

## V. ADVANCED TOPICS
- 5.1 Aggregation Pipeline
- 5.2 Indexing Strategies
- 5.3 Relationships & Population
- 5.4 Error Handling

## VI. BEST PRACTICES
- 6.1 Performance Optimization
- 6.2 Security Guidelines
- 6.3 Code Organization
- 6.4 Common Pitfalls

## VII. STUDI KASUS & PROJECT
- 7.1 Project Structure
- 7.2 Complete Example
- 7.3 Source Code

## VIII. SOAL & JAWABAN
- 8.1 Soal Konsep
- 8.2 Soal Praktik
- 8.3 Kunci Jawaban

## IX. TROUBLESHOOTING & FAQ
- 9.1 Common Errors
- 9.2 Solutions
- 9.3 FAQ

## X. REFERENSI & RESOURCES
- 10.1 Dokumentasi Official
- 10.2 Tools Recommendation
- 10.3 Learning Resources
- 10.4 Community Links

---

<div style="page-break-after: always;"></div>


# I. PENGENALAN DATABASE NoSQL

## 1.1 Definisi dan Konsep Dasar

### Apa itu NoSQL?

**NoSQL** (Not Only SQL) adalah paradigma database yang dirancang untuk menangani data dalam skala besar dengan struktur yang fleksibel. Berbeda dengan database relasional tradisional, NoSQL tidak menggunakan tabel dengan skema tetap, melainkan menggunakan berbagai model data seperti dokumen, key-value, graph, atau column-family.

### Sejarah Perkembangan NoSQL

**Timeline Perkembangan:**

```
1998 ─ Carlo Strozzi menciptakan istilah "NoSQL"
2000 ─ Graph database Neo4j mulai dikembangkan
2007 ─ Amazon merilis paper tentang Dynamo
2008 ─ Facebook mengembangkan Cassandra
2009 ─ MongoDB pertama kali dirilis sebagai open-source
2010 ─ Istilah "NoSQL" dipopulerkan untuk non-relational databases
2012 ─ MongoDB mencapai adopsi massal
2015+ ─ NoSQL menjadi standar untuk aplikasi modern
```

### Mengapa NoSQL Muncul?

NoSQL muncul sebagai solusi untuk mengatasi keterbatasan database relasional:

1. **Volume Data Besar** - Pertumbuhan data eksponensial dari web, mobile, IoT
2. **Velocity** - Kecepatan data yang masuk sangat tinggi (real-time)
3. **Variety** - Keragaman tipe data (structured, semi-structured, unstructured)
4. **Scalability** - Kebutuhan untuk scale horizontal dengan mudah
5. **Flexibility** - Perubahan struktur data yang cepat dalam development

### CAP Theorem

CAP Theorem adalah prinsip fundamental dalam sistem database terdistribusi yang menyatakan bahwa sistem hanya dapat memenuhi **maksimal 2 dari 3** properti berikut:

```
                 C (Consistency)
                       /\
                      /  \
                     /    \
                    /      \
                   /   CA   \
                  /  (RDBMS) \
                 /____________\
                /  CP      AP  \
               / (MongoDB)(Cassandra)
              /                  \
             A ─────────────────── P
        (Availability)    (Partition Tolerance)
```

**Penjelasan:**

- **Consistency (C)**: Semua node melihat data yang sama pada waktu yang sama
- **Availability (A)**: Setiap request mendapat response (sukses/gagal)
- **Partition Tolerance (P)**: Sistem tetap berfungsi meskipun ada network partition

**Kategori Database:**

- **CA**: MySQL, PostgreSQL - Tidak partition tolerant
- **CP**: MongoDB, HBase - Mungkin tidak available saat partition
- **AP**: Cassandra, DynamoDB - Eventually consistent

### Kapan Menggunakan NoSQL vs SQL?

**Gunakan NoSQL ketika:**

✅ Data tidak terstruktur atau semi-terstruktur  
✅ Skema data sering berubah  
✅ Perlu horizontal scaling  
✅ Performa read/write tinggi lebih penting dari konsistensi ketat  
✅ Bekerja dengan big data atau real-time analytics  
✅ Rapid development dan iterasi cepat  

**Gunakan SQL ketika:**

✅ Data terstruktur dengan relasi kompleks  
✅ Membutuhkan ACID transactions yang ketat  
✅ Query kompleks dengan JOIN banyak tabel  
✅ Data consistency adalah prioritas utama  
✅ Reporting dan analytics kompleks  
✅ Skema stabil dan well-defined  

---


## 1.2 Perbandingan SQL vs NoSQL

### Tabel Perbandingan Komprehensif

| Aspek | SQL (Relational) | NoSQL (Non-Relational) |
|-------|------------------|------------------------|
| **Model Data** | Tabel dengan baris dan kolom | Dokumen, Key-Value, Graph, Column-family |
| **Skema** | Fixed schema (rigid) | Dynamic schema (flexible) |
| **Skalabilitas** | Vertical scaling (scale-up) | Horizontal scaling (scale-out) |
| **Query Language** | SQL (Structured Query Language) | Berbeda per database |
| **Transaksi** | ACID compliant | BASE (Eventually consistent) |
| **Relasi Data** | Foreign keys, JOINs | Embedded documents, references |
| **Konsistensi** | Strong consistency | Eventual consistency |
| **Performa** | Baik untuk query kompleks | Sangat baik untuk operasi sederhana |
| **Use Case** | Banking, ERP, CRM | Social media, IoT, real-time analytics |
| **Contoh** | MySQL, PostgreSQL, Oracle | MongoDB, Cassandra, Redis, Neo4j |

### Perbandingan Struktur Data

**SQL - Relational Model:**

```sql
-- Tabel Users
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

-- Tabel Orders
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    product VARCHAR(100),
    quantity INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Query dengan JOIN
SELECT users.name, orders.product, orders.quantity
FROM users
JOIN orders ON users.id = orders.user_id
WHERE users.id = 1;
```

**NoSQL - Document Model (MongoDB):**

```javascript
// Collection: users
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John Doe",
  "email": "john@example.com",
  "orders": [
    {
      "product": "Laptop",
      "quantity": 1,
      "date": ISODate("2026-05-19")
    },
    {
      "product": "Mouse",
      "quantity": 2,
      "date": ISODate("2026-05-18")
    }
  ]
}

// Query tanpa JOIN
db.users.findOne({ "_id": ObjectId("507f1f77bcf86cd799439011") })
```

### Perbandingan Query Language

**SQL Query:**

```sql
-- SELECT dengan kondisi
SELECT * FROM users WHERE age > 25 AND city = 'Jakarta';

-- UPDATE
UPDATE users SET status = 'active' WHERE id = 1;

-- DELETE
DELETE FROM users WHERE last_login < '2025-01-01';

-- Aggregation
SELECT city, COUNT(*) as total, AVG(age) as avg_age
FROM users
GROUP BY city
HAVING COUNT(*) > 10;
```

**MongoDB Query:**

```javascript
// Find dengan kondisi
db.users.find({ age: { $gt: 25 }, city: "Jakarta" })

// Update
db.users.updateOne({ _id: 1 }, { $set: { status: "active" } })

// Delete
db.users.deleteMany({ last_login: { $lt: new Date("2025-01-01") } })

// Aggregation
db.users.aggregate([
  { $group: { _id: "$city", total: { $sum: 1 }, avg_age: { $avg: "$age" } }},
  { $match: { total: { $gt: 10 } } }
])
```

### Perbandingan Skalabilitas

**Vertical Scaling (SQL):**

```
┌────────────────────────────────────┐
│  Vertical Scaling (Scale-Up)       │
├────────────────────────────────────┤
│                                     │
│  Server 1 (Small)  →  Server 1 (Large)
│  ┌─────────┐          ┌─────────┐  │
│  │ 4 CPU   │          │ 32 CPU  │  │
│  │ 8 GB    │    →     │ 128 GB  │  │
│  │ 100 GB  │          │ 2 TB    │  │
│  └─────────┘          └─────────┘  │
│                                     │
│  Kelebihan:                         │
│  ✓ Sederhana                        │
│  ✓ Tidak perlu ubah aplikasi        │
│                                     │
│  Kekurangan:                        │
│  ✗ Ada limit hardware               │
│  ✗ Mahal                            │
│  ✗ Single point of failure          │
└────────────────────────────────────┘
```

**Horizontal Scaling (NoSQL):**

```
┌────────────────────────────────────┐
│  Horizontal Scaling (Scale-Out)    │
├────────────────────────────────────┤
│                                     │
│  Server 1    →    Server 1,2,3,4   │
│  ┌───────┐      ┌──┐┌──┐┌──┐┌──┐  │
│  │ 8 CPU │      │8 ││8 ││8 ││8 │  │
│  │ 16 GB │  →   │16││16││16││16│  │
│  │500 GB │      │500││500││500││500│ │
│  └───────┘      └──┘└──┘└──┘└──┘  │
│                                     │
│  Kelebihan:                         │
│  ✓ Tidak ada limit teoritis         │
│  ✓ Cost-effective                   │
│  ✓ High availability                │
│                                     │
│  Kekurangan:                        │
│  ✗ Kompleksitas lebih tinggi        │
│  ✗ Eventual consistency             │
└────────────────────────────────────┘
```

### ACID vs BASE

**ACID (SQL):**

- **Atomicity**: Transaksi all-or-nothing
- **Consistency**: Data selalu dalam state valid
- **Isolation**: Transaksi tidak saling mengganggu
- **Durability**: Data tersimpan permanen setelah commit

**BASE (NoSQL):**

- **Basically Available**: Sistem selalu merespons
- **Soft state**: State bisa berubah seiring waktu
- **Eventually consistent**: Konsistensi tercapai setelah beberapa waktu

### Use Case Comparison Matrix

| Skenario | SQL | NoSQL | Rekomendasi |
|----------|-----|-------|-------------|
| E-commerce Transactions | ✅ Excellent | ⚠️ Good | SQL (butuh ACID) |
| Product Catalog | ⚠️ Good | ✅ Excellent | NoSQL (flexible schema) |
| User Sessions | ❌ Poor | ✅ Excellent | NoSQL (key-value) |
| Financial Reports | ✅ Excellent | ⚠️ Good | SQL (complex queries) |
| Social Media Posts | ⚠️ Good | ✅ Excellent | NoSQL (high write) |
| Real-time Analytics | ❌ Poor | ✅ Excellent | NoSQL (speed) |
| Inventory Management | ✅ Excellent | ⚠️ Good | SQL (consistency) |
| IoT Sensor Data | ❌ Poor | ✅ Excellent | NoSQL (volume) |
| Content Management | ⚠️ Good | ✅ Excellent | NoSQL (flexibility) |
| Banking Transactions | ✅ Excellent | ❌ Poor | SQL (ACID critical) |

---


## 1.3 Kelebihan MongoDB

### 1. Fleksibilitas Schema

MongoDB menggunakan **dynamic schema** yang memungkinkan dokumen dalam collection yang sama memiliki struktur berbeda.

```javascript
// Dokumen 1 - User dengan alamat lengkap
{
  "_id": 1,
  "name": "Alice",
  "email": "alice@example.com",
  "address": {
    "street": "Jl. Sudirman",
    "city": "Jakarta",
    "zipcode": "12190"
  }
}

// Dokumen 2 - User tanpa alamat (tetap valid)
{
  "_id": 2,
  "name": "Bob",
  "email": "bob@example.com"
}
```

### 2. Performa Tinggi

- **Fast Read/Write**: Operasi CRUD sangat cepat
- **In-Memory Processing**: Working set disimpan di RAM
- **Indexing**: Mendukung berbagai jenis index (single, compound, geospatial, text)

### 3. Horizontal Scalability

MongoDB mendukung **sharding** untuk distribusi data across multiple servers:

```
┌─────────────────────────────────────────┐
│         MongoDB Sharded Cluster          │
├─────────────────────────────────────────┤
│                                          │
│  Client Application                      │
│         ↓                                │
│    mongos (Router)                       │
│         ↓                                │
│  ┌──────┴──────┬──────────┬──────────┐  │
│  ↓             ↓          ↓          ↓  │
│ Shard 1     Shard 2    Shard 3    Shard 4│
│ (Data A)    (Data B)   (Data C)   (Data D)│
│                                          │
└─────────────────────────────────────────┘
```

### 4. Rich Query Language

MongoDB mendukung query yang powerful:

```javascript
// Complex queries
db.products.find({
  price: { $gte: 100, $lte: 500 },
  category: { $in: ["Electronics", "Gadgets"] },
  "reviews.rating": { $gte: 4 }
})

// Aggregation pipeline
db.orders.aggregate([
  { $match: { status: "completed" } },
  { $group: { _id: "$customer_id", total: { $sum: "$amount" } }},
  { $sort: { total: -1 } },
  { $limit: 10 }
])
```

### 5. High Availability

**Replica Sets** menyediakan redundancy dan automatic failover:

```
┌─────────────────────────────────────┐
│        Replica Set                   │
├─────────────────────────────────────┤
│                                      │
│     Primary Node                     │
│     (Read/Write)                     │
│          ↓                           │
│    ┌─────┴─────┐                    │
│    ↓           ↓                    │
│ Secondary   Secondary                │
│ (Read Only) (Read Only)              │
│                                      │
│ Auto Failover jika Primary down      │
└─────────────────────────────────────┘
```

### 6. Document-Oriented

Data disimpan dalam format **BSON** (Binary JSON) yang natural untuk aplikasi:

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "title": "MongoDB Tutorial",
  "author": {
    "name": "John Doe",
    "email": "john@example.com"
  },
  "tags": ["database", "nosql", "mongodb"],
  "comments": [
    { "user": "Alice", "text": "Great article!", "date": ISODate("2026-05-19") },
    { "user": "Bob", "text": "Very helpful", "date": ISODate("2026-05-18") }
  ],
  "views": 1250,
  "published": true
}
```

---

## 1.4 Kekurangan MongoDB

### 1. Memory Usage Tinggi

MongoDB membutuhkan RAM yang besar untuk performa optimal:

- Working set harus fit di memory
- Indexing memakan banyak memory
- Tidak efisien untuk dataset yang sangat besar dengan RAM terbatas

**Solusi:**
- Gunakan sharding untuk distribusi data
- Optimize indexes
- Upgrade RAM server

### 2. JOIN Complexity

MongoDB tidak mendukung JOIN seperti SQL. Harus menggunakan:

**Embedding (Denormalization):**

```javascript
// Data digabung dalam satu dokumen
{
  "_id": 1,
  "user": "Alice",
  "orders": [
    { "product": "Laptop", "price": 1000 },
    { "product": "Mouse", "price": 20 }
  ]
}
```

**Referencing + Population:**

```javascript
// Data terpisah, perlu multiple queries
// Collection: users
{ "_id": 1, "name": "Alice" }

// Collection: orders
{ "_id": 101, "user_id": 1, "product": "Laptop" }

// Perlu 2 queries atau $lookup
```

### 3. Transaction Limitations

Sebelum MongoDB 4.0, tidak ada multi-document transactions:

- Single document operations adalah atomic
- Multi-document transactions ada overhead performa
- Tidak se-mature SQL transactions

### 4. Data Duplication

Denormalization menyebabkan data redundancy:

```javascript
// User data duplikat di setiap order
{
  "order_id": 1,
  "user": { "name": "Alice", "email": "alice@example.com" },
  "product": "Laptop"
}
{
  "order_id": 2,
  "user": { "name": "Alice", "email": "alice@example.com" },
  "product": "Mouse"
}
// Jika email Alice berubah, harus update semua dokumen
```

### 5. Storage Overhead

BSON format dan indexing membutuhkan storage lebih besar dibanding SQL.

### 6. Learning Curve

- Paradigma berbeda dari SQL
- Perlu memahami kapan embed vs reference
- Query syntax berbeda

---

## 1.5 Karakteristik MongoDB

### 1. Document-Oriented Database

MongoDB menyimpan data dalam bentuk **dokumen BSON** (Binary JSON):

**Struktur Dokumen:**

```javascript
{
  "_id": ObjectId("..."),           // Unique identifier
  "field1": "value",                // String
  "field2": 123,                    // Number
  "field3": true,                   // Boolean
  "field4": ISODate("2026-05-19"),  // Date
  "field5": ["array", "values"],    // Array
  "field6": {                       // Embedded document
    "nested": "object"
  },
  "field7": null                    // Null
}
```

**BSON vs JSON:**

| Aspek | JSON | BSON |
|-------|------|------|
| Format | Text-based | Binary |
| Size | Lebih besar | Lebih kecil |
| Speed | Slower parsing | Faster parsing |
| Data Types | Limited (string, number, boolean, null, array, object) | Extended (Date, ObjectId, Binary, Regex, etc) |
| Readability | Human-readable | Machine-readable |

### 2. Schema Flexibility

**Dynamic Schema** memungkinkan evolusi data tanpa migration:

```javascript
// Version 1 - Simple user
{
  "name": "Alice",
  "email": "alice@example.com"
}

// Version 2 - Add phone (tidak perlu ALTER TABLE)
{
  "name": "Bob",
  "email": "bob@example.com",
  "phone": "+62812345678"
}

// Version 3 - Add nested address
{
  "name": "Charlie",
  "email": "charlie@example.com",
  "phone": "+62812345679",
  "address": {
    "city": "Jakarta",
    "country": "Indonesia"
  }
}
```

### 3. Indexing Capabilities

MongoDB mendukung berbagai jenis index:

**Single Field Index:**

```javascript
db.users.createIndex({ email: 1 })  // Ascending
```

**Compound Index:**

```javascript
db.users.createIndex({ city: 1, age: -1 })  // city ASC, age DESC
```

**Multikey Index (Array):**

```javascript
db.products.createIndex({ tags: 1 })  // Index array elements
```

**Text Index:**

```javascript
db.articles.createIndex({ content: "text" })  // Full-text search
```

**Geospatial Index:**

```javascript
db.places.createIndex({ location: "2dsphere" })  // Geo queries
```

**Diagram Index:**

```
┌─────────────────────────────────────┐
│         Index Structure              │
├─────────────────────────────────────┤
│                                      │
│  Collection: users                   │
│  ┌────────────────────────────┐     │
│  │ _id  │ name   │ email      │     │
│  ├──────┼────────┼────────────┤     │
│  │ 1    │ Alice  │ a@ex.com   │     │
│  │ 2    │ Bob    │ b@ex.com   │     │
│  │ 3    │ Charlie│ c@ex.com   │     │
│  └────────────────────────────┘     │
│           ↓                          │
│  Index on email:                     │
│  ┌────────────────┬──────┐          │
│  │ a@ex.com       │  1   │          │
│  │ b@ex.com       │  2   │          │
│  │ c@ex.com       │  3   │          │
│  └────────────────┴──────┘          │
│  (Sorted untuk fast lookup)          │
└─────────────────────────────────────┘
```

### 4. Replication

**Replica Set** menyediakan data redundancy dan high availability:

**Arsitektur:**

```
┌──────────────────────────────────────────┐
│         Replica Set Architecture          │
├──────────────────────────────────────────┤
│                                           │
│           PRIMARY                         │
│      ┌──────────────┐                    │
│      │   Node 1     │                    │
│      │ (Read/Write) │                    │
│      └──────┬───────┘                    │
│             │                             │
│      Replication                          │
│             │                             │
│      ┌──────┴───────┐                    │
│      ↓              ↓                    │
│  SECONDARY      SECONDARY                 │
│ ┌──────────┐   ┌──────────┐             │
│ │  Node 2  │   │  Node 3  │             │
│ │(Read Only)│   │(Read Only)│             │
│ └──────────┘   └──────────┘             │
│                                           │
│ Automatic Failover:                       │
│ Jika Primary down, Secondary dipromosikan │
└──────────────────────────────────────────┘
```

**Keuntungan Replication:**

✅ **High Availability**: Automatic failover  
✅ **Data Redundancy**: Multiple copies  
✅ **Read Scalability**: Read dari secondary  
✅ **Disaster Recovery**: Backup otomatis  

### 5. Sharding

**Sharding** adalah metode distribusi data horizontal across multiple machines:

**Arsitektur Sharded Cluster:**

```
┌────────────────────────────────────────────┐
│       MongoDB Sharded Cluster               │
├────────────────────────────────────────────┤
│                                             │
│  Application                                │
│       ↓                                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐    │
│  │ mongos  │  │ mongos  │  │ mongos  │    │
│  │(Router) │  │(Router) │  │(Router) │    │
│  └────┬────┘  └────┬────┘  └────┬────┘    │
│       └────────────┼────────────┘          │
│                    ↓                        │
│         Config Servers (Metadata)           │
│              ┌──────────┐                   │
│              │ Config   │                   │
│              │ Replica  │                   │
│              │   Set    │                   │
│              └─────┬────┘                   │
│                    ↓                        │
│  ┌─────────┬──────┴──────┬─────────┐      │
│  ↓         ↓             ↓         ↓      │
│ Shard 1  Shard 2      Shard 3   Shard 4    │
│ (0-25%)  (26-50%)    (51-75%)  (76-100%)   │
│ Replica  Replica     Replica   Replica      │
│   Set      Set         Set       Set        │
│                                             │
└────────────────────────────────────────────┘
```

**Shard Key Strategy:**

```javascript
// Range-based sharding
sh.shardCollection("mydb.users", { user_id: 1 })

// Hash-based sharding (better distribution)
sh.shardCollection("mydb.users", { user_id: "hashed" })

// Compound shard key
sh.shardCollection("mydb.orders", { customer_id: 1, order_date: 1 })
```

**Keuntungan Sharding:**

✅ **Horizontal Scalability**: Tambah server untuk kapasitas  
✅ **Better Performance**: Parallel processing  
✅ **No Single Point of Failure**: Distributed system  

---

<div style="page-break-after: always;"></div>


# II. INSTALASI & SETUP

## 2.1 Install MongoDB

### Instalasi MongoDB di Windows

**Step 1: Download MongoDB**

1. Kunjungi https://www.mongodb.com/try/download/community
2. Pilih versi terbaru untuk Windows
3. Download file `.msi` installer

**Step 2: Install MongoDB**

```
1. Jalankan file .msi installer
2. Pilih "Complete" installation
3. Install MongoDB as a Service (recommended)
4. Install MongoDB Compass (GUI tool)
5. Klik "Install"
```

**Step 3: Verifikasi Instalasi**

```bash
# Buka Command Prompt
mongod --version

# Output:
# db version v7.0.0
# Build Info: ...
```

**Step 4: Jalankan MongoDB**

```bash
# MongoDB sudah running sebagai service
# Cek status:
net start MongoDB

# Akses MongoDB Shell:
mongosh

# Output:
# Current Mongosh Log ID: ...
# Connecting to: mongodb://127.0.0.1:27017
# test>
```

### Instalasi MongoDB di Linux (Ubuntu)

```bash
# Import public key
wget -qO - https://www.mongodb.org/static/pgp/server-7.0.asc | sudo apt-key add -

# Create list file
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# Update package database
sudo apt-get update

# Install MongoDB
sudo apt-get install -y mongodb-org

# Start MongoDB
sudo systemctl start mongod

# Enable auto-start
sudo systemctl enable mongod

# Verify
mongod --version
```

### Instalasi MongoDB di macOS

```bash
# Install menggunakan Homebrew
brew tap mongodb/brew
brew install mongodb-community@7.0

# Start MongoDB
brew services start mongodb-community@7.0

# Verify
mongod --version
```

### MongoDB Atlas (Cloud Database)

**Keuntungan MongoDB Atlas:**

✅ Fully managed (no server maintenance)  
✅ Free tier available (512MB storage)  
✅ Automatic backups  
✅ Global deployment  
✅ Built-in security  

**Setup MongoDB Atlas:**

**Step 1: Create Account**

1. Kunjungi https://www.mongodb.com/cloud/atlas
2. Sign up dengan email atau Google account
3. Verifikasi email

**Step 2: Create Cluster**

```
1. Klik "Build a Database"
2. Pilih "FREE" tier (M0 Sandbox)
3. Pilih Cloud Provider (AWS/GCP/Azure)
4. Pilih Region (Singapore untuk Indonesia)
5. Cluster Name: "MyFirstCluster"
6. Klik "Create Cluster"
```

**Step 3: Setup Database Access**

```
1. Database Access → Add New Database User
2. Username: admin
3. Password: [generate secure password]
4. Database User Privileges: Read and write to any database
5. Add User
```

**Step 4: Setup Network Access**

```
1. Network Access → Add IP Address
2. Pilih "Allow Access from Anywhere" (0.0.0.0/0)
   (Untuk development only, production gunakan specific IP)
3. Confirm
```

**Step 5: Get Connection String**

```
1. Clusters → Connect
2. Pilih "Connect your application"
3. Driver: Node.js
4. Version: 5.5 or later
5. Copy connection string:

mongodb+srv://admin:<password>@myfirstcluster.xxxxx.mongodb.net/?retryWrites=true&w=majority
```

---

## 2.2 Setup Node.js Environment

### Install Node.js

**Windows:**

```
1. Download dari https://nodejs.org/
2. Pilih LTS version
3. Jalankan installer
4. Ikuti wizard installation
```

**Verify Installation:**

```bash
node --version
# v20.11.0

npm --version
# 10.2.4
```

### Create Project

```bash
# Buat folder project
mkdir mongodb-project
cd mongodb-project

# Initialize npm
npm init -y

# Output: package.json created
```

**package.json:**

```json
{
  "name": "mongodb-project",
  "version": "1.0.0",
  "description": "MongoDB Integration Project",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
  "keywords": ["mongodb", "nodejs"],
  "author": "Your Name",
  "license": "ISC"
}
```

### Install Dependencies

```bash
# Install MongoDB driver
npm install mongodb

# Install Mongoose (ODM)
npm install mongoose

# Install dotenv (environment variables)
npm install dotenv

# Install nodemon (development)
npm install --save-dev nodemon
```

**package.json setelah install:**

```json
{
  "dependencies": {
    "dotenv": "^16.4.5",
    "mongodb": "^6.5.0",
    "mongoose": "^8.3.0"
  },
  "devDependencies": {
    "nodemon": "^3.1.0"
  }
}
```

### Setup Environment Variables

**Create .env file:**

```bash
# .env
MONGODB_URI=mongodb://localhost:27017/mydb
# atau untuk Atlas:
# MONGODB_URI=mongodb+srv://admin:password@cluster.xxxxx.mongodb.net/mydb

PORT=3000
NODE_ENV=development
```

**Create .gitignore:**

```
node_modules/
.env
*.log
```

### Project Structure

```
mongodb-project/
├── node_modules/
├── config/
│   └── database.js
├── models/
│   └── User.js
├── controllers/
│   └── userController.js
├── routes/
│   └── userRoutes.js
├── .env
├── .gitignore
├── package.json
└── index.js
```

---

## 2.3 Konfigurasi Mongoose

### Basic Connection

**config/database.js:**

```javascript
const mongoose = require('mongoose');
require('dotenv').config();

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGODB_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### Connection dengan Options

```javascript
const mongoose = require('mongoose');

const options = {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  serverSelectionTimeoutMS: 5000,
  socketTimeoutMS: 45000,
  family: 4, // Use IPv4
  maxPoolSize: 10, // Connection pool
  minPoolSize: 5,
  maxIdleTimeMS: 10000,
  retryWrites: true,
  w: 'majority'
};

mongoose.connect(process.env.MONGODB_URI, options)
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.error('MongoDB connection error:', err));
```

### Connection Events

```javascript
const mongoose = require('mongoose');

// Connection events
mongoose.connection.on('connected', () => {
  console.log('Mongoose connected to MongoDB');
});

mongoose.connection.on('error', (err) => {
  console.error('Mongoose connection error:', err);
});

mongoose.connection.on('disconnected', () => {
  console.log('Mongoose disconnected');
});

// Graceful shutdown
process.on('SIGINT', async () => {
  await mongoose.connection.close();
  console.log('Mongoose connection closed due to app termination');
  process.exit(0);
});
```

### Connection String Format

**Local MongoDB:**

```
mongodb://localhost:27017/database_name
mongodb://127.0.0.1:27017/database_name
```

**MongoDB dengan Authentication:**

```
mongodb://username:password@localhost:27017/database_name
```

**MongoDB Atlas:**

```
mongodb+srv://username:password@cluster.mongodb.net/database_name?retryWrites=true&w=majority
```

**Connection String Components:**

```
mongodb+srv://username:password@host:port/database?options

├── Protocol: mongodb:// atau mongodb+srv://
├── Credentials: username:password@
├── Host: cluster.mongodb.net
├── Port: :27017 (optional untuk srv)
├── Database: /database_name
└── Options: ?retryWrites=true&w=majority
```

---

## 2.4 Testing Connection

### Test Script

**test-connection.js:**

```javascript
const mongoose = require('mongoose');
require('dotenv').config();

const testConnection = async () => {
  try {
    console.log('Attempting to connect to MongoDB...');
    console.log('URI:', process.env.MONGODB_URI.replace(/\/\/.*@/, '//***:***@'));
    
    await mongoose.connect(process.env.MONGODB_URI);
    
    console.log('✅ MongoDB connection successful!');
    console.log('Database:', mongoose.connection.db.databaseName);
    console.log('Host:', mongoose.connection.host);
    console.log('Port:', mongoose.connection.port);
    
    // Test write operation
    const testCollection = mongoose.connection.collection('test');
    await testCollection.insertOne({ test: 'Hello MongoDB', timestamp: new Date() });
    console.log('✅ Write test successful!');
    
    // Test read operation
    const doc = await testCollection.findOne({ test: 'Hello MongoDB' });
    console.log('✅ Read test successful!');
    console.log('Document:', doc);
    
    // Cleanup
    await testCollection.deleteOne({ test: 'Hello MongoDB' });
    console.log('✅ Delete test successful!');
    
    await mongoose.connection.close();
    console.log('Connection closed');
    
  } catch (error) {
    console.error('❌ Connection failed:', error.message);
    process.exit(1);
  }
};

testConnection();
```

**Run test:**

```bash
node test-connection.js
```

**Expected Output:**

```
Attempting to connect to MongoDB...
URI: mongodb://***:***@localhost:27017/mydb
✅ MongoDB connection successful!
Database: mydb
Host: localhost
Port: 27017
✅ Write test successful!
✅ Read test successful!
Document: { _id: ..., test: 'Hello MongoDB', timestamp: 2026-05-19T... }
✅ Delete test successful!
Connection closed
```

### Main Application Setup

**index.js:**

```javascript
const express = require('express');
const connectDB = require('./config/database');
require('dotenv').config();

const app = express();

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Connect to MongoDB
connectDB();

// Routes
app.get('/', (req, res) => {
  res.json({ message: 'MongoDB API is running' });
});

// Health check
app.get('/health', (req, res) => {
  const dbState = ['disconnected', 'connected', 'connecting', 'disconnecting'];
  res.json({
    status: 'OK',
    database: dbState[mongoose.connection.readyState],
    timestamp: new Date()
  });
});

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Run application:**

```bash
npm start
# atau untuk development:
npm run dev
```

### Troubleshooting Connection Issues

**Common Errors:**

**1. MongoNetworkError: failed to connect**

```
Penyebab: MongoDB server tidak running
Solusi: 
- Cek apakah MongoDB service running
- Windows: net start MongoDB
- Linux: sudo systemctl start mongod
```

**2. MongoServerError: Authentication failed**

```
Penyebab: Username/password salah
Solusi:
- Cek credentials di .env
- Pastikan user sudah dibuat di database
```

**3. MongooseServerSelectionError: connect ECONNREFUSED**

```
Penyebab: Connection string salah atau firewall blocking
Solusi:
- Cek connection string format
- Cek firewall settings
- Untuk Atlas, cek Network Access whitelist
```

**4. MongoParseError: Invalid connection string**

```
Penyebab: Format connection string tidak valid
Solusi:
- Cek format: mongodb://host:port/database
- Encode special characters di password
```

**Debug Tips:**

```javascript
// Enable mongoose debug mode
mongoose.set('debug', true);

// Log all queries
mongoose.set('debug', (collectionName, method, query, doc) => {
  console.log(`${collectionName}.${method}`, JSON.stringify(query), doc);
});
```

---

<div style="page-break-after: always;"></div>


# III. INTEGRASI DENGAN NODE.JS

## 3.1 Koneksi MongoDB Driver

### Native MongoDB Driver

MongoDB menyediakan official driver untuk Node.js yang memberikan low-level access ke database.

**Install MongoDB Driver:**

```bash
npm install mongodb
```

### Basic Connection

**db.js:**

```javascript
const { MongoClient } = require('mongodb');

// Connection URI
const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri);

async function connect() {
  try {
    // Connect to MongoDB
    await client.connect();
    console.log('Connected to MongoDB');
    
    // Access database
    const database = client.db('mydb');
    
    // Access collection
    const collection = database.collection('users');
    
    return { database, collection };
  } catch (error) {
    console.error('Connection error:', error);
    throw error;
  }
}

module.exports = { connect, client };
```

### CRUD dengan Native Driver

```javascript
const { MongoClient, ObjectId } = require('mongodb');

const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri);

async function main() {
  try {
    await client.connect();
    const db = client.db('mydb');
    const users = db.collection('users');
    
    // CREATE
    const insertResult = await users.insertOne({
      name: 'Alice',
      email: 'alice@example.com',
      age: 25
    });
    console.log('Inserted:', insertResult.insertedId);
    
    // READ
    const user = await users.findOne({ name: 'Alice' });
    console.log('Found:', user);
    
    // UPDATE
    const updateResult = await users.updateOne(
      { name: 'Alice' },
      { $set: { age: 26 } }
    );
    console.log('Modified:', updateResult.modifiedCount);
    
    // DELETE
    const deleteResult = await users.deleteOne({ name: 'Alice' });
    console.log('Deleted:', deleteResult.deletedCount);
    
  } finally {
    await client.close();
  }
}

main().catch(console.error);
```

### Connection Pooling

```javascript
const { MongoClient } = require('mongodb');

const uri = 'mongodb://localhost:27017';

// Connection pool options
const options = {
  maxPoolSize: 10,        // Maximum connections
  minPoolSize: 5,         // Minimum connections
  maxIdleTimeMS: 10000,   // Close idle connections after 10s
  serverSelectionTimeoutMS: 5000,
  socketTimeoutMS: 45000,
};

const client = new MongoClient(uri, options);

// Singleton pattern
let dbInstance = null;

async function getDB() {
  if (!dbInstance) {
    await client.connect();
    dbInstance = client.db('mydb');
    console.log('Database connection established');
  }
  return dbInstance;
}

module.exports = { getDB, client };
```

**Usage:**

```javascript
const { getDB } = require('./db');

async function getUsers() {
  const db = await getDB();
  const users = await db.collection('users').find().toArray();
  return users;
}
```

---

## 3.2 Koneksi dengan Mongoose

### Mengapa Mongoose?

Mongoose adalah **ODM (Object Data Modeling)** library yang menyediakan:

✅ **Schema validation** - Struktur data yang jelas  
✅ **Type casting** - Automatic data type conversion  
✅ **Query building** - Chainable query API  
✅ **Middleware** - Pre/post hooks  
✅ **Virtuals** - Computed properties  
✅ **Population** - Automatic reference resolution  

### Basic Mongoose Connection

```javascript
const mongoose = require('mongoose');

// Simple connection
mongoose.connect('mongodb://localhost:27017/mydb')
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.error('Connection error:', err));
```

### Advanced Connection Setup

**config/database.js:**

```javascript
const mongoose = require('mongoose');

class Database {
  constructor() {
    this.connect();
  }
  
  connect() {
    mongoose.connect(process.env.MONGODB_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    })
    .then(() => {
      console.log('✅ Database connected successfully');
    })
    .catch((err) => {
      console.error('❌ Database connection error:', err);
      process.exit(1);
    });
    
    // Development logging
    if (process.env.NODE_ENV === 'development') {
      mongoose.set('debug', true);
    }
    
    // Connection events
    mongoose.connection.on('connected', () => {
      console.log('Mongoose connected to MongoDB');
    });
    
    mongoose.connection.on('error', (err) => {
      console.error('Mongoose connection error:', err);
    });
    
    mongoose.connection.on('disconnected', () => {
      console.log('Mongoose disconnected');
    });
    
    // Graceful shutdown
    process.on('SIGINT', this.gracefulShutdown);
    process.on('SIGTERM', this.gracefulShutdown);
  }
  
  async gracefulShutdown() {
    await mongoose.connection.close();
    console.log('Mongoose connection closed through app termination');
    process.exit(0);
  }
}

module.exports = new Database();
```

### Multiple Database Connections

```javascript
const mongoose = require('mongoose');

// Primary database
const db1 = mongoose.createConnection('mongodb://localhost:27017/db1');

// Secondary database
const db2 = mongoose.createConnection('mongodb://localhost:27017/db2');

// Define models for each connection
const User = db1.model('User', userSchema);
const Product = db2.model('Product', productSchema);

module.exports = { User, Product };
```

---

## 3.3 Schema & Model Definition

### Basic Schema

```javascript
const mongoose = require('mongoose');

// Define schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number,
  isActive: Boolean,
  createdAt: Date
});

// Create model
const User = mongoose.model('User', userSchema);

module.exports = User;
```

### Schema dengan Type Definitions

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  // String types
  name: {
    type: String,
    required: true,
    trim: true,
    minlength: 3,
    maxlength: 50
  },
  
  // Email dengan validation
  email: {
    type: String,
    required: [true, 'Email is required'],
    unique: true,
    lowercase: true,
    match: [/^\S+@\S+\.\S+$/, 'Please enter a valid email']
  },
  
  // Number dengan range
  age: {
    type: Number,
    min: [18, 'Must be at least 18'],
    max: [100, 'Must be at most 100']
  },
  
  // Enum
  role: {
    type: String,
    enum: ['user', 'admin', 'moderator'],
    default: 'user'
  },
  
  // Array
  tags: [String],
  
  // Nested object
  address: {
    street: String,
    city: String,
    zipcode: String,
    country: {
      type: String,
      default: 'Indonesia'
    }
  },
  
  // Date dengan default
  createdAt: {
    type: Date,
    default: Date.now
  },
  
  // Boolean
  isActive: {
    type: Boolean,
    default: true
  }
});

const User = mongoose.model('User', userSchema);
module.exports = User;
```

### Schema Types

| Type | Description | Example |
|------|-------------|---------|
| String | Text data | `name: String` |
| Number | Numeric data | `age: Number` |
| Date | Date/time | `createdAt: Date` |
| Boolean | true/false | `isActive: Boolean` |
| ObjectId | MongoDB ID | `userId: mongoose.Schema.Types.ObjectId` |
| Array | List of values | `tags: [String]` |
| Mixed | Any type | `data: mongoose.Schema.Types.Mixed` |
| Buffer | Binary data | `file: Buffer` |
| Map | Key-value pairs | `metadata: Map` |
| Decimal128 | High precision numbers | `price: mongoose.Schema.Types.Decimal128` |

### Schema Validation

```javascript
const productSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    validate: {
      validator: function(v) {
        return v.length >= 3;
      },
      message: 'Product name must be at least 3 characters'
    }
  },
  
  price: {
    type: Number,
    required: true,
    min: 0,
    validate: {
      validator: Number.isFinite,
      message: 'Price must be a valid number'
    }
  },
  
  sku: {
    type: String,
    required: true,
    unique: true,
    validate: {
      validator: function(v) {
        return /^[A-Z]{3}-\d{4}$/.test(v);
      },
      message: 'SKU must be in format: ABC-1234'
    }
  },
  
  stock: {
    type: Number,
    required: true,
    min: [0, 'Stock cannot be negative'],
    validate: {
      validator: Number.isInteger,
      message: 'Stock must be an integer'
    }
  }
});

const Product = mongoose.model('Product', productSchema);
```

### Custom Validation

```javascript
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    validate: {
      validator: async function(username) {
        // Check if username already exists
        const user = await mongoose.models.User.findOne({ username });
        return !user;
      },
      message: 'Username already exists'
    }
  },
  
  password: {
    type: String,
    required: true,
    validate: {
      validator: function(password) {
        // Password must contain uppercase, lowercase, number, special char
        return /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/.test(password);
      },
      message: 'Password must be at least 8 characters with uppercase, lowercase, number, and special character'
    }
  },
  
  confirmPassword: {
    type: String,
    required: true,
    validate: {
      validator: function(confirmPassword) {
        return confirmPassword === this.password;
      },
      message: 'Passwords do not match'
    }
  }
});
```

### Schema Options

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String
}, {
  // Options
  timestamps: true,           // Adds createdAt and updatedAt
  versionKey: false,          // Removes __v field
  collection: 'users',        // Custom collection name
  strict: true,               // Only save fields in schema
  strictQuery: false,         // Allow queries on non-schema fields
  toJSON: { virtuals: true }, // Include virtuals in JSON
  toObject: { virtuals: true } // Include virtuals in Object
});
```

---


## 3.4 Middleware & Hooks

### Apa itu Middleware?

Middleware (juga disebut hooks) adalah fungsi yang dijalankan pada tahap tertentu dalam lifecycle dokumen. Mongoose mendukung middleware untuk:

- `validate`
- `save`
- `remove`
- `updateOne`
- `deleteOne`
- `find`
- `findOne`
- `findOneAndUpdate`
- `findOneAndDelete`

### Pre Middleware

**Pre middleware** dijalankan **sebelum** operasi.

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String,
  createdAt: Date
});

// Pre-save middleware
userSchema.pre('save', function(next) {
  console.log('About to save user:', this.name);
  
  // Set createdAt if not exists
  if (!this.createdAt) {
    this.createdAt = new Date();
  }
  
  next();
});

// Pre-save dengan async/await
userSchema.pre('save', async function(next) {
  // Hash password before saving
  if (this.isModified('password')) {
    const bcrypt = require('bcrypt');
    this.password = await bcrypt.hash(this.password, 10);
  }
  next();
});
```

### Post Middleware

**Post middleware** dijalankan **setelah** operasi.

```javascript
// Post-save middleware
userSchema.post('save', function(doc, next) {
  console.log('User saved:', doc.name);
  next();
});

// Post-save error handling
userSchema.post('save', function(error, doc, next) {
  if (error.name === 'MongoServerError' && error.code === 11000) {
    next(new Error('Email already exists'));
  } else {
    next(error);
  }
});

// Post-find middleware
userSchema.post('find', function(docs) {
  console.log(`Found ${docs.length} users`);
});
```

### Practical Examples

**1. Password Hashing:**

```javascript
const bcrypt = require('bcrypt');

userSchema.pre('save', async function(next) {
  // Only hash if password is modified
  if (!this.isModified('password')) {
    return next();
  }
  
  try {
    const salt = await bcrypt.genSalt(10);
    this.password = await bcrypt.hash(this.password, salt);
    next();
  } catch (error) {
    next(error);
  }
});

// Method to compare password
userSchema.methods.comparePassword = async function(candidatePassword) {
  return await bcrypt.compare(candidatePassword, this.password);
};
```

**2. Slug Generation:**

```javascript
const slugify = require('slugify');

const articleSchema = new mongoose.Schema({
  title: String,
  slug: String,
  content: String
});

articleSchema.pre('save', function(next) {
  if (this.isModified('title')) {
    this.slug = slugify(this.title, { lower: true, strict: true });
  }
  next();
});
```

**3. Soft Delete:**

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  deletedAt: Date
});

// Override remove to soft delete
userSchema.pre('remove', function(next) {
  this.deletedAt = new Date();
  this.save();
  next();
});

// Filter out deleted documents
userSchema.pre(/^find/, function(next) {
  this.where({ deletedAt: null });
  next();
});
```

**4. Audit Trail:**

```javascript
const productSchema = new mongoose.Schema({
  name: String,
  price: Number,
  updatedBy: String,
  updateHistory: [{
    field: String,
    oldValue: mongoose.Schema.Types.Mixed,
    newValue: mongoose.Schema.Types.Mixed,
    updatedAt: Date,
    updatedBy: String
  }]
});

productSchema.pre('save', function(next) {
  if (this.isModified()) {
    const modifiedFields = this.modifiedPaths();
    
    modifiedFields.forEach(field => {
      this.updateHistory.push({
        field: field,
        oldValue: this._original[field],
        newValue: this[field],
        updatedAt: new Date(),
        updatedBy: this.updatedBy
      });
    });
  }
  next();
});
```

### Virtual Properties

Virtuals adalah properties yang tidak disimpan di database tapi bisa diakses seperti field biasa.

```javascript
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  email: String
});

// Virtual property
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

// Virtual setter
userSchema.virtual('fullName').set(function(name) {
  const parts = name.split(' ');
  this.firstName = parts[0];
  this.lastName = parts[1];
});

// Usage
const user = new User({ firstName: 'John', lastName: 'Doe' });
console.log(user.fullName); // "John Doe"

user.fullName = 'Jane Smith';
console.log(user.firstName); // "Jane"
console.log(user.lastName);  // "Smith"
```

### Instance Methods

Methods yang bisa dipanggil pada document instance.

```javascript
userSchema.methods.getPublicProfile = function() {
  return {
    id: this._id,
    name: this.name,
    email: this.email
    // password tidak di-include
  };
};

userSchema.methods.isAdmin = function() {
  return this.role === 'admin';
};

// Usage
const user = await User.findById(userId);
const profile = user.getPublicProfile();
if (user.isAdmin()) {
  // Admin logic
}
```

### Static Methods

Methods yang dipanggil pada Model (bukan instance).

```javascript
userSchema.statics.findByEmail = function(email) {
  return this.findOne({ email: email.toLowerCase() });
};

userSchema.statics.findActive = function() {
  return this.find({ isActive: true });
};

userSchema.statics.createWithDefaults = function(data) {
  return this.create({
    ...data,
    role: 'user',
    isActive: true,
    createdAt: new Date()
  });
};

// Usage
const user = await User.findByEmail('john@example.com');
const activeUsers = await User.findActive();
const newUser = await User.createWithDefaults({ name: 'Alice', email: 'alice@example.com' });
```

### Query Helpers

Custom query methods yang bisa di-chain.

```javascript
userSchema.query.byAge = function(age) {
  return this.where({ age: age });
};

userSchema.query.active = function() {
  return this.where({ isActive: true });
};

userSchema.query.sortByName = function() {
  return this.sort({ name: 1 });
};

// Usage
const users = await User
  .find()
  .byAge(25)
  .active()
  .sortByName();
```

### Complete Example

```javascript
const mongoose = require('mongoose');
const bcrypt = require('bcrypt');

const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    unique: true,
    trim: true
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true
  },
  password: {
    type: String,
    required: true,
    minlength: 8
  },
  firstName: String,
  lastName: String,
  role: {
    type: String,
    enum: ['user', 'admin'],
    default: 'user'
  },
  isActive: {
    type: Boolean,
    default: true
  },
  lastLogin: Date
}, {
  timestamps: true
});

// Virtual: fullName
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

// Pre-save: Hash password
userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();
  
  try {
    this.password = await bcrypt.hash(this.password, 10);
    next();
  } catch (error) {
    next(error);
  }
});

// Post-save: Log
userSchema.post('save', function(doc) {
  console.log(`User ${doc.username} has been saved`);
});

// Instance method: Compare password
userSchema.methods.comparePassword = async function(candidatePassword) {
  return await bcrypt.compare(candidatePassword, this.password);
};

// Instance method: Update last login
userSchema.methods.updateLastLogin = function() {
  this.lastLogin = new Date();
  return this.save();
};

// Static method: Find by email
userSchema.statics.findByEmail = function(email) {
  return this.findOne({ email: email.toLowerCase() });
};

// Query helper: Active users
userSchema.query.active = function() {
  return this.where({ isActive: true });
};

const User = mongoose.model('User', userSchema);

module.exports = User;
```

**Usage:**

```javascript
// Create user (password akan di-hash otomatis)
const user = await User.create({
  username: 'johndoe',
  email: 'john@example.com',
  password: 'SecurePass123',
  firstName: 'John',
  lastName: 'Doe'
});

// Get full name (virtual)
console.log(user.fullName); // "John Doe"

// Compare password
const isMatch = await user.comparePassword('SecurePass123');

// Update last login
await user.updateLastLogin();

// Find by email (static method)
const foundUser = await User.findByEmail('john@example.com');

// Query active users
const activeUsers = await User.find().active();
```

---

<div style="page-break-after: always;"></div>


# IV. CRUD OPERATIONS

## 4.1 Create Operation

### insertOne() - Native Driver

```javascript
const { MongoClient } = require('mongodb');

async function insertOneExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    const result = await collection.insertOne({
      name: 'Alice',
      email: 'alice@example.com',
      age: 25,
      createdAt: new Date()
    });
    
    console.log('Inserted ID:', result.insertedId);
    // Output: Inserted ID: 664a1b2c3d4e5f6g7h8i9j0k
    
  } finally {
    await client.close();
  }
}
```

### insertMany() - Native Driver

```javascript
async function insertManyExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    const users = [
      { name: 'Bob', email: 'bob@example.com', age: 30 },
      { name: 'Charlie', email: 'charlie@example.com', age: 28 },
      { name: 'Diana', email: 'diana@example.com', age: 32 }
    ];
    
    const result = await collection.insertMany(users);
    
    console.log('Inserted count:', result.insertedCount);
    console.log('Inserted IDs:', result.insertedIds);
    
  } finally {
    await client.close();
  }
}
```

### save() - Mongoose

```javascript
const User = require('./models/User');

// Method 1: Create instance then save
async function createUserMethod1() {
  const user = new User({
    name: 'Alice',
    email: 'alice@example.com',
    age: 25
  });
  
  await user.save();
  console.log('User saved:', user._id);
  return user;
}

// Method 2: Using create()
async function createUserMethod2() {
  const user = await User.create({
    name: 'Bob',
    email: 'bob@example.com',
    age: 30
  });
  
  console.log('User created:', user._id);
  return user;
}

// Method 3: Create multiple
async function createMultipleUsers() {
  const users = await User.create([
    { name: 'Charlie', email: 'charlie@example.com', age: 28 },
    { name: 'Diana', email: 'diana@example.com', age: 32 }
  ]);
  
  console.log('Created users:', users.length);
  return users;
}
```

### insertMany() - Mongoose

```javascript
async function bulkInsert() {
  const users = [
    { name: 'User 1', email: 'user1@example.com', age: 20 },
    { name: 'User 2', email: 'user2@example.com', age: 21 },
    { name: 'User 3', email: 'user3@example.com', age: 22 }
  ];
  
  const result = await User.insertMany(users);
  console.log('Inserted:', result.length);
  return result;
}

// With options
async function bulkInsertWithOptions() {
  const users = [
    { name: 'User 1', email: 'user1@example.com' },
    { name: 'User 2', email: 'duplicate@example.com' }, // Duplicate
    { name: 'User 3', email: 'user3@example.com' }
  ];
  
  try {
    const result = await User.insertMany(users, {
      ordered: false,  // Continue on error
      rawResult: true  // Return full result
    });
    console.log('Inserted:', result.insertedCount);
  } catch (error) {
    console.error('Some documents failed:', error.writeErrors);
  }
}
```

### Error Handling

```javascript
async function createWithErrorHandling() {
  try {
    const user = await User.create({
      name: 'Test User',
      email: 'invalid-email',  // Invalid format
      age: 15  // Below minimum
    });
  } catch (error) {
    if (error.name === 'ValidationError') {
      // Validation errors
      Object.keys(error.errors).forEach(key => {
        console.error(`${key}: ${error.errors[key].message}`);
      });
    } else if (error.code === 11000) {
      // Duplicate key error
      console.error('Email already exists');
    } else {
      console.error('Unknown error:', error);
    }
  }
}
```

### Practical Examples

**1. User Registration:**

```javascript
const bcrypt = require('bcrypt');

async function registerUser(userData) {
  try {
    // Check if email exists
    const existingUser = await User.findOne({ email: userData.email });
    if (existingUser) {
      throw new Error('Email already registered');
    }
    
    // Hash password
    const hashedPassword = await bcrypt.hash(userData.password, 10);
    
    // Create user
    const user = await User.create({
      name: userData.name,
      email: userData.email,
      password: hashedPassword,
      role: 'user',
      isActive: true,
      createdAt: new Date()
    });
    
    // Return without password
    return {
      id: user._id,
      name: user.name,
      email: user.email,
      role: user.role
    };
    
  } catch (error) {
    throw error;
  }
}

// Usage
const newUser = await registerUser({
  name: 'John Doe',
  email: 'john@example.com',
  password: 'SecurePass123'
});
```

**2. Create with Nested Documents:**

```javascript
const orderSchema = new mongoose.Schema({
  orderNumber: String,
  customer: {
    name: String,
    email: String,
    phone: String
  },
  items: [{
    product: String,
    quantity: Number,
    price: Number
  }],
  totalAmount: Number,
  status: {
    type: String,
    enum: ['pending', 'processing', 'shipped', 'delivered'],
    default: 'pending'
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

const Order = mongoose.model('Order', orderSchema);

async function createOrder(orderData) {
  // Calculate total
  const totalAmount = orderData.items.reduce((sum, item) => {
    return sum + (item.quantity * item.price);
  }, 0);
  
  const order = await Order.create({
    orderNumber: `ORD-${Date.now()}`,
    customer: orderData.customer,
    items: orderData.items,
    totalAmount: totalAmount,
    status: 'pending'
  });
  
  return order;
}

// Usage
const order = await createOrder({
  customer: {
    name: 'Alice',
    email: 'alice@example.com',
    phone: '+62812345678'
  },
  items: [
    { product: 'Laptop', quantity: 1, price: 1000 },
    { product: 'Mouse', quantity: 2, price: 20 }
  ]
});
```

**3. Bulk Create with Transaction:**

```javascript
async function createUsersWithTransaction(usersData) {
  const session = await mongoose.startSession();
  session.startTransaction();
  
  try {
    // Create users
    const users = await User.create(usersData, { session });
    
    // Create audit log
    await AuditLog.create({
      action: 'BULK_USER_CREATE',
      count: users.length,
      timestamp: new Date()
    }, { session });
    
    // Commit transaction
    await session.commitTransaction();
    console.log('Transaction committed');
    
    return users;
    
  } catch (error) {
    // Rollback on error
    await session.abortTransaction();
    console.error('Transaction aborted:', error);
    throw error;
    
  } finally {
    session.endSession();
  }
}
```

---

## 4.2 Read Operation

### findOne() - Native Driver

```javascript
async function findOneExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    // Find by field
    const user = await collection.findOne({ email: 'alice@example.com' });
    console.log('Found user:', user);
    
    // Find by ID
    const { ObjectId } = require('mongodb');
    const userById = await collection.findOne({ 
      _id: new ObjectId('664a1b2c3d4e5f6g7h8i9j0k') 
    });
    
  } finally {
    await client.close();
  }
}
```

### find() - Native Driver

```javascript
async function findExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    // Find all
    const allUsers = await collection.find().toArray();
    console.log('All users:', allUsers.length);
    
    // Find with filter
    const adults = await collection.find({ age: { $gte: 18 } }).toArray();
    
    // Find with projection (select fields)
    const names = await collection.find(
      {},
      { projection: { name: 1, email: 1, _id: 0 } }
    ).toArray();
    
    // Find with sort
    const sorted = await collection.find()
      .sort({ age: -1 })  // Descending
      .toArray();
    
    // Find with limit
    const limited = await collection.find()
      .limit(10)
      .toArray();
    
    // Find with skip (pagination)
    const page2 = await collection.find()
      .skip(10)
      .limit(10)
      .toArray();
    
  } finally {
    await client.close();
  }
}
```

### findOne() - Mongoose

```javascript
// Find by field
const user = await User.findOne({ email: 'alice@example.com' });

// Find by ID
const userById = await User.findById('664a1b2c3d4e5f6g7h8i9j0k');

// Find with select
const userWithoutPassword = await User.findOne({ email: 'alice@example.com' })
  .select('-password');

// Find with multiple conditions
const user = await User.findOne({
  email: 'alice@example.com',
  isActive: true
});

// Find or null
const user = await User.findOne({ email: 'notfound@example.com' });
if (!user) {
  console.log('User not found');
}
```

### find() - Mongoose

```javascript
// Find all
const allUsers = await User.find();

// Find with filter
const activeUsers = await User.find({ isActive: true });

// Find with multiple conditions
const users = await User.find({
  age: { $gte: 18, $lte: 65 },
  role: 'user'
});

// Find with select (projection)
const users = await User.find()
  .select('name email -_id');  // Include name, email; exclude _id

// Find with sort
const users = await User.find()
  .sort({ createdAt: -1 });  // Newest first

// Find with limit
const users = await User.find()
  .limit(10);

// Find with pagination
const page = 2;
const limit = 10;
const users = await User.find()
  .skip((page - 1) * limit)
  .limit(limit);

// Chaining
const users = await User.find({ isActive: true })
  .select('name email')
  .sort({ name: 1 })
  .limit(20)
  .skip(0);
```

### Query Operators

**Comparison Operators:**

```javascript
// $eq - Equal
await User.find({ age: { $eq: 25 } });
// atau
await User.find({ age: 25 });

// $ne - Not equal
await User.find({ role: { $ne: 'admin' } });

// $gt - Greater than
await User.find({ age: { $gt: 18 } });

// $gte - Greater than or equal
await User.find({ age: { $gte: 18 } });

// $lt - Less than
await User.find({ age: { $lt: 65 } });

// $lte - Less than or equal
await User.find({ age: { $lte: 65 } });

// $in - In array
await User.find({ role: { $in: ['user', 'moderator'] } });

// $nin - Not in array
await User.find({ status: { $nin: ['banned', 'suspended'] } });
```

**Logical Operators:**

```javascript
// $and
await User.find({
  $and: [
    { age: { $gte: 18 } },
    { age: { $lte: 65 } }
  ]
});

// $or
await User.find({
  $or: [
    { role: 'admin' },
    { role: 'moderator' }
  ]
});

// $not
await User.find({
  age: { $not: { $lt: 18 } }
});

// $nor - Not any
await User.find({
  $nor: [
    { status: 'banned' },
    { status: 'suspended' }
  ]
});
```

**Element Operators:**

```javascript
// $exists - Field exists
await User.find({ phone: { $exists: true } });

// $type - Field type
await User.find({ age: { $type: 'number' } });
```

**Array Operators:**

```javascript
// $all - Contains all elements
await User.find({ tags: { $all: ['javascript', 'nodejs'] } });

// $elemMatch - Array element matches
await Order.find({
  items: {
    $elemMatch: { quantity: { $gt: 5 }, price: { $lt: 100 } }
  }
});

// $size - Array size
await User.find({ tags: { $size: 3 } });
```

**String Operators:**

```javascript
// $regex - Regular expression
await User.find({ name: { $regex: /^John/, $options: 'i' } });

// Case-insensitive search
await User.find({ email: { $regex: 'gmail.com$', $options: 'i' } });
```

### Advanced Queries

**1. Pagination:**

```javascript
async function getPaginatedUsers(page = 1, limit = 10) {
  const skip = (page - 1) * limit;
  
  const users = await User.find()
    .select('-password')
    .sort({ createdAt: -1 })
    .skip(skip)
    .limit(limit);
  
  const total = await User.countDocuments();
  
  return {
    users,
    pagination: {
      page,
      limit,
      total,
      pages: Math.ceil(total / limit)
    }
  };
}

// Usage
const result = await getPaginatedUsers(2, 20);
console.log(`Page ${result.pagination.page} of ${result.pagination.pages}`);
```

**2. Search:**

```javascript
async function searchUsers(query) {
  const users = await User.find({
    $or: [
      { name: { $regex: query, $options: 'i' } },
      { email: { $regex: query, $options: 'i' } }
    ]
  })
  .select('name email')
  .limit(10);
  
  return users;
}

// Usage
const results = await searchUsers('john');
```

**3. Filter with Multiple Conditions:**

```javascript
async function filterUsers(filters) {
  const query = {};
  
  if (filters.role) {
    query.role = filters.role;
  }
  
  if (filters.minAge) {
    query.age = { ...query.age, $gte: filters.minAge };
  }
  
  if (filters.maxAge) {
    query.age = { ...query.age, $lte: filters.maxAge };
  }
  
  if (filters.isActive !== undefined) {
    query.isActive = filters.isActive;
  }
  
  if (filters.search) {
    query.$or = [
      { name: { $regex: filters.search, $options: 'i' } },
      { email: { $regex: filters.search, $options: 'i' } }
    ];
  }
  
  const users = await User.find(query)
    .select('-password')
    .sort({ createdAt: -1 });
  
  return users;
}

// Usage
const users = await filterUsers({
  role: 'user',
  minAge: 18,
  maxAge: 65,
  isActive: true,
  search: 'john'
});
```

---


## 4.3 Update Operation

### updateOne() - Native Driver

```javascript
async function updateOneExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    const result = await collection.updateOne(
      { email: 'alice@example.com' },  // Filter
      { $set: { age: 26, updatedAt: new Date() } }  // Update
    );
    
    console.log('Matched:', result.matchedCount);
    console.log('Modified:', result.modifiedCount);
    
  } finally {
    await client.close();
  }
}
```

### updateMany() - Native Driver

```javascript
async function updateManyExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    // Update all inactive users
    const result = await collection.updateMany(
      { isActive: false },
      { $set: { status: 'inactive', updatedAt: new Date() } }
    );
    
    console.log('Modified:', result.modifiedCount);
    
  } finally {
    await client.close();
  }
}
```

### Update Operators

**$set - Set field value:**

```javascript
await User.updateOne(
  { _id: userId },
  { $set: { name: 'New Name', email: 'new@example.com' } }
);
```

**$unset - Remove field:**

```javascript
await User.updateOne(
  { _id: userId },
  { $unset: { phone: '' } }  // Remove phone field
);
```

**$inc - Increment number:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $inc: { stock: -1, sold: 1 } }  // Decrease stock, increase sold
);
```

**$mul - Multiply:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $mul: { price: 1.1 } }  // Increase price by 10%
);
```

**$min - Update if new value is less:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $min: { lowestPrice: 100 } }  // Set to 100 if current > 100
);
```

**$max - Update if new value is greater:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $max: { highestPrice: 1000 } }  // Set to 1000 if current < 1000
);
```

**$rename - Rename field:**

```javascript
await User.updateMany(
  {},
  { $rename: { 'phone': 'phoneNumber' } }
);
```

**$currentDate - Set to current date:**

```javascript
await User.updateOne(
  { _id: userId },
  { $currentDate: { lastModified: true, lastLogin: { $type: 'date' } } }
);
```

### Array Update Operators

**$push - Add to array:**

```javascript
await User.updateOne(
  { _id: userId },
  { $push: { tags: 'javascript' } }
);

// Push multiple
await User.updateOne(
  { _id: userId },
  { $push: { tags: { $each: ['nodejs', 'mongodb'] } } }
);

// Push with sort and limit
await User.updateOne(
  { _id: userId },
  { 
    $push: { 
      scores: { 
        $each: [85, 90],
        $sort: -1,  // Sort descending
        $slice: 5   // Keep only top 5
      } 
    } 
  }
);
```

**$pull - Remove from array:**

```javascript
await User.updateOne(
  { _id: userId },
  { $pull: { tags: 'javascript' } }
);

// Pull with condition
await Order.updateOne(
  { _id: orderId },
  { $pull: { items: { quantity: 0 } } }
);
```

**$pop - Remove first or last element:**

```javascript
await User.updateOne(
  { _id: userId },
  { $pop: { tags: 1 } }  // Remove last element (-1 for first)
);
```

**$addToSet - Add if not exists:**

```javascript
await User.updateOne(
  { _id: userId },
  { $addToSet: { tags: 'javascript' } }  // Only add if not already in array
);

// Add multiple unique
await User.updateOne(
  { _id: userId },
  { $addToSet: { tags: { $each: ['nodejs', 'mongodb'] } } }
);
```

**$ (positional) - Update array element:**

```javascript
await Order.updateOne(
  { _id: orderId, 'items.product': 'Laptop' },
  { $set: { 'items.$.quantity': 2 } }  // Update matched item
);
```

**$[] (all positional) - Update all array elements:**

```javascript
await Order.updateOne(
  { _id: orderId },
  { $set: { 'items.$[].discount': 10 } }  // Update all items
);
```

**$[element] (filtered positional) - Update matching elements:**

```javascript
await Order.updateOne(
  { _id: orderId },
  { $set: { 'items.$[elem].discount': 20 } },
  { arrayFilters: [{ 'elem.price': { $gte: 100 } }] }  // Only items with price >= 100
);
```

### Mongoose Update Methods

**updateOne():**

```javascript
const result = await User.updateOne(
  { email: 'alice@example.com' },
  { $set: { age: 26 } }
);

console.log('Modified:', result.modifiedCount);
```

**updateMany():**

```javascript
const result = await User.updateMany(
  { isActive: false },
  { $set: { status: 'inactive' } }
);

console.log('Modified:', result.modifiedCount);
```

**findByIdAndUpdate():**

```javascript
const user = await User.findByIdAndUpdate(
  userId,
  { $set: { name: 'New Name' } },
  { new: true }  // Return updated document
);

console.log('Updated user:', user);
```

**findOneAndUpdate():**

```javascript
const user = await User.findOneAndUpdate(
  { email: 'alice@example.com' },
  { $set: { age: 26 } },
  { 
    new: true,           // Return updated document
    runValidators: true  // Run schema validators
  }
);
```

**save() method:**

```javascript
const user = await User.findById(userId);
user.name = 'New Name';
user.age = 26;
await user.save();  // Triggers middleware
```

### Practical Examples

**1. Update User Profile:**

```javascript
async function updateUserProfile(userId, updates) {
  try {
    const allowedUpdates = ['name', 'email', 'phone', 'address'];
    const updateData = {};
    
    // Filter allowed fields
    Object.keys(updates).forEach(key => {
      if (allowedUpdates.includes(key)) {
        updateData[key] = updates[key];
      }
    });
    
    const user = await User.findByIdAndUpdate(
      userId,
      { $set: updateData },
      { 
        new: true,
        runValidators: true,
        select: '-password'
      }
    );
    
    if (!user) {
      throw new Error('User not found');
    }
    
    return user;
    
  } catch (error) {
    throw error;
  }
}

// Usage
const updated = await updateUserProfile(userId, {
  name: 'John Doe',
  phone: '+62812345678'
});
```

**2. Increment Product Views:**

```javascript
async function incrementProductViews(productId) {
  const product = await Product.findByIdAndUpdate(
    productId,
    { 
      $inc: { views: 1 },
      $set: { lastViewed: new Date() }
    },
    { new: true }
  );
  
  return product;
}
```

**3. Add Comment to Post:**

```javascript
async function addComment(postId, commentData) {
  const post = await Post.findByIdAndUpdate(
    postId,
    {
      $push: {
        comments: {
          user: commentData.userId,
          text: commentData.text,
          createdAt: new Date()
        }
      },
      $inc: { commentCount: 1 }
    },
    { new: true }
  );
  
  return post;
}
```

**4. Update Order Status:**

```javascript
async function updateOrderStatus(orderId, newStatus) {
  const validStatuses = ['pending', 'processing', 'shipped', 'delivered', 'cancelled'];
  
  if (!validStatuses.includes(newStatus)) {
    throw new Error('Invalid status');
  }
  
  const order = await Order.findByIdAndUpdate(
    orderId,
    {
      $set: { status: newStatus },
      $push: {
        statusHistory: {
          status: newStatus,
          timestamp: new Date()
        }
      }
    },
    { new: true }
  );
  
  return order;
}
```

---

## 4.4 Delete Operation

### deleteOne() - Native Driver

```javascript
async function deleteOneExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    const result = await collection.deleteOne({ email: 'alice@example.com' });
    
    console.log('Deleted:', result.deletedCount);
    
  } finally {
    await client.close();
  }
}
```

### deleteMany() - Native Driver

```javascript
async function deleteManyExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    // Delete all inactive users
    const result = await collection.deleteMany({ isActive: false });
    
    console.log('Deleted:', result.deletedCount);
    
  } finally {
    await client.close();
  }
}
```

### Mongoose Delete Methods

**deleteOne():**

```javascript
const result = await User.deleteOne({ email: 'alice@example.com' });
console.log('Deleted:', result.deletedCount);
```

**deleteMany():**

```javascript
const result = await User.deleteMany({ isActive: false });
console.log('Deleted:', result.deletedCount);
```

**findByIdAndDelete():**

```javascript
const user = await User.findByIdAndDelete(userId);
if (user) {
  console.log('Deleted user:', user.name);
} else {
  console.log('User not found');
}
```

**findOneAndDelete():**

```javascript
const user = await User.findOneAndDelete({ email: 'alice@example.com' });
console.log('Deleted:', user);
```

**remove() - Deprecated:**

```javascript
// DON'T USE - Deprecated
// const user = await User.findById(userId);
// await user.remove();

// USE THIS INSTEAD:
const user = await User.findByIdAndDelete(userId);
```

### Soft Delete

Soft delete tidak menghapus data, hanya menandai sebagai deleted.

**Schema dengan Soft Delete:**

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  isDeleted: {
    type: Boolean,
    default: false
  },
  deletedAt: Date
});

// Middleware untuk filter deleted documents
userSchema.pre(/^find/, function(next) {
  this.where({ isDeleted: { $ne: true } });
  next();
});

const User = mongoose.model('User', userSchema);
```

**Soft Delete Implementation:**

```javascript
async function softDeleteUser(userId) {
  const user = await User.findByIdAndUpdate(
    userId,
    {
      $set: {
        isDeleted: true,
        deletedAt: new Date()
      }
    },
    { new: true }
  );
  
  return user;
}

// Restore deleted user
async function restoreUser(userId) {
  const user = await User.findOneAndUpdate(
    { _id: userId, isDeleted: true },
    {
      $set: {
        isDeleted: false,
        deletedAt: null
      }
    },
    { new: true }
  );
  
  return user;
}

// Find including deleted
async function findAllIncludingDeleted() {
  return await User.find().where('isDeleted').in([true, false]);
}
```

### Cascade Delete

Delete related documents when parent is deleted.

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

// Cascade delete posts when user is deleted
userSchema.pre('findOneAndDelete', async function(next) {
  const user = await this.model.findOne(this.getFilter());
  if (user) {
    await Post.deleteMany({ author: user._id });
    await Comment.deleteMany({ user: user._id });
  }
  next();
});

const User = mongoose.model('User', userSchema);
```

### Practical Examples

**1. Delete User with Validation:**

```javascript
async function deleteUser(userId, requesterId) {
  try {
    // Check if user exists
    const user = await User.findById(userId);
    if (!user) {
      throw new Error('User not found');
    }
    
    // Check permissions
    const requester = await User.findById(requesterId);
    if (requester.role !== 'admin' && userId !== requesterId) {
      throw new Error('Unauthorized');
    }
    
    // Delete user
    await User.findByIdAndDelete(userId);
    
    // Delete related data
    await Post.deleteMany({ author: userId });
    await Comment.deleteMany({ user: userId });
    
    return { message: 'User deleted successfully' };
    
  } catch (error) {
    throw error;
  }
}
```

**2. Bulk Delete with Conditions:**

```javascript
async function deleteInactiveUsers(days = 90) {
  const cutoffDate = new Date();
  cutoffDate.setDate(cutoffDate.getDate() - days);
  
  const result = await User.deleteMany({
    isActive: false,
    lastLogin: { $lt: cutoffDate }
  });
  
  console.log(`Deleted ${result.deletedCount} inactive users`);
  return result.deletedCount;
}
```

**3. Delete with Transaction:**

```javascript
async function deleteOrderWithTransaction(orderId) {
  const session = await mongoose.startSession();
  session.startTransaction();
  
  try {
    // Find order
    const order = await Order.findById(orderId).session(session);
    if (!order) {
      throw new Error('Order not found');
    }
    
    // Restore product stock
    for (const item of order.items) {
      await Product.findByIdAndUpdate(
        item.productId,
        { $inc: { stock: item.quantity } },
        { session }
      );
    }
    
    // Delete order
    await Order.findByIdAndDelete(orderId).session(session);
    
    // Commit transaction
    await session.commitTransaction();
    console.log('Order deleted and stock restored');
    
  } catch (error) {
    await session.abortTransaction();
    throw error;
  } finally {
    session.endSession();
  }
}
```

---

## 4.5 Query Operators & Filtering

### Comparison Operators Summary

| Operator | Description | Example |
|----------|-------------|---------|
| `$eq` | Equal | `{ age: { $eq: 25 } }` |
| `$ne` | Not equal | `{ age: { $ne: 25 } }` |
| `$gt` | Greater than | `{ age: { $gt: 18 } }` |
| `$gte` | Greater than or equal | `{ age: { $gte: 18 } }` |
| `$lt` | Less than | `{ age: { $lt: 65 } }` |
| `$lte` | Less than or equal | `{ age: { $lte: 65 } }` |
| `$in` | In array | `{ role: { $in: ['user', 'admin'] } }` |
| `$nin` | Not in array | `{ status: { $nin: ['banned'] } }` |

### Logical Operators Summary

| Operator | Description | Example |
|----------|-------------|---------|
| `$and` | All conditions true | `{ $and: [{ age: { $gte: 18 } }, { age: { $lte: 65 } }] }` |
| `$or` | Any condition true | `{ $or: [{ role: 'admin' }, { role: 'moderator' }] }` |
| `$not` | Inverts condition | `{ age: { $not: { $lt: 18 } } }` |
| `$nor` | None of conditions true | `{ $nor: [{ status: 'banned' }, { status: 'suspended' }] }` |

### Element Operators Summary

| Operator | Description | Example |
|----------|-------------|---------|
| `$exists` | Field exists | `{ phone: { $exists: true } }` |
| `$type` | Field type | `{ age: { $type: 'number' } }` |

### Array Operators Summary

| Operator | Description | Example |
|----------|-------------|---------|
| `$all` | Contains all | `{ tags: { $all: ['js', 'node'] } }` |
| `$elemMatch` | Array element matches | `{ items: { $elemMatch: { qty: { $gt: 5 } } } }` |
| `$size` | Array size | `{ tags: { $size: 3 } }` |

### Complex Query Examples

**1. Advanced Filtering:**

```javascript
async function advancedUserSearch(filters) {
  const query = {};
  
  // Age range
  if (filters.minAge || filters.maxAge) {
    query.age = {};
    if (filters.minAge) query.age.$gte = filters.minAge;
    if (filters.maxAge) query.age.$lte = filters.maxAge;
  }
  
  // Multiple roles
  if (filters.roles && filters.roles.length > 0) {
    query.role = { $in: filters.roles };
  }
  
  // Text search
  if (filters.search) {
    query.$or = [
      { name: { $regex: filters.search, $options: 'i' } },
      { email: { $regex: filters.search, $options: 'i' } }
    ];
  }
  
  // Date range
  if (filters.startDate || filters.endDate) {
    query.createdAt = {};
    if (filters.startDate) query.createdAt.$gte = new Date(filters.startDate);
    if (filters.endDate) query.createdAt.$lte = new Date(filters.endDate);
  }
  
  // Active status
  if (filters.isActive !== undefined) {
    query.isActive = filters.isActive;
  }
  
  const users = await User.find(query)
    .select('-password')
    .sort({ createdAt: -1 })
    .limit(filters.limit || 50);
  
  return users;
}
```

**2. Nested Object Query:**

```javascript
// Find users in Jakarta
await User.find({ 'address.city': 'Jakarta' });

// Find users with complete address
await User.find({
  'address.street': { $exists: true },
  'address.city': { $exists: true },
  'address.zipcode': { $exists: true }
});
```

**3. Array Query:**

```javascript
// Find users with 'javascript' tag
await User.find({ tags: 'javascript' });

// Find users with both tags
await User.find({ tags: { $all: ['javascript', 'nodejs'] } });

// Find users with at least 3 tags
await User.find({ tags: { $size: 3 } });

// Find orders with expensive items
await Order.find({
  items: {
    $elemMatch: {
      price: { $gte: 1000 },
      quantity: { $gte: 1 }
    }
  }
});
```

---

<div style="page-break-after: always;"></div>



# V. ADVANCED TOPICS

## 5.1 Aggregation Pipeline

Aggregation Pipeline adalah framework untuk memproses data dalam beberapa tahap (stages).

### Konsep Dasar

```
Collection → Stage 1 → Stage 2 → Stage 3 → Result
              $match    $group    $sort
```

### Stage-Stage Utama

**$match - Filter dokumen:**

```javascript
db.orders.aggregate([
  { $match: { status: "completed", amount: { $gte: 100 } } }
])
```

**$group - Kelompokkan dan hitung:**

```javascript
db.orders.aggregate([
  {
    $group: {
      _id: "$customer_id",
      totalSpent: { $sum: "$amount" },
      orderCount: { $sum: 1 },
      avgOrder: { $avg: "$amount" }
    }
  }
])
```

**$project - Pilih/transformasi field:**

```javascript
db.users.aggregate([
  {
    $project: {
      name: 1,
      email: 1,
      _id: 0,
      nameUpper: { $toUpper: "$name" },
      yearJoined: { $year: "$createdAt" }
    }
  }
])
```

**$sort, $limit, $skip:**

```javascript
db.products.aggregate([
  { $sort: { price: -1 } },
  { $skip: 0 },
  { $limit: 10 }
])
```

**$lookup - JOIN antar collection:**

```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "customer_id",
      foreignField: "_id",
      as: "customer"
    }
  },
  { $unwind: "$customer" }
])
```

**$unwind - Pecah array jadi dokumen terpisah:**

```javascript
db.orders.aggregate([
  { $unwind: "$items" },
  {
    $group: {
      _id: "$items.product",
      totalSold: { $sum: "$items.quantity" }
    }
  }
])
```

### Contoh Pipeline Lengkap - Laporan Penjualan Bulanan

```javascript
const salesReport = await Order.aggregate([
  { $match: { status: "completed" } },
  {
    $group: {
      _id: { year: { $year: "$createdAt" }, month: { $month: "$createdAt" } },
      totalRevenue: { $sum: "$amount" },
      orderCount: { $sum: 1 },
      avgOrderValue: { $avg: "$amount" }
    }
  },
  { $sort: { "_id.year": -1, "_id.month": -1 } },
  {
    $project: {
      _id: 0,
      period: { $concat: [{ $toString: "$_id.year" }, "-", { $toString: "$_id.month" }] },
      totalRevenue: { $round: ["$totalRevenue", 2] },
      orderCount: 1,
      avgOrderValue: { $round: ["$avgOrderValue", 2] }
    }
  }
]);
```

### Aggregation Expressions

```javascript
// String
{ $toUpper: "$name" }
{ $concat: ["$firstName", " ", "$lastName"] }

// Arithmetic
{ $add: ["$price", "$tax"] }
{ $multiply: ["$quantity", "$price"] }
{ $round: ["$price", 2] }

// Date
{ $year: "$createdAt" }
{ $month: "$createdAt" }
{ $dateToString: { format: "%Y-%m-%d", date: "$createdAt" } }

// Conditional
{ $cond: { if: { $gte: ["$age", 18] }, then: "adult", else: "minor" } }
{ $ifNull: ["$phone", "N/A"] }
```

---

## 5.2 Indexing Strategies

### Jenis-Jenis Index

**Single Field Index:**

```javascript
db.users.createIndex({ email: 1 })                          // Ascending
db.users.createIndex({ email: 1 }, { unique: true })        // Unique
db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 }) // TTL
```

**Compound Index:**

```javascript
db.users.createIndex({ city: 1, age: -1 })
// Mendukung: find({ city: "Jakarta" }) dan find({ city: "Jakarta", age: 25 })
// TIDAK mendukung: find({ age: 25 }) saja
```

**Text Index:**

```javascript
db.articles.createIndex({ title: "text", content: "text" })
db.articles.find({ $text: { $search: "mongodb tutorial" } })
```

**Geospatial Index:**

```javascript
db.places.createIndex({ location: "2dsphere" })
db.places.find({
  location: {
    $near: {
      $geometry: { type: "Point", coordinates: [106.83, -6.18] },
      $maxDistance: 5000
    }
  }
})
```

### Mongoose Index

```javascript
const userSchema = new mongoose.Schema({
  email: { type: String, index: true, unique: true },
  name: String,
  city: String,
  age: Number
});

userSchema.index({ city: 1, age: -1 });           // Compound
userSchema.index({ name: "text", email: "text" }); // Text
```

### Analisis Query dengan explain()

```javascript
const result = await User.find({ email: "alice@example.com" })
  .explain("executionStats");
// totalDocsExamined: 1 (dengan index) vs 1000 (tanpa index)
```

### Best Practices

```
✅ Index field yang sering di-query dan di-sort
✅ Compound index: equality → sort → range
✅ Monitor dengan $indexStats

❌ Jangan terlalu banyak index (memperlambat write)
❌ Jangan index field low cardinality (boolean)
```

---

## 5.3 Relationships & Population

### Embedding vs Referencing

**Embedding (data dalam satu dokumen):**

```javascript
// Cocok: data selalu diakses bersama, 1-to-few
const userSchema = new mongoose.Schema({
  name: String,
  address: { street: String, city: String, zipcode: String },
  phones: [String]
});
```

**Referencing (data terpisah dengan ID):**

```javascript
// Cocok: data besar, many-to-many, sering berubah
const postSchema = new mongoose.Schema({
  title: String,
  content: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  tags: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Tag' }]
});
```

### Mongoose Population

```javascript
// Basic populate
const post = await Post.findById(postId)
  .populate('author', 'name email');

// Nested populate
const post = await Post.findById(postId)
  .populate({
    path: 'author',
    select: 'name email',
    populate: { path: 'profile', select: 'avatar bio' }
  });

// Multiple populate
const post = await Post.findById(postId)
  .populate('author', 'name')
  .populate('tags', 'name color')
  .populate('comments.user', 'name avatar');
```

### $lookup (Aggregation JOIN)

```javascript
const postsWithAuthors = await Post.aggregate([
  { $match: { isPublished: true } },
  {
    $lookup: {
      from: "users",
      localField: "author",
      foreignField: "_id",
      as: "authorData"
    }
  },
  { $unwind: "$authorData" },
  { $project: { title: 1, "authorData.name": 1 } }
]);
```

---

## 5.4 Error Handling

### Jenis Error MongoDB/Mongoose

| Error | Penyebab |
|-------|----------|
| `ValidationError` | Data tidak sesuai schema |
| `CastError` | Tipe data salah (string ke ObjectId) |
| `MongoServerError 11000` | Duplicate key |
| `MongoNetworkError` | Koneksi gagal |

### Error Handling Pattern

```javascript
async function createUser(data) {
  try {
    const user = await User.create(data);
    return user;
  } catch (error) {
    if (error.name === 'ValidationError') {
      const messages = Object.values(error.errors).map(e => e.message);
      throw new Error(`Validation: ${messages.join(', ')}`);
    }
    if (error.code === 11000) {
      const field = Object.keys(error.keyValue)[0];
      throw new Error(`${field} sudah digunakan`);
    }
    throw error;
  }
}
```

### Express Error Handler Middleware

```javascript
// middleware/errorHandler.js
const errorHandler = (err, req, res, next) => {
  let statusCode = 500;
  let message = 'Internal Server Error';

  if (err.name === 'ValidationError') {
    statusCode = 400;
    message = Object.values(err.errors).map(e => e.message).join(', ');
  } else if (err.name === 'CastError') {
    statusCode = 400;
    message = `Invalid ${err.path}: ${err.value}`;
  } else if (err.code === 11000) {
    statusCode = 409;
    message = `${Object.keys(err.keyValue)[0]} sudah terdaftar`;
  } else if (err.statusCode) {
    statusCode = err.statusCode;
    message = err.message;
  }

  res.status(statusCode).json({ success: false, message });
};

module.exports = errorHandler;
```

### Async Handler Wrapper

```javascript
// utils/asyncHandler.js
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

// Penggunaan - tidak perlu try-catch di setiap route
app.get('/users', asyncHandler(async (req, res) => {
  const users = await User.find();
  res.json({ success: true, data: users });
}));

app.use(errorHandler);
```

---

<div style="page-break-after: always;"></div>



# VI. BEST PRACTICES

## 6.1 Performance Optimization

### Query Optimization

```javascript
// ❌ Buruk: Ambil semua field
const users = await User.find();

// ✅ Baik: Hanya ambil field yang dibutuhkan
const users = await User.find().select('name email');

// ❌ Buruk: Ambil semua data lalu filter di aplikasi
const allUsers = await User.find();
const adults = allUsers.filter(u => u.age >= 18);

// ✅ Baik: Filter di database
const adults = await User.find({ age: { $gte: 18 } });

// ✅ Gunakan lean() untuk read-only (skip Mongoose overhead)
const users = await User.find().lean();

// ✅ Pagination
const users = await User.find()
  .sort({ createdAt: -1 })
  .skip((page - 1) * limit)
  .limit(limit);
```

### Connection Pooling

```javascript
// config/database.js
mongoose.connect(process.env.MONGODB_URI, {
  maxPoolSize: 10,      // Max connections
  minPoolSize: 5,       // Min connections
  maxIdleTimeMS: 10000, // Close idle connections
  serverSelectionTimeoutMS: 5000
});
```

### Bulk Operations

```javascript
// ❌ Buruk: Loop individual operations
for (const item of items) {
  await Product.updateOne({ _id: item.id }, { $set: { price: item.price } });
}

// ✅ Baik: Bulk write
const bulkOps = items.map(item => ({
  updateOne: {
    filter: { _id: item.id },
    update: { $set: { price: item.price } }
  }
}));
await Product.bulkWrite(bulkOps);
```

### Caching Strategy

```javascript
// Simple in-memory cache
const cache = new Map();

async function getUserById(id) {
  const cacheKey = `user:${id}`;
  
  if (cache.has(cacheKey)) {
    return cache.get(cacheKey);
  }
  
  const user = await User.findById(id).lean();
  cache.set(cacheKey, user);
  setTimeout(() => cache.delete(cacheKey), 60000); // TTL 60s
  
  return user;
}
```

---

## 6.2 Security Guidelines

### Input Validation & Sanitization

```javascript
// ❌ Buruk: Langsung pakai input user
app.get('/users', async (req, res) => {
  const users = await User.find(req.query); // NoSQL Injection!
});

// ✅ Baik: Validasi dan sanitize input
const sanitize = require('mongo-sanitize');

app.get('/users', async (req, res) => {
  const filter = {};
  if (req.query.name) filter.name = sanitize(req.query.name);
  if (req.query.role) filter.role = sanitize(req.query.role);
  const users = await User.find(filter);
  res.json(users);
});
```

### NoSQL Injection Prevention

```javascript
// ❌ Rentan injection: { "$gt": "" } bisa bypass
app.post('/login', async (req, res) => {
  const user = await User.findOne({
    email: req.body.email,
    password: req.body.password  // Bisa diinject!
  });
});

// ✅ Aman: Validasi tipe data
app.post('/login', async (req, res) => {
  if (typeof req.body.email !== 'string' || typeof req.body.password !== 'string') {
    return res.status(400).json({ message: 'Invalid input' });
  }
  const user = await User.findOne({ email: req.body.email });
  if (!user || !(await bcrypt.compare(req.body.password, user.password))) {
    return res.status(401).json({ message: 'Invalid credentials' });
  }
  res.json({ token: generateToken(user) });
});
```

### Environment Variables

```bash
# .env - JANGAN commit ke git!
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/mydb
JWT_SECRET=your-secret-key
NODE_ENV=production
```

```javascript
// Validasi env vars saat startup
const requiredEnvVars = ['MONGODB_URI', 'JWT_SECRET'];
requiredEnvVars.forEach(varName => {
  if (!process.env[varName]) {
    console.error(`Missing env var: ${varName}`);
    process.exit(1);
  }
});
```

### Field-Level Security

```javascript
// Jangan pernah return password
const userSchema = new mongoose.Schema({
  email: String,
  password: { type: String, select: false } // Tidak di-return by default
});

// Hanya ambil password saat login
const user = await User.findOne({ email }).select('+password');
```

---

## 6.3 Code Organization

### Project Structure (MVC Pattern)

```
project/
├── config/
│   └── database.js          # Koneksi database
├── models/
│   ├── User.js              # User schema & model
│   ├── Post.js              # Post schema & model
│   └── index.js             # Export semua models
├── controllers/
│   ├── userController.js    # Logic handler
│   └── postController.js
├── routes/
│   ├── userRoutes.js        # Route definitions
│   └── postRoutes.js
├── middleware/
│   ├── auth.js              # Authentication
│   ├── errorHandler.js      # Error handling
│   └── validate.js          # Input validation
├── utils/
│   ├── asyncHandler.js
│   └── helpers.js
├── .env
├── .gitignore
├── package.json
└── index.js                 # Entry point
```

### Controller Pattern

```javascript
// controllers/userController.js
const User = require('../models/User');
const asyncHandler = require('../utils/asyncHandler');

exports.getUsers = asyncHandler(async (req, res) => {
  const { page = 1, limit = 10, search } = req.query;
  const filter = search
    ? { name: { $regex: search, $options: 'i' } }
    : {};

  const users = await User.find(filter)
    .select('-password')
    .skip((page - 1) * limit)
    .limit(Number(limit));

  const total = await User.countDocuments(filter);

  res.json({
    success: true,
    data: users,
    pagination: { page: Number(page), limit: Number(limit), total }
  });
});

exports.createUser = asyncHandler(async (req, res) => {
  const user = await User.create(req.body);
  res.status(201).json({ success: true, data: user });
});
```

### Route Pattern

```javascript
// routes/userRoutes.js
const router = require('express').Router();
const { getUsers, createUser } = require('../controllers/userController');
const { protect, authorize } = require('../middleware/auth');

router.route('/')
  .get(getUsers)
  .post(protect, authorize('admin'), createUser);

module.exports = router;
```

---

## 6.4 Common Pitfalls

### 1. Lupa await

```javascript
// ❌ Buruk: Lupa await - mendapat Promise bukan data
const user = User.findById(id);
console.log(user.name); // undefined!

// ✅ Baik
const user = await User.findById(id);
console.log(user.name);
```

### 2. N+1 Query Problem

```javascript
// ❌ Buruk: Query di dalam loop
const posts = await Post.find();
for (const post of posts) {
  post.author = await User.findById(post.authorId); // N queries!
}

// ✅ Baik: Gunakan populate atau $lookup
const posts = await Post.find().populate('author', 'name email');
```

### 3. Tidak Handle null

```javascript
// ❌ Buruk: Crash jika user null
const user = await User.findById(id);
res.json(user.name); // TypeError jika null!

// ✅ Baik
const user = await User.findById(id);
if (!user) {
  return res.status(404).json({ message: 'User not found' });
}
res.json(user.name);
```

### 4. Memory Leak - Cursor Tidak Ditutup

```javascript
// ❌ Buruk untuk data besar
const allDocs = await Collection.find().toArray(); // Load semua ke memory

// ✅ Baik: Gunakan cursor/stream
const cursor = Collection.find().cursor();
for await (const doc of cursor) {
  // Process satu per satu
}
```

### 5. Tidak Validasi ObjectId

```javascript
// ❌ Crash jika id bukan valid ObjectId
app.get('/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id); // CastError!
});

// ✅ Validasi dulu
const mongoose = require('mongoose');

app.get('/users/:id', async (req, res) => {
  if (!mongoose.Types.ObjectId.isValid(req.params.id)) {
    return res.status(400).json({ message: 'Invalid ID' });
  }
  const user = await User.findById(req.params.id);
  if (!user) return res.status(404).json({ message: 'Not found' });
  res.json(user);
});
```

### 6. Schema Mismatch

```javascript
// ❌ Field tidak ada di schema (strict mode default)
const userSchema = new mongoose.Schema({ name: String, email: String });
await User.create({ name: "Alice", email: "a@b.com", phone: "123" });
// phone TIDAK tersimpan!

// ✅ Pastikan semua field ada di schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  phone: String  // Tambahkan field
});
```

---

<div style="page-break-after: always;"></div>



# VII. STUDI KASUS & PROJECT

## 7.1 Project Structure

### Studi Kasus: REST API Toko Online

Membangun REST API sederhana untuk manajemen produk dan pesanan menggunakan Express.js + MongoDB + Mongoose.

### Struktur Folder

```
toko-online-api/
├── config/
│   └── database.js
├── models/
│   ├── Product.js
│   ├── Order.js
│   └── User.js
├── controllers/
│   ├── productController.js
│   └── orderController.js
├── routes/
│   ├── productRoutes.js
│   └── orderRoutes.js
├── middleware/
│   ├── auth.js
│   └── errorHandler.js
├── utils/
│   └── asyncHandler.js
├── .env
├── package.json
└── server.js
```

### Dependencies

```json
{
  "name": "toko-online-api",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^8.3.0",
    "dotenv": "^16.4.5",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.2"
  },
  "devDependencies": {
    "nodemon": "^3.1.0"
  }
}
```

---

## 7.2 Complete Example

### config/database.js

```javascript
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI);
    console.log('✅ MongoDB Connected');
  } catch (error) {
    console.error('❌ MongoDB Error:', error.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### models/Product.js

```javascript
const mongoose = require('mongoose');

const productSchema = new mongoose.Schema({
  name: { type: String, required: [true, 'Nama produk wajib diisi'], trim: true },
  price: { type: Number, required: true, min: [0, 'Harga tidak boleh negatif'] },
  stock: { type: Number, required: true, min: 0, default: 0 },
  category: { type: String, enum: ['elektronik', 'pakaian', 'makanan', 'lainnya'], default: 'lainnya' },
  description: String,
  isActive: { type: Boolean, default: true }
}, { timestamps: true });

productSchema.index({ name: 'text', description: 'text' });
productSchema.index({ category: 1, price: 1 });

module.exports = mongoose.model('Product', productSchema);
```

### models/Order.js

```javascript
const mongoose = require('mongoose');

const orderSchema = new mongoose.Schema({
  orderNumber: { type: String, unique: true },
  customer: {
    name: { type: String, required: true },
    email: { type: String, required: true },
    phone: String
  },
  items: [{
    product: { type: mongoose.Schema.Types.ObjectId, ref: 'Product', required: true },
    quantity: { type: Number, required: true, min: 1 },
    price: { type: Number, required: true }
  }],
  totalAmount: { type: Number, required: true },
  status: {
    type: String,
    enum: ['pending', 'processing', 'shipped', 'delivered', 'cancelled'],
    default: 'pending'
  }
}, { timestamps: true });

// Auto-generate order number
orderSchema.pre('save', function(next) {
  if (!this.orderNumber) {
    this.orderNumber = `ORD-${Date.now()}-${Math.random().toString(36).substr(2, 5).toUpperCase()}`;
  }
  next();
});

module.exports = mongoose.model('Order', orderSchema);
```

### controllers/productController.js

```javascript
const Product = require('../models/Product');
const asyncHandler = require('../utils/asyncHandler');

// GET /api/products
exports.getProducts = asyncHandler(async (req, res) => {
  const { page = 1, limit = 10, category, search, sort = '-createdAt' } = req.query;
  const filter = { isActive: true };

  if (category) filter.category = category;
  if (search) filter.$text = { $search: search };

  const products = await Product.find(filter)
    .sort(sort)
    .skip((page - 1) * limit)
    .limit(Number(limit));

  const total = await Product.countDocuments(filter);

  res.json({
    success: true,
    data: products,
    pagination: { page: Number(page), limit: Number(limit), total, pages: Math.ceil(total / limit) }
  });
});

// GET /api/products/:id
exports.getProduct = asyncHandler(async (req, res) => {
  const product = await Product.findById(req.params.id);
  if (!product) return res.status(404).json({ success: false, message: 'Produk tidak ditemukan' });
  res.json({ success: true, data: product });
});

// POST /api/products
exports.createProduct = asyncHandler(async (req, res) => {
  const product = await Product.create(req.body);
  res.status(201).json({ success: true, data: product });
});

// PUT /api/products/:id
exports.updateProduct = asyncHandler(async (req, res) => {
  const product = await Product.findByIdAndUpdate(req.params.id, req.body, {
    new: true, runValidators: true
  });
  if (!product) return res.status(404).json({ success: false, message: 'Produk tidak ditemukan' });
  res.json({ success: true, data: product });
});

// DELETE /api/products/:id
exports.deleteProduct = asyncHandler(async (req, res) => {
  const product = await Product.findByIdAndUpdate(req.params.id, { isActive: false }, { new: true });
  if (!product) return res.status(404).json({ success: false, message: 'Produk tidak ditemukan' });
  res.json({ success: true, message: 'Produk dihapus' });
});
```

### controllers/orderController.js

```javascript
const Order = require('../models/Order');
const Product = require('../models/Product');
const asyncHandler = require('../utils/asyncHandler');

// POST /api/orders
exports.createOrder = asyncHandler(async (req, res) => {
  const { customer, items } = req.body;

  // Validasi stok dan hitung total
  let totalAmount = 0;
  const orderItems = [];

  for (const item of items) {
    const product = await Product.findById(item.product);
    if (!product) return res.status(404).json({ message: `Produk ${item.product} tidak ditemukan` });
    if (product.stock < item.quantity) {
      return res.status(400).json({ message: `Stok ${product.name} tidak cukup` });
    }

    orderItems.push({ product: product._id, quantity: item.quantity, price: product.price });
    totalAmount += product.price * item.quantity;

    // Kurangi stok
    await Product.findByIdAndUpdate(product._id, { $inc: { stock: -item.quantity } });
  }

  const order = await Order.create({ customer, items: orderItems, totalAmount });
  res.status(201).json({ success: true, data: order });
});

// GET /api/orders/:id
exports.getOrder = asyncHandler(async (req, res) => {
  const order = await Order.findById(req.params.id).populate('items.product', 'name category');
  if (!order) return res.status(404).json({ success: false, message: 'Order tidak ditemukan' });
  res.json({ success: true, data: order });
});

// PATCH /api/orders/:id/status
exports.updateStatus = asyncHandler(async (req, res) => {
  const { status } = req.body;
  const order = await Order.findByIdAndUpdate(
    req.params.id,
    { status },
    { new: true, runValidators: true }
  );
  if (!order) return res.status(404).json({ success: false, message: 'Order tidak ditemukan' });
  res.json({ success: true, data: order });
});
```

### routes/productRoutes.js & orderRoutes.js

```javascript
// routes/productRoutes.js
const router = require('express').Router();
const { getProducts, getProduct, createProduct, updateProduct, deleteProduct } = require('../controllers/productController');

router.route('/').get(getProducts).post(createProduct);
router.route('/:id').get(getProduct).put(updateProduct).delete(deleteProduct);

module.exports = router;

// routes/orderRoutes.js
const router = require('express').Router();
const { createOrder, getOrder, updateStatus } = require('../controllers/orderController');

router.route('/').post(createOrder);
router.route('/:id').get(getOrder);
router.route('/:id/status').patch(updateStatus);

module.exports = router;
```

### server.js

```javascript
const express = require('express');
const connectDB = require('./config/database');
const errorHandler = require('./middleware/errorHandler');
require('dotenv').config();

const app = express();

// Connect DB
connectDB();

// Middleware
app.use(express.json());

// Routes
app.use('/api/products', require('./routes/productRoutes'));
app.use('/api/orders', require('./routes/orderRoutes'));

// Health check
app.get('/health', (req, res) => res.json({ status: 'OK', time: new Date() }));

// Error handler
app.use(errorHandler);

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

---

## 7.3 Source Code

### utils/asyncHandler.js

```javascript
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};
module.exports = asyncHandler;
```

### middleware/errorHandler.js

```javascript
const errorHandler = (err, req, res, next) => {
  let statusCode = err.statusCode || 500;
  let message = err.message || 'Internal Server Error';

  if (err.name === 'ValidationError') {
    statusCode = 400;
    message = Object.values(err.errors).map(e => e.message).join(', ');
  } else if (err.name === 'CastError') {
    statusCode = 400;
    message = 'ID tidak valid';
  } else if (err.code === 11000) {
    statusCode = 409;
    message = 'Data duplikat';
  }

  res.status(statusCode).json({ success: false, message });
};
module.exports = errorHandler;
```

### Testing API dengan cURL

```bash
# Create Product
curl -X POST http://localhost:3000/api/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop ASUS","price":12000000,"stock":50,"category":"elektronik"}'

# Get All Products
curl http://localhost:3000/api/products?page=1&limit=5&category=elektronik

# Search Products
curl http://localhost:3000/api/products?search=laptop

# Create Order
curl -X POST http://localhost:3000/api/orders \
  -H "Content-Type: application/json" \
  -d '{
    "customer": {"name":"Budi","email":"budi@email.com","phone":"08123456"},
    "items": [{"product":"<product_id>","quantity":1}]
  }'

# Update Order Status
curl -X PATCH http://localhost:3000/api/orders/<order_id>/status \
  -H "Content-Type: application/json" \
  -d '{"status":"shipped"}'
```

---

<div style="page-break-after: always;"></div>



# VIII. SOAL & JAWABAN

## 8.1 Soal Konsep (Pilihan Ganda & Essay)

### Pilihan Ganda

**1.** Apa kepanjangan dari NoSQL?

a) No SQL  
b) Not Only SQL  
c) New SQL  
d) Non-Standard Query Language  

**2.** MongoDB menyimpan data dalam format?

a) Tabel dan baris  
b) Key-Value pairs  
c) Dokumen BSON  
d) Graph nodes  

**3.** Manakah yang BUKAN merupakan kelebihan MongoDB?

a) Schema fleksibel  
b) Horizontal scaling  
c) Multi-document ACID transactions sejak versi 1.0  
d) High availability dengan Replica Set  

**4.** Operator MongoDB yang digunakan untuk mencocokkan nilai lebih besar dari adalah?

a) `$gt`  
b) `$gte`  
c) `$lt`  
d) `$bigger`  

**5.** Apa fungsi dari `$lookup` dalam aggregation pipeline?

a) Mencari dokumen  
b) Melakukan JOIN antar collection  
c) Membuat index  
d) Menghapus dokumen  

**6.** Mongoose adalah?

a) MongoDB GUI tool  
b) Object Data Modeling (ODM) library untuk Node.js  
c) Database engine  
d) Query language  

**7.** Middleware `pre('save')` di Mongoose dijalankan?

a) Setelah dokumen disimpan  
b) Sebelum dokumen disimpan  
c) Saat dokumen dihapus  
d) Saat koneksi dibuat  

**8.** Apa yang terjadi jika field tidak ada di schema Mongoose (strict mode default)?

a) Error thrown  
b) Field tetap disimpan  
c) Field diabaikan/tidak disimpan  
d) Database crash  

**9.** Index TTL digunakan untuk?

a) Mempercepat query  
b) Auto-delete dokumen setelah waktu tertentu  
c) Membuat unique constraint  
d) Full-text search  

**10.** Metode mana yang mengembalikan dokumen yang sudah di-update?

a) `updateOne()`  
b) `updateMany()`  
c) `findByIdAndUpdate()` dengan option `{ new: true }`  
d) `deleteOne()`  

### Essay

**11.** Jelaskan perbedaan antara embedding dan referencing dalam MongoDB. Kapan sebaiknya menggunakan masing-masing pendekatan?

**12.** Apa itu Aggregation Pipeline? Jelaskan minimal 4 stage yang sering digunakan beserta fungsinya.

**13.** Jelaskan konsep CAP Theorem dan bagaimana MongoDB memposisikan diri dalam theorem tersebut.

**14.** Mengapa indexing penting dalam MongoDB? Jelaskan minimal 3 jenis index yang tersedia.

**15.** Jelaskan apa itu NoSQL Injection dan bagaimana cara mencegahnya di aplikasi Node.js + MongoDB.

---

## 8.2 Soal Praktik

**Soal 1: Schema Design**

Buatlah Mongoose schema untuk sistem perpustakaan dengan ketentuan:
- Model `Book`: judul (wajib), pengarang, ISBN (unik), tahun terbit, genre (enum), stok
- Model `Member`: nama (wajib), email (unik), no_anggota, tanggal_daftar
- Model `Borrowing`: referensi ke Book dan Member, tanggal_pinjam, tanggal_kembali, status

**Soal 2: CRUD Operations**

Tuliskan kode untuk:
- a) Menambahkan 5 buku sekaligus (insertMany)
- b) Mencari buku dengan genre "fiksi" dan tahun terbit > 2020
- c) Update stok buku berkurang 1 saat dipinjam
- d) Soft delete buku (set isActive = false)

**Soal 3: Aggregation**

Buatlah aggregation pipeline untuk:
- Menghitung jumlah buku per genre
- Menampilkan genre dengan buku terbanyak di urutan pertama
- Hanya tampilkan genre yang memiliki lebih dari 5 buku

**Soal 4: API Endpoint**

Buatlah Express route `GET /api/books` dengan fitur:
- Pagination (page & limit)
- Filter berdasarkan genre
- Search berdasarkan judul
- Sort berdasarkan tahun terbit

---

## 8.3 Kunci Jawaban

### Jawaban Pilihan Ganda

| No | Jawaban | Penjelasan |
|----|---------|------------|
| 1 | **b** | NoSQL = Not Only SQL |
| 2 | **c** | MongoDB menggunakan dokumen BSON (Binary JSON) |
| 3 | **c** | Multi-document transactions baru ada sejak MongoDB 4.0 |
| 4 | **a** | `$gt` = greater than, `$gte` = greater than or equal |
| 5 | **b** | `$lookup` melakukan JOIN antar collection |
| 6 | **b** | Mongoose adalah ODM library untuk Node.js |
| 7 | **b** | `pre('save')` dijalankan sebelum save |
| 8 | **c** | Strict mode: field di luar schema diabaikan |
| 9 | **b** | TTL index auto-delete dokumen setelah expireAfterSeconds |
| 10 | **c** | `findByIdAndUpdate` dengan `{ new: true }` return updated doc |

### Jawaban Essay

**11. Embedding vs Referencing:**

- **Embedding**: Data disimpan dalam satu dokumen. Cocok untuk relasi 1-to-few, data yang selalu diakses bersama, dan data yang jarang berubah. Contoh: alamat user.
- **Referencing**: Data disimpan terpisah dengan ObjectId sebagai penghubung. Cocok untuk relasi many-to-many, data besar, dan data yang sering berubah. Contoh: post dan author.

**12. Aggregation Pipeline:**

Pipeline memproses data dalam tahap berurutan:
- `$match`: Filter dokumen (seperti WHERE di SQL)
- `$group`: Kelompokkan dan hitung (seperti GROUP BY)
- `$sort`: Urutkan hasil
- `$project`: Pilih/transformasi field (seperti SELECT)
- `$lookup`: JOIN antar collection
- `$unwind`: Pecah array menjadi dokumen terpisah

**13. CAP Theorem:**

CAP Theorem menyatakan sistem terdistribusi hanya bisa memenuhi 2 dari 3: Consistency, Availability, Partition Tolerance. MongoDB termasuk kategori **CP** - mengutamakan Consistency dan Partition Tolerance. Saat terjadi network partition, MongoDB mungkin tidak available (primary election) tapi menjamin data konsisten.

**14. Indexing:**

Index mempercepat query dengan membuat struktur data terurut. Tanpa index, MongoDB harus scan seluruh collection (COLLSCAN). Jenis index:
- **Single Field**: Index pada satu field (`{ email: 1 }`)
- **Compound**: Index pada beberapa field (`{ city: 1, age: -1 }`)
- **Text**: Full-text search (`{ content: "text" }`)
- **TTL**: Auto-expire documents
- **Geospatial**: Query lokasi (`{ location: "2dsphere" }`)

**15. NoSQL Injection:**

NoSQL Injection terjadi saat attacker menyisipkan operator MongoDB melalui input. Contoh: mengirim `{"$gt": ""}` sebagai password untuk bypass authentication. Pencegahan:
- Validasi tipe data input (pastikan string, bukan object)
- Gunakan library `mongo-sanitize`
- Jangan langsung pass `req.body`/`req.query` ke query
- Gunakan schema validation Mongoose

### Jawaban Soal Praktik

**Soal 1:**

```javascript
const bookSchema = new mongoose.Schema({
  judul: { type: String, required: true },
  pengarang: String,
  isbn: { type: String, unique: true },
  tahunTerbit: Number,
  genre: { type: String, enum: ['fiksi', 'nonfiksi', 'sains', 'sejarah', 'teknologi'] },
  stok: { type: Number, default: 0, min: 0 },
  isActive: { type: Boolean, default: true }
}, { timestamps: true });

const memberSchema = new mongoose.Schema({
  nama: { type: String, required: true },
  email: { type: String, unique: true },
  noAnggota: { type: String, unique: true },
  tanggalDaftar: { type: Date, default: Date.now }
});

const borrowingSchema = new mongoose.Schema({
  book: { type: mongoose.Schema.Types.ObjectId, ref: 'Book', required: true },
  member: { type: mongoose.Schema.Types.ObjectId, ref: 'Member', required: true },
  tanggalPinjam: { type: Date, default: Date.now },
  tanggalKembali: Date,
  status: { type: String, enum: ['dipinjam', 'dikembalikan', 'terlambat'], default: 'dipinjam' }
});
```

**Soal 2:**

```javascript
// a) Insert 5 buku
await Book.insertMany([
  { judul: "Laskar Pelangi", pengarang: "Andrea Hirata", genre: "fiksi", tahunTerbit: 2005, stok: 10 },
  { judul: "Atomic Habits", pengarang: "James Clear", genre: "nonfiksi", tahunTerbit: 2018, stok: 8 },
  { judul: "Dune", pengarang: "Frank Herbert", genre: "fiksi", tahunTerbit: 2021, stok: 5 },
  { judul: "Sapiens", pengarang: "Yuval Harari", genre: "sejarah", tahunTerbit: 2022, stok: 7 },
  { judul: "Clean Code", pengarang: "Robert Martin", genre: "teknologi", tahunTerbit: 2023, stok: 12 }
]);

// b) Cari buku fiksi tahun > 2020
const books = await Book.find({ genre: "fiksi", tahunTerbit: { $gt: 2020 } });

// c) Kurangi stok saat dipinjam
await Book.findByIdAndUpdate(bookId, { $inc: { stok: -1 } });

// d) Soft delete
await Book.findByIdAndUpdate(bookId, { $set: { isActive: false } });
```

**Soal 3:**

```javascript
const result = await Book.aggregate([
  { $match: { isActive: true } },
  { $group: { _id: "$genre", jumlahBuku: { $sum: 1 } } },
  { $match: { jumlahBuku: { $gt: 5 } } },
  { $sort: { jumlahBuku: -1 } }
]);
```

**Soal 4:**

```javascript
app.get('/api/books', async (req, res) => {
  const { page = 1, limit = 10, genre, search, sort = '-tahunTerbit' } = req.query;
  const filter = { isActive: true };

  if (genre) filter.genre = genre;
  if (search) filter.judul = { $regex: search, $options: 'i' };

  const books = await Book.find(filter)
    .sort(sort)
    .skip((page - 1) * limit)
    .limit(Number(limit));

  const total = await Book.countDocuments(filter);

  res.json({
    success: true,
    data: books,
    pagination: { page: Number(page), limit: Number(limit), total, pages: Math.ceil(total / limit) }
  });
});
```

---

<div style="page-break-after: always;"></div>



# IX. TROUBLESHOOTING & FAQ

## 9.1 Common Errors

### 1. MongoNetworkError: connect ECONNREFUSED

```
MongoNetworkError: connect ECONNREFUSED 127.0.0.1:27017
```

**Penyebab:** MongoDB server tidak berjalan.

**Solusi:**

```bash
# Windows
net start MongoDB

# Linux
sudo systemctl start mongod

# macOS
brew services start mongodb-community

# Cek status
mongosh --eval "db.runCommand({ ping: 1 })"
```

---

### 2. MongoServerError: E11000 duplicate key

```
MongoServerError: E11000 duplicate key error collection: mydb.users index: email_1 dup key: { email: "test@email.com" }
```

**Penyebab:** Mencoba insert data dengan value yang sudah ada pada field unique.

**Solusi:**

```javascript
// Cek dulu sebelum insert
const exists = await User.findOne({ email: data.email });
if (exists) throw new Error('Email sudah terdaftar');

// Atau handle error
try {
  await User.create(data);
} catch (err) {
  if (err.code === 11000) {
    res.status(409).json({ message: 'Data sudah ada' });
  }
}
```

---

### 3. MongooseError: Operation timed out

```
MongooseError: Operation `users.find()` buffering timed out after 10000ms
```

**Penyebab:** Mongoose belum terkoneksi ke database saat query dijalankan.

**Solusi:**

```javascript
// Pastikan connect selesai sebelum listen
const connectDB = async () => {
  await mongoose.connect(process.env.MONGODB_URI);
  console.log('DB Connected');
};

connectDB().then(() => {
  app.listen(PORT, () => console.log(`Server on port ${PORT}`));
});
```

---

### 4. ValidationError

```
ValidationError: User validation failed: email: Path `email` is required.
```

**Penyebab:** Data tidak memenuhi schema validation.

**Solusi:**

```javascript
// Pastikan semua required field terisi
const user = await User.create({
  name: req.body.name,    // required
  email: req.body.email   // required
});

// Atau validasi sebelum create
if (!req.body.email) {
  return res.status(400).json({ message: 'Email wajib diisi' });
}
```

---

### 5. CastError: Cast to ObjectId failed

```
CastError: Cast to ObjectId failed for value "abc123" at path "_id"
```

**Penyebab:** String yang diberikan bukan format ObjectId valid (24 hex characters).

**Solusi:**

```javascript
const mongoose = require('mongoose');

// Validasi sebelum query
if (!mongoose.Types.ObjectId.isValid(req.params.id)) {
  return res.status(400).json({ message: 'ID tidak valid' });
}

const user = await User.findById(req.params.id);
```

---

### 6. MongooseServerSelectionError

```
MongooseServerSelectionError: Could not connect to any servers in your MongoDB Atlas cluster
```

**Penyebab:** IP tidak di-whitelist di Atlas, atau connection string salah.

**Solusi:**

```
1. Buka MongoDB Atlas → Network Access
2. Tambahkan IP address Anda (atau 0.0.0.0/0 untuk development)
3. Pastikan username/password benar
4. Pastikan connection string format benar:
   mongodb+srv://user:password@cluster.mongodb.net/dbname
5. Encode special characters di password (gunakan encodeURIComponent)
```

---

### 7. OverwriteModelError

```
OverwriteModelError: Cannot overwrite `User` model once compiled
```

**Penyebab:** `mongoose.model('User', schema)` dipanggil lebih dari sekali.

**Solusi:**

```javascript
// ❌ Buruk
const User = mongoose.model('User', userSchema); // Dipanggil berkali-kali

// ✅ Baik
const User = mongoose.models.User || mongoose.model('User', userSchema);
```

---

## 9.2 Solutions & Tips

### Connection Best Practices

```javascript
// Retry connection
const connectWithRetry = async (retries = 5) => {
  for (let i = 0; i < retries; i++) {
    try {
      await mongoose.connect(process.env.MONGODB_URI);
      console.log('MongoDB connected');
      return;
    } catch (err) {
      console.log(`Retry ${i + 1}/${retries}...`);
      await new Promise(res => setTimeout(res, 5000));
    }
  }
  console.error('Failed to connect after retries');
  process.exit(1);
};
```

### Debug Mode

```javascript
// Aktifkan debug untuk lihat semua query
mongoose.set('debug', true);

// Custom debug
mongoose.set('debug', (collectionName, method, query, doc) => {
  console.log(`${collectionName}.${method}`, JSON.stringify(query));
});
```

### Memory Management

```javascript
// Untuk data besar, gunakan cursor
const cursor = User.find().cursor();
for await (const user of cursor) {
  // Process satu per satu, hemat memory
}

// Atau stream
User.find().stream()
  .on('data', (doc) => { /* process */ })
  .on('error', (err) => { /* handle */ })
  .on('end', () => { /* done */ });
```

### Slow Query Detection

```javascript
// Monitor slow queries
mongoose.set('debug', (coll, method, query, doc, options) => {
  const start = Date.now();
  // Log jika query > 100ms
  setTimeout(() => {
    const duration = Date.now() - start;
    if (duration > 100) {
      console.warn(`SLOW QUERY: ${coll}.${method} took ${duration}ms`);
    }
  }, 0);
});
```

---

## 9.3 FAQ

### Q1: MongoDB gratis atau berbayar?

**A:** MongoDB Community Edition gratis dan open-source. MongoDB Atlas menyediakan free tier (512MB). Untuk fitur enterprise (advanced security, analytics), perlu lisensi berbayar.

---

### Q2: Kapan sebaiknya pakai MongoDB vs MySQL?

**A:**
- **MongoDB**: Data fleksibel, rapid development, horizontal scaling, real-time apps, content management
- **MySQL**: Data relasional kompleks, butuh ACID strict, financial transactions, reporting kompleks

---

### Q3: Apakah MongoDB bisa digunakan untuk transaksi keuangan?

**A:** Sejak versi 4.0, MongoDB mendukung multi-document ACID transactions. Namun untuk sistem keuangan kritikal, SQL database masih lebih mature dan proven.

---

### Q4: Berapa batas ukuran dokumen MongoDB?

**A:** Maksimal **16MB** per dokumen. Untuk file besar, gunakan **GridFS** yang memecah file menjadi chunks 255KB.

---

### Q5: Apa perbedaan `find()` dan `findOne()`?

**A:**
- `find()`: Mengembalikan array (cursor) dari semua dokumen yang cocok
- `findOne()`: Mengembalikan satu dokumen pertama yang cocok, atau `null`

---

### Q6: Bagaimana cara backup MongoDB?

**A:**

```bash
# Backup
mongodump --uri="mongodb://localhost:27017/mydb" --out=./backup

# Restore
mongorestore --uri="mongodb://localhost:27017/mydb" ./backup/mydb
```

---

### Q7: Apa itu Replica Set?

**A:** Replica Set adalah grup MongoDB server yang menyimpan data yang sama. Terdiri dari 1 Primary (read/write) dan beberapa Secondary (read-only). Jika Primary down, Secondary otomatis dipromosikan (automatic failover).

---

### Q8: Mongoose wajib digunakan?

**A:** Tidak. Mongoose adalah ODM opsional. Bisa menggunakan native MongoDB driver langsung. Mongoose memberikan kemudahan: schema validation, middleware, populate, dll. Untuk aplikasi sederhana atau yang butuh performa maksimal, native driver bisa lebih cocok.

---

### Q9: Bagaimana mengatasi "connection pool exhausted"?

**A:**

```javascript
// Tingkatkan pool size
mongoose.connect(uri, {
  maxPoolSize: 50,  // Default 10
  minPoolSize: 10
});

// Pastikan tidak ada connection leak
// Selalu close connection saat app shutdown
process.on('SIGINT', () => mongoose.connection.close());
```

---

### Q10: Bagaimana cara migrasi dari SQL ke MongoDB?

**A:**
1. Analisis relasi data (tentukan embed vs reference)
2. Redesign schema sesuai access pattern
3. Export data dari SQL (CSV/JSON)
4. Transform data sesuai schema baru
5. Import ke MongoDB (`mongoimport`)
6. Update application code (query syntax)
7. Testing menyeluruh

---

<div style="page-break-after: always;"></div>



# X. REFERENSI & RESOURCES

## 10.1 Dokumentasi Official

| Resource | URL |
|----------|-----|
| MongoDB Documentation | https://www.mongodb.com/docs/ |
| MongoDB Manual | https://www.mongodb.com/docs/manual/ |
| Mongoose Documentation | https://mongoosejs.com/docs/ |
| MongoDB Node.js Driver | https://www.mongodb.com/docs/drivers/node/current/ |
| MongoDB Atlas | https://www.mongodb.com/cloud/atlas |
| MongoDB University (Free Courses) | https://university.mongodb.com/ |

---

## 10.2 Tools Recommendation

### Database Management

| Tool | Deskripsi | Platform |
|------|-----------|----------|
| **MongoDB Compass** | Official GUI untuk MongoDB | Windows, macOS, Linux |
| **MongoDB Shell (mongosh)** | CLI interaktif | All platforms |
| **Studio 3T** | Advanced GUI (free & paid) | Windows, macOS, Linux |
| **Robo 3T** | Lightweight GUI (free) | Windows, macOS, Linux |

### Development Tools

| Tool | Deskripsi |
|------|-----------|
| **Postman** | API testing & documentation |
| **Thunder Client** | REST client extension untuk VS Code |
| **Nodemon** | Auto-restart server saat file berubah |
| **dotenv** | Manage environment variables |
| **Joi / express-validator** | Input validation |
| **morgan** | HTTP request logger |

### VS Code Extensions

| Extension | Fungsi |
|-----------|--------|
| MongoDB for VS Code | Browse & query MongoDB langsung dari VS Code |
| REST Client | Kirim HTTP request dari file `.http` |
| ESLint | JavaScript linting |
| Prettier | Code formatting |

---

## 10.3 Learning Resources

### Kursus Online (Gratis)

1. **MongoDB University** - https://university.mongodb.com/
   - M001: MongoDB Basics
   - M220JS: MongoDB for JavaScript Developers
   - M320: Data Modeling

2. **freeCodeCamp** - MongoDB & Mongoose tutorial di YouTube

3. **The Net Ninja** - MongoDB playlist di YouTube

### Buku Rekomendasi

| Judul | Penulis |
|-------|---------|
| MongoDB: The Definitive Guide | Shannon Bradshaw, Eoin Brazil, Kristina Chodorow |
| Mongoose for Application Development | Simon Holmes |
| Node.js Design Patterns | Mario Casciaro, Luciano Mammino |

### Artikel & Blog

- MongoDB Blog: https://www.mongodb.com/blog
- Dev.to MongoDB tag: https://dev.to/t/mongodb
- Medium MongoDB publications

---

## 10.4 Community Links

| Platform | Link |
|----------|------|
| MongoDB Community Forums | https://www.mongodb.com/community/forums/ |
| Stack Overflow (tag: mongodb) | https://stackoverflow.com/questions/tagged/mongodb |
| Reddit r/mongodb | https://www.reddit.com/r/mongodb/ |
| MongoDB GitHub | https://github.com/mongodb |
| Mongoose GitHub | https://github.com/Automattic/mongoose |
| Discord MongoDB Community | https://discord.gg/mongodb |

---

## Penutup

Laporan ini telah membahas secara komprehensif tentang MongoDB mulai dari konsep dasar NoSQL, instalasi, integrasi dengan Node.js menggunakan Mongoose, operasi CRUD, advanced topics (aggregation, indexing, relationships), best practices, hingga studi kasus pembuatan REST API. Dengan pemahaman materi ini, diharapkan dapat mengimplementasikan MongoDB dalam pengembangan aplikasi web modern secara efektif dan efisien.

---

*Laporan ini disusun sebagai bahan pembelajaran mata kuliah Pemrograman Web / Database Management.*  
*Tahun Akademik 2026*
