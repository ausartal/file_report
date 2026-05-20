# LAPORAN MATERI PEMBELAJARAN
## DATABASE NoSQL - MongoDB dan Integrasi dengan Aplikasi Web

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

## II. INSTALASI DAN KONFIGURASI
- 2.1 Instalasi MongoDB
- 2.2 Konfigurasi Lingkungan Node.js
- 2.3 Konfigurasi Mongoose
- 2.4 Pengujian Koneksi

## III. INTEGRASI DENGAN NODE.JS
- 3.1 Koneksi MongoDB Driver
- 3.2 Koneksi dengan Mongoose
- 3.3 Definisi Schema dan Model
- 3.4 Middleware dan Hooks

## IV. OPERASI CRUD
- 4.1 Operasi Create
- 4.2 Operasi Read
- 4.3 Operasi Update
- 4.4 Operasi Delete
- 4.5 Query Operators dan Filtering

## V. TOPIK LANJUTAN
- 5.1 Aggregation Pipeline
- 5.2 Strategi Indexing
- 5.3 Relationships dan Population
- 5.4 Penanganan Error

## VI. PRAKTIK TERBAIK
- 6.1 Optimasi Performa
- 6.2 Panduan Keamanan
- 6.3 Organisasi Kode
- 6.4 Kesalahan Umum

## VII. STUDI KASUS DAN PROJECT
- 7.1 Struktur Project
- 7.2 Implementasi Lengkap
- 7.3 Kode Sumber

## VIII. SOAL DAN JAWABAN
- 8.1 Soal Konsep
- 8.2 Soal Praktik
- 8.3 Kunci Jawaban

## IX. TROUBLESHOOTING DAN FAQ
- 9.1 Error Umum
- 9.2 Solusi dan Tips
- 9.3 Pertanyaan yang Sering Diajukan

## X. REFERENSI DAN SUMBER DAYA
- 10.1 Dokumentasi Resmi
- 10.2 Rekomendasi Tools
- 10.3 Sumber Pembelajaran
- 10.4 Tautan Komunitas

---

<div style="page-break-after: always;"></div>


# I. PENGENALAN DATABASE NoSQL

## 1.1 Definisi dan Konsep Dasar

### Pengertian NoSQL

NoSQL (Not Only SQL) adalah paradigma database yang dirancang untuk menangani data dalam skala besar dengan struktur yang fleksibel. Berbeda dengan database relasional tradisional, NoSQL tidak menggunakan tabel dengan skema tetap, melainkan menggunakan berbagai model data seperti dokumen, key-value, graph, atau column-family.

### Sejarah Perkembangan NoSQL

Berikut adalah timeline perkembangan teknologi NoSQL:

```
1998 - Carlo Strozzi menciptakan istilah "NoSQL"
2000 - Graph database Neo4j mulai dikembangkan
2007 - Amazon merilis paper tentang Dynamo
2008 - Facebook mengembangkan Cassandra
2009 - MongoDB pertama kali dirilis sebagai open-source
2010 - Istilah "NoSQL" dipopulerkan untuk non-relational databases
2012 - MongoDB mencapai adopsi massal
2015 - NoSQL menjadi standar untuk aplikasi modern
```

### Latar Belakang Kemunculan NoSQL

NoSQL muncul sebagai solusi untuk mengatasi keterbatasan database relasional dalam menghadapi tantangan berikut:

1. **Volume Data Besar** - Pertumbuhan data eksponensial dari web, mobile, dan IoT
2. **Velocity** - Kecepatan data yang masuk sangat tinggi secara real-time
3. **Variety** - Keragaman tipe data (structured, semi-structured, unstructured)
4. **Scalability** - Kebutuhan untuk melakukan horizontal scaling dengan mudah
5. **Flexibility** - Perubahan struktur data yang cepat dalam siklus pengembangan

### CAP Theorem

CAP Theorem adalah prinsip fundamental dalam sistem database terdistribusi yang menyatakan bahwa sistem hanya dapat memenuhi maksimal 2 dari 3 properti berikut:

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

Penjelasan masing-masing properti:

- **Consistency (C)**: Semua node melihat data yang sama pada waktu yang sama
- **Availability (A)**: Setiap request mendapat response (sukses atau gagal)
- **Partition Tolerance (P)**: Sistem tetap berfungsi meskipun ada network partition

Kategori database berdasarkan CAP Theorem:

- **CA**: MySQL, PostgreSQL - Tidak partition tolerant
- **CP**: MongoDB, HBase - Mungkin tidak available saat partition
- **AP**: Cassandra, DynamoDB - Eventually consistent

### Panduan Pemilihan NoSQL vs SQL

**Gunakan NoSQL ketika:**

- Data tidak terstruktur atau semi-terstruktur
- Skema data sering berubah
- Membutuhkan horizontal scaling
- Performa read/write tinggi lebih penting dari konsistensi ketat
- Bekerja dengan big data atau real-time analytics
- Memerlukan rapid development dan iterasi cepat

**Gunakan SQL ketika:**

- Data terstruktur dengan relasi kompleks
- Membutuhkan ACID transactions yang ketat
- Query kompleks dengan JOIN banyak tabel
- Data consistency adalah prioritas utama
- Reporting dan analytics kompleks
- Skema stabil dan terdefinisi dengan baik

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
│  - Sederhana                        │
│  - Tidak perlu ubah aplikasi        │
│                                     │
│  Kekurangan:                        │
│  - Ada limit hardware               │
│  - Mahal                            │
│  - Single point of failure          │
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
│  - Tidak ada limit teoritis         │
│  - Cost-effective                   │
│  - High availability                │
│                                     │
│  Kekurangan:                        │
│  - Kompleksitas lebih tinggi        │
│  - Eventual consistency             │
└────────────────────────────────────┘
```

### ACID vs BASE

**ACID (SQL):**

- **Atomicity**: Transaksi bersifat all-or-nothing
- **Consistency**: Data selalu dalam state valid
- **Isolation**: Transaksi tidak saling mengganggu
- **Durability**: Data tersimpan permanen setelah commit

**BASE (NoSQL):**

- **Basically Available**: Sistem selalu merespons
- **Soft state**: State dapat berubah seiring waktu
- **Eventually consistent**: Konsistensi tercapai setelah beberapa waktu

### Matriks Perbandingan Use Case

| Skenario | SQL | NoSQL | Rekomendasi |
|----------|-----|-------|-------------|
| E-commerce Transactions | Sangat Baik | Baik | SQL (butuh ACID) |
| Product Catalog | Baik | Sangat Baik | NoSQL (flexible schema) |
| User Sessions | Kurang Baik | Sangat Baik | NoSQL (key-value) |
| Financial Reports | Sangat Baik | Baik | SQL (complex queries) |
| Social Media Posts | Baik | Sangat Baik | NoSQL (high write) |
| Real-time Analytics | Kurang Baik | Sangat Baik | NoSQL (speed) |
| Inventory Management | Sangat Baik | Baik | SQL (consistency) |
| IoT Sensor Data | Kurang Baik | Sangat Baik | NoSQL (volume) |
| Content Management | Baik | Sangat Baik | NoSQL (flexibility) |
| Banking Transactions | Sangat Baik | Kurang Baik | SQL (ACID critical) |

---


## 1.3 Kelebihan MongoDB

### 1. Fleksibilitas Schema

MongoDB menggunakan dynamic schema yang memungkinkan dokumen dalam collection yang sama memiliki struktur berbeda.

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

MongoDB mendukung sharding untuk distribusi data ke beberapa server:

```
┌─────────────────────────────────────────┐
│         MongoDB Sharded Cluster          │
├─────────────────────────────────────────┤
│                                          │
│  Client Application                      │
│         |                                │
│    mongos (Router)                       │
│         |                                │
│  ┌──────┴──────┬──────────┬──────────┐  │
│  |             |          |          |  │
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

Replica Sets menyediakan redundancy dan automatic failover:

```
┌─────────────────────────────────────┐
│        Replica Set                   │
├─────────────────────────────────────┤
│                                      │
│     Primary Node                     │
│     (Read/Write)                     │
│          |                           │
│    ┌─────┴─────┐                    │
│    |           |                    │
│ Secondary   Secondary                │
│ (Read Only) (Read Only)              │
│                                      │
│ Auto Failover jika Primary down      │
└─────────────────────────────────────┘
```

### 6. Document-Oriented

Data disimpan dalam format BSON (Binary JSON) yang natural untuk aplikasi:

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

### 1. Penggunaan Memory Tinggi

MongoDB membutuhkan RAM yang besar untuk performa optimal:

- Working set harus fit di memory
- Indexing memakan banyak memory
- Tidak efisien untuk dataset yang sangat besar dengan RAM terbatas

**Solusi:**
- Gunakan sharding untuk distribusi data
- Optimasi indexes
- Upgrade RAM server

### 2. Kompleksitas JOIN

MongoDB tidak mendukung JOIN seperti SQL. Alternatif yang tersedia:

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
// Data terpisah, memerlukan multiple queries
// Collection: users
{ "_id": 1, "name": "Alice" }

// Collection: orders
{ "_id": 101, "user_id": 1, "product": "Laptop" }

// Memerlukan 2 queries atau $lookup
```

### 3. Keterbatasan Transaksi

Sebelum MongoDB 4.0, tidak tersedia multi-document transactions:

- Single document operations bersifat atomic
- Multi-document transactions memiliki overhead performa
- Tidak se-mature SQL transactions

### 4. Duplikasi Data

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

### 5. Overhead Penyimpanan

Format BSON dan indexing membutuhkan storage lebih besar dibanding SQL.

### 6. Kurva Pembelajaran

- Paradigma berbeda dari SQL
- Perlu memahami kapan menggunakan embed vs reference
- Sintaks query berbeda

---

## 1.5 Karakteristik MongoDB

### 1. Document-Oriented Database

MongoDB menyimpan data dalam bentuk dokumen BSON (Binary JSON):

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

**Perbandingan BSON vs JSON:**

| Aspek | JSON | BSON |
|-------|------|------|
| Format | Text-based | Binary |
| Ukuran | Lebih besar | Lebih kecil |
| Kecepatan | Parsing lebih lambat | Parsing lebih cepat |
| Tipe Data | Terbatas (string, number, boolean, null, array, object) | Extended (Date, ObjectId, Binary, Regex, dll) |
| Keterbacaan | Human-readable | Machine-readable |

### 2. Fleksibilitas Schema

Dynamic Schema memungkinkan evolusi data tanpa migration:

```javascript
// Version 1 - Simple user
{
  "name": "Alice",
  "email": "alice@example.com"
}

// Version 2 - Penambahan phone (tidak perlu ALTER TABLE)
{
  "name": "Bob",
  "email": "bob@example.com",
  "phone": "+62812345678"
}

// Version 3 - Penambahan nested address
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

### 3. Kemampuan Indexing

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

**Diagram Struktur Index:**

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
│           |                          │
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

Replica Set menyediakan data redundancy dan high availability:

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
│      |              |                    │
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

- **High Availability**: Automatic failover
- **Data Redundancy**: Multiple copies
- **Read Scalability**: Read dari secondary
- **Disaster Recovery**: Backup otomatis

### 5. Sharding

Sharding adalah metode distribusi data secara horizontal ke beberapa mesin:

**Arsitektur Sharded Cluster:**

```
┌────────────────────────────────────────────┐
│       MongoDB Sharded Cluster               │
├────────────────────────────────────────────┤
│                                             │
│  Application                                │
│       |                                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐    │
│  │ mongos  │  │ mongos  │  │ mongos  │    │
│  │(Router) │  │(Router) │  │(Router) │    │
│  └────┬────┘  └────┬────┘  └────┬────┘    │
│       └────────────┼────────────┘          │
│                    |                        │
│         Config Servers (Metadata)           │
│              ┌──────────┐                   │
│              │ Config   │                   │
│              │ Replica  │                   │
│              │   Set    │                   │
│              └─────┬────┘                   │
│                    |                        │
│  ┌─────────┬──────┴──────┬─────────┐      │
│  |         |             |         |      │
│ Shard 1  Shard 2      Shard 3   Shard 4    │
│ (0-25%)  (26-50%)    (51-75%)  (76-100%)   │
│ Replica  Replica     Replica   Replica      │
│   Set      Set         Set       Set        │
│                                             │
└────────────────────────────────────────────┘
```

**Strategi Shard Key:**

```javascript
// Range-based sharding
sh.shardCollection("mydb.users", { user_id: 1 })

// Hash-based sharding (distribusi lebih merata)
sh.shardCollection("mydb.users", { user_id: "hashed" })

// Compound shard key
sh.shardCollection("mydb.orders", { customer_id: 1, order_date: 1 })
```

**Keuntungan Sharding:**

- **Horizontal Scalability**: Menambah server untuk meningkatkan kapasitas
- **Better Performance**: Parallel processing
- **No Single Point of Failure**: Distributed system

---

<div style="page-break-after: always;"></div>



# II. INSTALASI DAN KONFIGURASI

## 2.1 Instalasi MongoDB

### Instalasi MongoDB di Windows

**Langkah 1: Unduh MongoDB**

1. Kunjungi https://www.mongodb.com/try/download/community
2. Pilih versi terbaru untuk Windows
3. Unduh file installer berformat `.msi`

**Langkah 2: Proses Instalasi**

```
1. Jalankan file .msi installer
2. Pilih "Complete" installation
3. Install MongoDB as a Service (direkomendasikan)
4. Install MongoDB Compass (GUI tool)
5. Klik "Install"
```

**Langkah 3: Verifikasi Instalasi**

```bash
# Buka Command Prompt
mongod --version

# Output yang diharapkan:
# db version v7.0.0
# Build Info: ...
```

**Langkah 4: Menjalankan MongoDB**

```bash
# MongoDB sudah berjalan sebagai service
# Cek status:
net start MongoDB

# Akses MongoDB Shell:
mongosh

# Output yang diharapkan:
# Current Mongosh Log ID: ...
# Connecting to: mongodb://127.0.0.1:27017
# test>
```

### Instalasi MongoDB di Linux (Ubuntu)

```bash
# Import public key
wget -qO - https://www.mongodb.org/static/pgp/server-7.0.asc | sudo apt-key add -

# Buat list file
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# Update package database
sudo apt-get update

# Install MongoDB
sudo apt-get install -y mongodb-org

# Jalankan MongoDB
sudo systemctl start mongod

# Aktifkan auto-start
sudo systemctl enable mongod

# Verifikasi
mongod --version
```

### Instalasi MongoDB di macOS

```bash
# Install menggunakan Homebrew
brew tap mongodb/brew
brew install mongodb-community@7.0

# Jalankan MongoDB
brew services start mongodb-community@7.0

# Verifikasi
mongod --version
```

### MongoDB Atlas (Cloud Database)

**Keuntungan MongoDB Atlas:**

- Fully managed (tanpa maintenance server)
- Free tier tersedia (512MB storage)
- Automatic backups
- Global deployment
- Built-in security

**Langkah Konfigurasi MongoDB Atlas:**

**Langkah 1: Buat Akun**

1. Kunjungi https://www.mongodb.com/cloud/atlas
2. Daftar dengan email atau akun Google
3. Verifikasi email

**Langkah 2: Buat Cluster**

```
1. Klik "Build a Database"
2. Pilih "FREE" tier (M0 Sandbox)
3. Pilih Cloud Provider (AWS/GCP/Azure)
4. Pilih Region (Singapore untuk Indonesia)
5. Cluster Name: "MyFirstCluster"
6. Klik "Create Cluster"
```

**Langkah 3: Konfigurasi Database Access**

```
1. Database Access → Add New Database User
2. Username: admin
3. Password: [generate secure password]
4. Database User Privileges: Read and write to any database
5. Add User
```

**Langkah 4: Konfigurasi Network Access**

```
1. Network Access → Add IP Address
2. Pilih "Allow Access from Anywhere" (0.0.0.0/0)
   (Hanya untuk development, production gunakan specific IP)
3. Confirm
```

**Langkah 5: Dapatkan Connection String**

```
1. Clusters → Connect
2. Pilih "Connect your application"
3. Driver: Node.js
4. Version: 5.5 or later
5. Salin connection string:

mongodb+srv://admin:<password>@myfirstcluster.xxxxx.mongodb.net/?retryWrites=true&w=majority
```

---

## 2.2 Konfigurasi Lingkungan Node.js

### Instalasi Node.js

**Windows:**

```
1. Unduh dari https://nodejs.org/
2. Pilih versi LTS
3. Jalankan installer
4. Ikuti wizard installation
```

**Verifikasi Instalasi:**

```bash
node --version
# v20.11.0

npm --version
# 10.2.4
```

### Membuat Project

```bash
# Buat folder project
mkdir mongodb-project
cd mongodb-project

# Inisialisasi npm
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

### Instalasi Dependencies

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

**package.json setelah instalasi:**

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

### Konfigurasi Environment Variables

**Buat file .env:**

```bash
# .env
MONGODB_URI=mongodb://localhost:27017/mydb
# atau untuk Atlas:
# MONGODB_URI=mongodb+srv://admin:password@cluster.xxxxx.mongodb.net/mydb

PORT=3000
NODE_ENV=development
```

**Buat file .gitignore:**

```
node_modules/
.env
*.log
```

### Struktur Project

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

### Koneksi Dasar

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

### Koneksi dengan Options Lengkap

```javascript
const mongoose = require('mongoose');

const options = {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  serverSelectionTimeoutMS: 5000,
  socketTimeoutMS: 45000,
  family: 4, // Gunakan IPv4
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

// Event koneksi
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

### Format Connection String

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

**Komponen Connection String:**

```
mongodb+srv://username:password@host:port/database?options

├── Protocol: mongodb:// atau mongodb+srv://
├── Credentials: username:password@
├── Host: cluster.mongodb.net
├── Port: :27017 (opsional untuk srv)
├── Database: /database_name
└── Options: ?retryWrites=true&w=majority
```

---

## 2.4 Pengujian Koneksi

### Script Pengujian

**test-connection.js:**

```javascript
const mongoose = require('mongoose');
require('dotenv').config();

const testConnection = async () => {
  try {
    console.log('Mencoba koneksi ke MongoDB...');
    console.log('URI:', process.env.MONGODB_URI.replace(/\/\/.*@/, '//***:***@'));
    
    await mongoose.connect(process.env.MONGODB_URI);
    
    console.log('[BERHASIL] Koneksi MongoDB berhasil!');
    console.log('Database:', mongoose.connection.db.databaseName);
    console.log('Host:', mongoose.connection.host);
    console.log('Port:', mongoose.connection.port);
    
    // Test operasi write
    const testCollection = mongoose.connection.collection('test');
    await testCollection.insertOne({ test: 'Hello MongoDB', timestamp: new Date() });
    console.log('[BERHASIL] Write test berhasil!');
    
    // Test operasi read
    const doc = await testCollection.findOne({ test: 'Hello MongoDB' });
    console.log('[BERHASIL] Read test berhasil!');
    console.log('Document:', doc);
    
    // Cleanup
    await testCollection.deleteOne({ test: 'Hello MongoDB' });
    console.log('[BERHASIL] Delete test berhasil!');
    
    await mongoose.connection.close();
    console.log('Koneksi ditutup');
    
  } catch (error) {
    console.error('[GAGAL] Koneksi gagal:', error.message);
    process.exit(1);
  }
};

testConnection();
```

**Menjalankan test:**

```bash
node test-connection.js
```

**Output yang Diharapkan:**

```
Mencoba koneksi ke MongoDB...
URI: mongodb://***:***@localhost:27017/mydb
[BERHASIL] Koneksi MongoDB berhasil!
Database: mydb
Host: localhost
Port: 27017
[BERHASIL] Write test berhasil!
[BERHASIL] Read test berhasil!
Document: { _id: ..., test: 'Hello MongoDB', timestamp: 2026-05-19T... }
[BERHASIL] Delete test berhasil!
Koneksi ditutup
```

### Setup Aplikasi Utama

**index.js:**

```javascript
const express = require('express');
const connectDB = require('./config/database');
require('dotenv').config();

const app = express();

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Koneksi ke MongoDB
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

**Menjalankan aplikasi:**

```bash
npm start
# atau untuk development:
npm run dev
```

### Troubleshooting Masalah Koneksi

**Error Umum:**

**1. MongoNetworkError: failed to connect**

```
Penyebab: MongoDB server tidak berjalan
Solusi: 
- Periksa apakah MongoDB service berjalan
- Windows: net start MongoDB
- Linux: sudo systemctl start mongod
```

**2. MongoServerError: Authentication failed**

```
Penyebab: Username/password salah
Solusi:
- Periksa credentials di file .env
- Pastikan user sudah dibuat di database
```

**3. MongooseServerSelectionError: connect ECONNREFUSED**

```
Penyebab: Connection string salah atau firewall memblokir
Solusi:
- Periksa format connection string
- Periksa pengaturan firewall
- Untuk Atlas, periksa Network Access whitelist
```

**4. MongoParseError: Invalid connection string**

```
Penyebab: Format connection string tidak valid
Solusi:
- Periksa format: mongodb://host:port/database
- Encode special characters di password
```

**Tips Debugging:**

```javascript
// Aktifkan mongoose debug mode
mongoose.set('debug', true);

// Log semua queries
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

**Instalasi MongoDB Driver:**

```bash
npm install mongodb
```

### Koneksi Dasar

**db.js:**

```javascript
const { MongoClient } = require('mongodb');

// Connection URI
const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri);

async function connect() {
  try {
    // Koneksi ke MongoDB
    await client.connect();
    console.log('Connected to MongoDB');
    
    // Akses database
    const database = client.db('mydb');
    
    // Akses collection
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

// Opsi connection pool
const options = {
  maxPoolSize: 10,        // Maksimum koneksi
  minPoolSize: 5,         // Minimum koneksi
  maxIdleTimeMS: 10000,   // Tutup koneksi idle setelah 10 detik
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

**Penggunaan:**

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

### Mengapa Menggunakan Mongoose?

Mongoose adalah ODM (Object Data Modeling) library yang menyediakan:

- **Schema validation** - Struktur data yang jelas dan tervalidasi
- **Type casting** - Konversi tipe data otomatis
- **Query building** - Chainable query API
- **Middleware** - Pre/post hooks
- **Virtuals** - Computed properties
- **Population** - Resolusi referensi otomatis

### Koneksi Dasar Mongoose

```javascript
const mongoose = require('mongoose');

// Koneksi sederhana
mongoose.connect('mongodb://localhost:27017/mydb')
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.error('Connection error:', err));
```

### Konfigurasi Koneksi Lanjutan

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
      console.log('Database connected successfully');
    })
    .catch((err) => {
      console.error('Database connection error:', err);
      process.exit(1);
    });
    
    // Logging untuk development
    if (process.env.NODE_ENV === 'development') {
      mongoose.set('debug', true);
    }
    
    // Event koneksi
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

// Database primer
const db1 = mongoose.createConnection('mongodb://localhost:27017/db1');

// Database sekunder
const db2 = mongoose.createConnection('mongodb://localhost:27017/db2');

// Definisi model untuk masing-masing koneksi
const User = db1.model('User', userSchema);
const Product = db2.model('Product', productSchema);

module.exports = { User, Product };
```

---

## 3.3 Definisi Schema dan Model

### Schema Dasar

```javascript
const mongoose = require('mongoose');

// Definisi schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number,
  isActive: Boolean,
  createdAt: Date
});

// Pembuatan model
const User = mongoose.model('User', userSchema);

module.exports = User;
```

### Schema dengan Type Definitions

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  // Tipe String
  name: {
    type: String,
    required: true,
    trim: true,
    minlength: 3,
    maxlength: 50
  },
  
  // Email dengan validasi
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

### Tipe Data Schema

| Tipe | Deskripsi | Contoh |
|------|-----------|--------|
| String | Data teks | `name: String` |
| Number | Data numerik | `age: Number` |
| Date | Tanggal/waktu | `createdAt: Date` |
| Boolean | true/false | `isActive: Boolean` |
| ObjectId | MongoDB ID | `userId: mongoose.Schema.Types.ObjectId` |
| Array | Daftar nilai | `tags: [String]` |
| Mixed | Tipe apapun | `data: mongoose.Schema.Types.Mixed` |
| Buffer | Data binary | `file: Buffer` |
| Map | Pasangan key-value | `metadata: Map` |
| Decimal128 | Angka presisi tinggi | `price: mongoose.Schema.Types.Decimal128` |

### Validasi Schema

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

### Validasi Kustom

```javascript
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    validate: {
      validator: async function(username) {
        // Periksa apakah username sudah ada
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
        // Password harus mengandung huruf besar, kecil, angka, karakter khusus
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

### Opsi Schema

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String
}, {
  // Opsi
  timestamps: true,           // Menambahkan createdAt dan updatedAt
  versionKey: false,          // Menghapus field __v
  collection: 'users',        // Nama collection kustom
  strict: true,               // Hanya simpan field yang ada di schema
  strictQuery: false,         // Izinkan query pada field di luar schema
  toJSON: { virtuals: true }, // Sertakan virtuals dalam JSON
  toObject: { virtuals: true } // Sertakan virtuals dalam Object
});
```

---


## 3.4 Middleware dan Hooks

### Pengertian Middleware

Middleware (disebut juga hooks) adalah fungsi yang dijalankan pada tahap tertentu dalam lifecycle dokumen. Mongoose mendukung middleware untuk operasi berikut:

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

Pre middleware dijalankan sebelum operasi dilaksanakan.

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
  
  // Set createdAt jika belum ada
  if (!this.createdAt) {
    this.createdAt = new Date();
  }
  
  next();
});

// Pre-save dengan async/await
userSchema.pre('save', async function(next) {
  // Hash password sebelum menyimpan
  if (this.isModified('password')) {
    const bcrypt = require('bcrypt');
    this.password = await bcrypt.hash(this.password, 10);
  }
  next();
});
```

### Post Middleware

Post middleware dijalankan setelah operasi selesai.

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

### Contoh Praktis

**1. Hashing Password:**

```javascript
const bcrypt = require('bcrypt');

userSchema.pre('save', async function(next) {
  // Hanya hash jika password dimodifikasi
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

// Method untuk membandingkan password
userSchema.methods.comparePassword = async function(candidatePassword) {
  return await bcrypt.compare(candidatePassword, this.password);
};
```

**2. Pembuatan Slug:**

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

// Override remove untuk soft delete
userSchema.pre('remove', function(next) {
  this.deletedAt = new Date();
  this.save();
  next();
});

// Filter dokumen yang sudah dihapus
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

Virtuals adalah properties yang tidak disimpan di database tetapi dapat diakses seperti field biasa.

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

// Penggunaan
const user = new User({ firstName: 'John', lastName: 'Doe' });
console.log(user.fullName); // "John Doe"

user.fullName = 'Jane Smith';
console.log(user.firstName); // "Jane"
console.log(user.lastName);  // "Smith"
```

### Instance Methods

Methods yang dapat dipanggil pada document instance.

```javascript
userSchema.methods.getPublicProfile = function() {
  return {
    id: this._id,
    name: this.name,
    email: this.email
    // password tidak disertakan
  };
};

userSchema.methods.isAdmin = function() {
  return this.role === 'admin';
};

// Penggunaan
const user = await User.findById(userId);
const profile = user.getPublicProfile();
if (user.isAdmin()) {
  // Logika admin
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

// Penggunaan
const user = await User.findByEmail('john@example.com');
const activeUsers = await User.findActive();
const newUser = await User.createWithDefaults({ name: 'Alice', email: 'alice@example.com' });
```

### Query Helpers

Custom query methods yang dapat di-chain.

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

// Penggunaan
const users = await User
  .find()
  .byAge(25)
  .active()
  .sortByName();
```

### Contoh Lengkap

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

**Penggunaan:**

```javascript
// Membuat user (password akan di-hash otomatis)
const user = await User.create({
  username: 'johndoe',
  email: 'john@example.com',
  password: 'SecurePass123',
  firstName: 'John',
  lastName: 'Doe'
});

// Mendapatkan full name (virtual)
console.log(user.fullName); // "John Doe"

// Membandingkan password
const isMatch = await user.comparePassword('SecurePass123');

// Update last login
await user.updateLastLogin();

// Mencari berdasarkan email (static method)
const foundUser = await User.findByEmail('john@example.com');

// Query active users
const activeUsers = await User.find().active();
```

---

<div style="page-break-after: always;"></div>



# IV. OPERASI CRUD

## 4.1 Operasi Create

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

// Metode 1: Buat instance lalu simpan
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

// Metode 2: Menggunakan create()
async function createUserMethod2() {
  const user = await User.create({
    name: 'Bob',
    email: 'bob@example.com',
    age: 30
  });
  
  console.log('User created:', user._id);
  return user;
}

// Metode 3: Membuat beberapa dokumen sekaligus
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

// Dengan opsi
async function bulkInsertWithOptions() {
  const users = [
    { name: 'User 1', email: 'user1@example.com' },
    { name: 'User 2', email: 'duplicate@example.com' }, // Duplikat
    { name: 'User 3', email: 'user3@example.com' }
  ];
  
  try {
    const result = await User.insertMany(users, {
      ordered: false,  // Lanjutkan meskipun ada error
      rawResult: true  // Kembalikan hasil lengkap
    });
    console.log('Inserted:', result.insertedCount);
  } catch (error) {
    console.error('Beberapa dokumen gagal:', error.writeErrors);
  }
}
```

### Penanganan Error pada Create

```javascript
async function createWithErrorHandling() {
  try {
    const user = await User.create({
      name: 'Test User',
      email: 'invalid-email',  // Format tidak valid
      age: 15  // Di bawah minimum
    });
  } catch (error) {
    if (error.name === 'ValidationError') {
      // Error validasi
      Object.keys(error.errors).forEach(key => {
        console.error(`${key}: ${error.errors[key].message}`);
      });
    } else if (error.code === 11000) {
      // Error duplicate key
      console.error('Email sudah terdaftar');
    } else {
      console.error('Error tidak diketahui:', error);
    }
  }
}
```

### Contoh Praktis

**1. Registrasi User:**

```javascript
const bcrypt = require('bcrypt');

async function registerUser(userData) {
  try {
    // Periksa apakah email sudah ada
    const existingUser = await User.findOne({ email: userData.email });
    if (existingUser) {
      throw new Error('Email sudah terdaftar');
    }
    
    // Hash password
    const hashedPassword = await bcrypt.hash(userData.password, 10);
    
    // Buat user
    const user = await User.create({
      name: userData.name,
      email: userData.email,
      password: hashedPassword,
      role: 'user',
      isActive: true,
      createdAt: new Date()
    });
    
    // Kembalikan tanpa password
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
```

**2. Create dengan Nested Documents:**

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
  // Hitung total
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
```

**3. Bulk Create dengan Transaction:**

```javascript
async function createUsersWithTransaction(usersData) {
  const session = await mongoose.startSession();
  session.startTransaction();
  
  try {
    // Buat users
    const users = await User.create(usersData, { session });
    
    // Buat audit log
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
    // Rollback jika terjadi error
    await session.abortTransaction();
    console.error('Transaction aborted:', error);
    throw error;
    
  } finally {
    session.endSession();
  }
}
```

---

## 4.2 Operasi Read

### findOne() - Native Driver

```javascript
async function findOneExample() {
  const client = new MongoClient('mongodb://localhost:27017');
  
  try {
    await client.connect();
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    // Cari berdasarkan field
    const user = await collection.findOne({ email: 'alice@example.com' });
    console.log('Found user:', user);
    
    // Cari berdasarkan ID
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
    
    // Cari semua
    const allUsers = await collection.find().toArray();
    
    // Cari dengan filter
    const adults = await collection.find({ age: { $gte: 18 } }).toArray();
    
    // Cari dengan projection (pilih field)
    const names = await collection.find(
      {},
      { projection: { name: 1, email: 1, _id: 0 } }
    ).toArray();
    
    // Cari dengan sort
    const sorted = await collection.find()
      .sort({ age: -1 })
      .toArray();
    
    // Cari dengan limit
    const limited = await collection.find()
      .limit(10)
      .toArray();
    
    // Cari dengan skip (pagination)
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
// Cari berdasarkan field
const user = await User.findOne({ email: 'alice@example.com' });

// Cari berdasarkan ID
const userById = await User.findById('664a1b2c3d4e5f6g7h8i9j0k');

// Cari dengan select
const userWithoutPassword = await User.findOne({ email: 'alice@example.com' })
  .select('-password');

// Cari dengan beberapa kondisi
const user = await User.findOne({
  email: 'alice@example.com',
  isActive: true
});

// Cari atau null
const user = await User.findOne({ email: 'notfound@example.com' });
if (!user) {
  console.log('User tidak ditemukan');
}
```

### find() - Mongoose

```javascript
// Cari semua
const allUsers = await User.find();

// Cari dengan filter
const activeUsers = await User.find({ isActive: true });

// Cari dengan beberapa kondisi
const users = await User.find({
  age: { $gte: 18, $lte: 65 },
  role: 'user'
});

// Cari dengan select (projection)
const users = await User.find()
  .select('name email -_id');

// Cari dengan sort
const users = await User.find()
  .sort({ createdAt: -1 });

// Cari dengan limit
const users = await User.find()
  .limit(10);

// Cari dengan pagination
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
// $eq - Sama dengan
await User.find({ age: { $eq: 25 } });

// $ne - Tidak sama dengan
await User.find({ role: { $ne: 'admin' } });

// $gt - Lebih besar dari
await User.find({ age: { $gt: 18 } });

// $gte - Lebih besar atau sama dengan
await User.find({ age: { $gte: 18 } });

// $lt - Kurang dari
await User.find({ age: { $lt: 65 } });

// $lte - Kurang dari atau sama dengan
await User.find({ age: { $lte: 65 } });

// $in - Dalam array
await User.find({ role: { $in: ['user', 'moderator'] } });

// $nin - Tidak dalam array
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

// $nor - Tidak satupun
await User.find({
  $nor: [
    { status: 'banned' },
    { status: 'suspended' }
  ]
});
```

**Element Operators:**

```javascript
// $exists - Field ada
await User.find({ phone: { $exists: true } });

// $type - Tipe field
await User.find({ age: { $type: 'number' } });
```

**Array Operators:**

```javascript
// $all - Mengandung semua elemen
await User.find({ tags: { $all: ['javascript', 'nodejs'] } });

// $elemMatch - Elemen array cocok
await Order.find({
  items: {
    $elemMatch: { quantity: { $gt: 5 }, price: { $lt: 100 } }
  }
});

// $size - Ukuran array
await User.find({ tags: { $size: 3 } });
```

**String Operators:**

```javascript
// $regex - Regular expression
await User.find({ name: { $regex: /^John/, $options: 'i' } });

// Pencarian case-insensitive
await User.find({ email: { $regex: 'gmail.com$', $options: 'i' } });
```

### Query Lanjutan

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
```

**2. Pencarian:**

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
```

**3. Filter dengan Beberapa Kondisi:**

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
```



---

## 4.3 Operasi Update

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

**$set - Menetapkan nilai field:**

```javascript
await User.updateOne(
  { _id: userId },
  { $set: { name: 'New Name', email: 'new@example.com' } }
);
```

**$unset - Menghapus field:**

```javascript
await User.updateOne(
  { _id: userId },
  { $unset: { phone: '' } }
);
```

**$inc - Menambah/mengurangi angka:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $inc: { stock: -1, sold: 1 } }
);
```

**$mul - Mengalikan:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $mul: { price: 1.1 } }  // Naikkan harga 10%
);
```

**$min - Update jika nilai baru lebih kecil:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $min: { lowestPrice: 100 } }
);
```

**$max - Update jika nilai baru lebih besar:**

```javascript
await Product.updateOne(
  { _id: productId },
  { $max: { highestPrice: 1000 } }
);
```

**$rename - Mengubah nama field:**

```javascript
await User.updateMany(
  {},
  { $rename: { 'phone': 'phoneNumber' } }
);
```

**$currentDate - Menetapkan tanggal saat ini:**

```javascript
await User.updateOne(
  { _id: userId },
  { $currentDate: { lastModified: true, lastLogin: { $type: 'date' } } }
);
```

### Array Update Operators

**$push - Menambahkan ke array:**

```javascript
await User.updateOne(
  { _id: userId },
  { $push: { tags: 'javascript' } }
);

// Push beberapa elemen
await User.updateOne(
  { _id: userId },
  { $push: { tags: { $each: ['nodejs', 'mongodb'] } } }
);

// Push dengan sort dan limit
await User.updateOne(
  { _id: userId },
  { 
    $push: { 
      scores: { 
        $each: [85, 90],
        $sort: -1,
        $slice: 5
      } 
    } 
  }
);
```

**$pull - Menghapus dari array:**

```javascript
await User.updateOne(
  { _id: userId },
  { $pull: { tags: 'javascript' } }
);

// Pull dengan kondisi
await Order.updateOne(
  { _id: orderId },
  { $pull: { items: { quantity: 0 } } }
);
```

**$pop - Menghapus elemen pertama atau terakhir:**

```javascript
await User.updateOne(
  { _id: userId },
  { $pop: { tags: 1 } }  // Hapus elemen terakhir (-1 untuk pertama)
);
```

**$addToSet - Menambahkan jika belum ada:**

```javascript
await User.updateOne(
  { _id: userId },
  { $addToSet: { tags: 'javascript' } }
);

// Menambahkan beberapa elemen unik
await User.updateOne(
  { _id: userId },
  { $addToSet: { tags: { $each: ['nodejs', 'mongodb'] } } }
);
```

**$ (positional) - Update elemen array tertentu:**

```javascript
await Order.updateOne(
  { _id: orderId, 'items.product': 'Laptop' },
  { $set: { 'items.$.quantity': 2 } }
);
```

**$[] (all positional) - Update semua elemen array:**

```javascript
await Order.updateOne(
  { _id: orderId },
  { $set: { 'items.$[].discount': 10 } }
);
```

**$[element] (filtered positional) - Update elemen yang cocok:**

```javascript
await Order.updateOne(
  { _id: orderId },
  { $set: { 'items.$[elem].discount': 20 } },
  { arrayFilters: [{ 'elem.price': { $gte: 100 } }] }
);
```

### Metode Update Mongoose

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
  { new: true }  // Kembalikan dokumen yang sudah di-update
);
console.log('Updated user:', user);
```

**findOneAndUpdate():**

```javascript
const user = await User.findOneAndUpdate(
  { email: 'alice@example.com' },
  { $set: { age: 26 } },
  { 
    new: true,           // Kembalikan dokumen yang sudah di-update
    runValidators: true  // Jalankan schema validators
  }
);
```

**Metode save():**

```javascript
const user = await User.findById(userId);
user.name = 'New Name';
user.age = 26;
await user.save();  // Memicu middleware
```

### Contoh Praktis

**1. Update Profil User:**

```javascript
async function updateUserProfile(userId, updates) {
  try {
    const allowedUpdates = ['name', 'email', 'phone', 'address'];
    const updateData = {};
    
    // Filter field yang diizinkan
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
      throw new Error('User tidak ditemukan');
    }
    
    return user;
    
  } catch (error) {
    throw error;
  }
}
```

**2. Increment Views Produk:**

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

**3. Menambahkan Komentar ke Post:**

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

**4. Update Status Order:**

```javascript
async function updateOrderStatus(orderId, newStatus) {
  const validStatuses = ['pending', 'processing', 'shipped', 'delivered', 'cancelled'];
  
  if (!validStatuses.includes(newStatus)) {
    throw new Error('Status tidak valid');
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

## 4.4 Operasi Delete

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
    
    const result = await collection.deleteMany({ isActive: false });
    console.log('Deleted:', result.deletedCount);
    
  } finally {
    await client.close();
  }
}
```

### Metode Delete Mongoose

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
  console.log('User tidak ditemukan');
}
```

**findOneAndDelete():**

```javascript
const user = await User.findOneAndDelete({ email: 'alice@example.com' });
console.log('Deleted:', user);
```

### Soft Delete

Soft delete tidak menghapus data secara permanen, hanya menandai sebagai deleted.

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

// Middleware untuk memfilter dokumen yang sudah dihapus
userSchema.pre(/^find/, function(next) {
  this.where({ isDeleted: { $ne: true } });
  next();
});

const User = mongoose.model('User', userSchema);
```

**Implementasi Soft Delete:**

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

// Memulihkan user yang dihapus
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

// Mencari termasuk yang sudah dihapus
async function findAllIncludingDeleted() {
  return await User.find().where('isDeleted').in([true, false]);
}
```

### Cascade Delete

Menghapus dokumen terkait ketika parent dihapus.

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

// Cascade delete posts ketika user dihapus
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

### Contoh Praktis

**1. Delete User dengan Validasi:**

```javascript
async function deleteUser(userId, requesterId) {
  try {
    // Periksa apakah user ada
    const user = await User.findById(userId);
    if (!user) {
      throw new Error('User tidak ditemukan');
    }
    
    // Periksa izin
    const requester = await User.findById(requesterId);
    if (requester.role !== 'admin' && userId !== requesterId) {
      throw new Error('Tidak memiliki izin');
    }
    
    // Hapus user
    await User.findByIdAndDelete(userId);
    
    // Hapus data terkait
    await Post.deleteMany({ author: userId });
    await Comment.deleteMany({ user: userId });
    
    return { message: 'User berhasil dihapus' };
    
  } catch (error) {
    throw error;
  }
}
```

**2. Bulk Delete dengan Kondisi:**

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

**3. Delete dengan Transaction:**

```javascript
async function deleteOrderWithTransaction(orderId) {
  const session = await mongoose.startSession();
  session.startTransaction();
  
  try {
    // Cari order
    const order = await Order.findById(orderId).session(session);
    if (!order) {
      throw new Error('Order tidak ditemukan');
    }
    
    // Kembalikan stok produk
    for (const item of order.items) {
      await Product.findByIdAndUpdate(
        item.productId,
        { $inc: { stock: item.quantity } },
        { session }
      );
    }
    
    // Hapus order
    await Order.findByIdAndDelete(orderId).session(session);
    
    // Commit transaction
    await session.commitTransaction();
    console.log('Order dihapus dan stok dikembalikan');
    
  } catch (error) {
    await session.abortTransaction();
    throw error;
  } finally {
    session.endSession();
  }
}
```

---

## 4.5 Query Operators dan Filtering

### Ringkasan Comparison Operators

| Operator | Deskripsi | Contoh |
|----------|-----------|--------|
| `$eq` | Sama dengan | `{ age: { $eq: 25 } }` |
| `$ne` | Tidak sama dengan | `{ age: { $ne: 25 } }` |
| `$gt` | Lebih besar dari | `{ age: { $gt: 18 } }` |
| `$gte` | Lebih besar atau sama | `{ age: { $gte: 18 } }` |
| `$lt` | Kurang dari | `{ age: { $lt: 65 } }` |
| `$lte` | Kurang dari atau sama | `{ age: { $lte: 65 } }` |
| `$in` | Dalam array | `{ role: { $in: ['user', 'admin'] } }` |
| `$nin` | Tidak dalam array | `{ status: { $nin: ['banned'] } }` |

### Ringkasan Logical Operators

| Operator | Deskripsi | Contoh |
|----------|-----------|--------|
| `$and` | Semua kondisi benar | `{ $and: [{ age: { $gte: 18 } }, { age: { $lte: 65 } }] }` |
| `$or` | Salah satu kondisi benar | `{ $or: [{ role: 'admin' }, { role: 'moderator' }] }` |
| `$not` | Membalik kondisi | `{ age: { $not: { $lt: 18 } } }` |
| `$nor` | Tidak satupun benar | `{ $nor: [{ status: 'banned' }, { status: 'suspended' }] }` |

### Ringkasan Element Operators

| Operator | Deskripsi | Contoh |
|----------|-----------|--------|
| `$exists` | Field ada | `{ phone: { $exists: true } }` |
| `$type` | Tipe field | `{ age: { $type: 'number' } }` |

### Ringkasan Array Operators

| Operator | Deskripsi | Contoh |
|----------|-----------|--------|
| `$all` | Mengandung semua | `{ tags: { $all: ['js', 'node'] } }` |
| `$elemMatch` | Elemen array cocok | `{ items: { $elemMatch: { qty: { $gt: 5 } } } }` |
| `$size` | Ukuran array | `{ tags: { $size: 3 } }` |

### Contoh Query Kompleks

**1. Advanced Filtering:**

```javascript
async function advancedUserSearch(filters) {
  const query = {};
  
  // Range usia
  if (filters.minAge || filters.maxAge) {
    query.age = {};
    if (filters.minAge) query.age.$gte = filters.minAge;
    if (filters.maxAge) query.age.$lte = filters.maxAge;
  }
  
  // Beberapa role
  if (filters.roles && filters.roles.length > 0) {
    query.role = { $in: filters.roles };
  }
  
  // Pencarian teks
  if (filters.search) {
    query.$or = [
      { name: { $regex: filters.search, $options: 'i' } },
      { email: { $regex: filters.search, $options: 'i' } }
    ];
  }
  
  // Range tanggal
  if (filters.startDate || filters.endDate) {
    query.createdAt = {};
    if (filters.startDate) query.createdAt.$gte = new Date(filters.startDate);
    if (filters.endDate) query.createdAt.$lte = new Date(filters.endDate);
  }
  
  // Status aktif
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

**2. Query Nested Object:**

```javascript
// Cari users di Jakarta
await User.find({ 'address.city': 'Jakarta' });

// Cari users dengan alamat lengkap
await User.find({
  'address.street': { $exists: true },
  'address.city': { $exists: true },
  'address.zipcode': { $exists: true }
});
```

**3. Query Array:**

```javascript
// Cari users dengan tag 'javascript'
await User.find({ tags: 'javascript' });

// Cari users dengan kedua tag
await User.find({ tags: { $all: ['javascript', 'nodejs'] } });

// Cari users dengan minimal 3 tag
await User.find({ tags: { $size: 3 } });

// Cari orders dengan item mahal
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



# V. TOPIK LANJUTAN

## 5.1 Aggregation Pipeline

Aggregation Pipeline adalah framework untuk memproses data dalam beberapa tahap (stages) secara berurutan.

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

**$group - Mengelompokkan dan menghitung:**

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

**$project - Memilih/mentransformasi field:**

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

**$unwind - Memecah array menjadi dokumen terpisah:**

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

// Aritmatika
{ $add: ["$price", "$tax"] }
{ $multiply: ["$quantity", "$price"] }
{ $round: ["$price", 2] }

// Tanggal
{ $year: "$createdAt" }
{ $month: "$createdAt" }
{ $dateToString: { format: "%Y-%m-%d", date: "$createdAt" } }

// Kondisional
{ $cond: { if: { $gte: ["$age", 18] }, then: "adult", else: "minor" } }
{ $ifNull: ["$phone", "N/A"] }
```

---

## 5.2 Strategi Indexing

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

### Index pada Mongoose

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

### Praktik Terbaik Indexing

Yang sebaiknya dilakukan:
- Index field yang sering di-query dan di-sort
- Compound index: equality, sort, range (berurutan)
- Monitor dengan $indexStats

Yang sebaiknya dihindari:
- Terlalu banyak index (memperlambat operasi write)
- Index pada field low cardinality (seperti boolean)

---

## 5.3 Relationships dan Population

### Embedding vs Referencing

**Embedding (data dalam satu dokumen):**

```javascript
// Cocok untuk: data selalu diakses bersama, relasi 1-to-few
const userSchema = new mongoose.Schema({
  name: String,
  address: { street: String, city: String, zipcode: String },
  phones: [String]
});
```

**Referencing (data terpisah dengan ID):**

```javascript
// Cocok untuk: data besar, many-to-many, sering berubah
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

## 5.4 Penanganan Error

### Jenis Error MongoDB/Mongoose

| Error | Penyebab |
|-------|----------|
| `ValidationError` | Data tidak sesuai schema |
| `CastError` | Tipe data salah (string ke ObjectId) |
| `MongoServerError 11000` | Duplicate key |
| `MongoNetworkError` | Koneksi gagal |

### Pola Penanganan Error

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



# VI. PRAKTIK TERBAIK

## 6.1 Optimasi Performa

### Optimasi Query

```javascript
// Tidak direkomendasikan: Mengambil semua field
const users = await User.find();

// Direkomendasikan: Hanya ambil field yang dibutuhkan
const users = await User.find().select('name email');

// Tidak direkomendasikan: Ambil semua data lalu filter di aplikasi
const allUsers = await User.find();
const adults = allUsers.filter(u => u.age >= 18);

// Direkomendasikan: Filter di database
const adults = await User.find({ age: { $gte: 18 } });

// Gunakan lean() untuk read-only (melewati overhead Mongoose)
const users = await User.find().lean();

// Pagination
const users = await User.find()
  .sort({ createdAt: -1 })
  .skip((page - 1) * limit)
  .limit(limit);
```

### Connection Pooling

```javascript
// config/database.js
mongoose.connect(process.env.MONGODB_URI, {
  maxPoolSize: 10,      // Maksimum koneksi
  minPoolSize: 5,       // Minimum koneksi
  maxIdleTimeMS: 10000, // Tutup koneksi idle
  serverSelectionTimeoutMS: 5000
});
```

### Bulk Operations

```javascript
// Tidak direkomendasikan: Loop operasi individual
for (const item of items) {
  await Product.updateOne({ _id: item.id }, { $set: { price: item.price } });
}

// Direkomendasikan: Bulk write
const bulkOps = items.map(item => ({
  updateOne: {
    filter: { _id: item.id },
    update: { $set: { price: item.price } }
  }
}));
await Product.bulkWrite(bulkOps);
```

### Strategi Caching

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
  setTimeout(() => cache.delete(cacheKey), 60000); // TTL 60 detik
  
  return user;
}
```

---

## 6.2 Panduan Keamanan

### Validasi dan Sanitasi Input

```javascript
// Tidak direkomendasikan: Langsung menggunakan input user
app.get('/users', async (req, res) => {
  const users = await User.find(req.query); // Rentan NoSQL Injection
});

// Direkomendasikan: Validasi dan sanitasi input
const sanitize = require('mongo-sanitize');

app.get('/users', async (req, res) => {
  const filter = {};
  if (req.query.name) filter.name = sanitize(req.query.name);
  if (req.query.role) filter.role = sanitize(req.query.role);
  const users = await User.find(filter);
  res.json(users);
});
```

### Pencegahan NoSQL Injection

```javascript
// Rentan injection: { "$gt": "" } dapat mem-bypass autentikasi
app.post('/login', async (req, res) => {
  const user = await User.findOne({
    email: req.body.email,
    password: req.body.password  // Dapat diinjeksi
  });
});

// Aman: Validasi tipe data
app.post('/login', async (req, res) => {
  if (typeof req.body.email !== 'string' || typeof req.body.password !== 'string') {
    return res.status(400).json({ message: 'Input tidak valid' });
  }
  const user = await User.findOne({ email: req.body.email });
  if (!user || !(await bcrypt.compare(req.body.password, user.password))) {
    return res.status(401).json({ message: 'Kredensial tidak valid' });
  }
  res.json({ token: generateToken(user) });
});
```

### Environment Variables

```bash
# .env - JANGAN commit ke git
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

### Keamanan Level Field

```javascript
// Jangan pernah mengembalikan password
const userSchema = new mongoose.Schema({
  email: String,
  password: { type: String, select: false } // Tidak dikembalikan secara default
});

// Hanya ambil password saat login
const user = await User.findOne({ email }).select('+password');
```

---

## 6.3 Organisasi Kode

### Struktur Project (Pola MVC)

```
project/
├── config/
│   └── database.js          # Koneksi database
├── models/
│   ├── User.js              # User schema dan model
│   ├── Post.js              # Post schema dan model
│   └── index.js             # Export semua models
├── controllers/
│   ├── userController.js    # Logic handler
│   └── postController.js
├── routes/
│   ├── userRoutes.js        # Definisi route
│   └── postRoutes.js
├── middleware/
│   ├── auth.js              # Authentication
│   ├── errorHandler.js      # Penanganan error
│   └── validate.js          # Validasi input
├── utils/
│   ├── asyncHandler.js
│   └── helpers.js
├── .env
├── .gitignore
├── package.json
└── index.js                 # Entry point
```

### Pola Controller

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

### Pola Route

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

## 6.4 Kesalahan Umum

### 1. Lupa await

```javascript
// Salah: Lupa await - mendapat Promise bukan data
const user = User.findById(id);
console.log(user.name); // undefined

// Benar
const user = await User.findById(id);
console.log(user.name);
```

### 2. N+1 Query Problem

```javascript
// Tidak efisien: Query di dalam loop
const posts = await Post.find();
for (const post of posts) {
  post.author = await User.findById(post.authorId); // N queries tambahan
}

// Efisien: Gunakan populate atau $lookup
const posts = await Post.find().populate('author', 'name email');
```

### 3. Tidak Menangani null

```javascript
// Salah: Crash jika user null
const user = await User.findById(id);
res.json(user.name); // TypeError jika null

// Benar
const user = await User.findById(id);
if (!user) {
  return res.status(404).json({ message: 'User tidak ditemukan' });
}
res.json(user.name);
```

### 4. Memory Leak - Cursor Tidak Ditutup

```javascript
// Tidak direkomendasikan untuk data besar
const allDocs = await Collection.find().toArray(); // Load semua ke memory

// Direkomendasikan: Gunakan cursor/stream
const cursor = Collection.find().cursor();
for await (const doc of cursor) {
  // Proses satu per satu
}
```

### 5. Tidak Memvalidasi ObjectId

```javascript
// Salah: Crash jika id bukan valid ObjectId
app.get('/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id); // CastError
});

// Benar: Validasi terlebih dahulu
const mongoose = require('mongoose');

app.get('/users/:id', async (req, res) => {
  if (!mongoose.Types.ObjectId.isValid(req.params.id)) {
    return res.status(400).json({ message: 'ID tidak valid' });
  }
  const user = await User.findById(req.params.id);
  if (!user) return res.status(404).json({ message: 'Tidak ditemukan' });
  res.json(user);
});
```

### 6. Schema Mismatch

```javascript
// Salah: Field tidak ada di schema (strict mode default)
const userSchema = new mongoose.Schema({ name: String, email: String });
await User.create({ name: "Alice", email: "a@b.com", phone: "123" });
// phone TIDAK tersimpan

// Benar: Pastikan semua field ada di schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  phone: String  // Tambahkan field
});
```

---

<div style="page-break-after: always;"></div>



# VII. STUDI KASUS DAN PROJECT

## 7.1 Struktur Project

### Studi Kasus: REST API Toko Online

Membangun REST API sederhana untuk manajemen produk dan pesanan menggunakan Express.js, MongoDB, dan Mongoose.

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

## 7.2 Implementasi Lengkap

### config/database.js

```javascript
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI);
    console.log('MongoDB Connected');
  } catch (error) {
    console.error('MongoDB Error:', error.message);
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

// Auto-generate nomor order
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

### routes/productRoutes.js dan orderRoutes.js

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

// Koneksi Database
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

## 7.3 Kode Sumber

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

### Pengujian API dengan cURL

```bash
# Membuat Produk
curl -X POST http://localhost:3000/api/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop ASUS","price":12000000,"stock":50,"category":"elektronik"}'

# Mendapatkan Semua Produk
curl http://localhost:3000/api/products?page=1&limit=5&category=elektronik

# Pencarian Produk
curl http://localhost:3000/api/products?search=laptop

# Membuat Order
curl -X POST http://localhost:3000/api/orders \
  -H "Content-Type: application/json" \
  -d '{
    "customer": {"name":"Budi","email":"budi@email.com","phone":"08123456"},
    "items": [{"product":"<product_id>","quantity":1}]
  }'

# Update Status Order
curl -X PATCH http://localhost:3000/api/orders/<order_id>/status \
  -H "Content-Type: application/json" \
  -d '{"status":"shipped"}'
```

---

<div style="page-break-after: always;"></div>



# VIII. SOAL DAN JAWABAN

## 8.1 Soal Konsep (Pilihan Ganda dan Essay)

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
- Pagination (page dan limit)
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
| 10 | **c** | `findByIdAndUpdate` dengan `{ new: true }` mengembalikan dokumen yang sudah di-update |

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

CAP Theorem menyatakan sistem terdistribusi hanya dapat memenuhi 2 dari 3 properti: Consistency, Availability, Partition Tolerance. MongoDB termasuk kategori CP - mengutamakan Consistency dan Partition Tolerance. Saat terjadi network partition, MongoDB mungkin tidak available (primary election) tetapi menjamin data konsisten.

**14. Indexing:**

Index mempercepat query dengan membuat struktur data terurut. Tanpa index, MongoDB harus melakukan scan seluruh collection (COLLSCAN). Jenis index:
- **Single Field**: Index pada satu field (`{ email: 1 }`)
- **Compound**: Index pada beberapa field (`{ city: 1, age: -1 }`)
- **Text**: Full-text search (`{ content: "text" }`)
- **TTL**: Auto-expire documents
- **Geospatial**: Query lokasi (`{ location: "2dsphere" }`)

**15. NoSQL Injection:**

NoSQL Injection terjadi saat attacker menyisipkan operator MongoDB melalui input. Contoh: mengirim `{"$gt": ""}` sebagai password untuk mem-bypass authentication. Pencegahan:
- Validasi tipe data input (pastikan string, bukan object)
- Gunakan library `mongo-sanitize`
- Jangan langsung meneruskan `req.body`/`req.query` ke query
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



# IX. TROUBLESHOOTING DAN FAQ

## 9.1 Error Umum

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

# Verifikasi
mongosh --eval "db.runCommand({ ping: 1 })"
```

---

### 2. MongoServerError: E11000 duplicate key

```
MongoServerError: E11000 duplicate key error collection: mydb.users index: email_1 dup key: { email: "test@email.com" }
```

**Penyebab:** Mencoba menyisipkan data dengan value yang sudah ada pada field unique.

**Solusi:**

```javascript
// Periksa terlebih dahulu sebelum insert
const exists = await User.findOne({ email: data.email });
if (exists) throw new Error('Email sudah terdaftar');

// Atau tangani error
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
// Pastikan koneksi selesai sebelum listen
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

**Penyebab:** String yang diberikan bukan format ObjectId valid (24 karakter hexadecimal).

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
1. Buka MongoDB Atlas - Network Access
2. Tambahkan IP address (atau 0.0.0.0/0 untuk development)
3. Pastikan username/password benar
4. Pastikan format connection string benar:
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
// Salah
const User = mongoose.model('User', userSchema); // Dipanggil berkali-kali

// Benar
const User = mongoose.models.User || mongoose.model('User', userSchema);
```

---

## 9.2 Solusi dan Tips

### Praktik Terbaik Koneksi

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
  console.error('Gagal terhubung setelah beberapa percobaan');
  process.exit(1);
};
```

### Mode Debug

```javascript
// Aktifkan debug untuk melihat semua query
mongoose.set('debug', true);

// Debug kustom
mongoose.set('debug', (collectionName, method, query, doc) => {
  console.log(`${collectionName}.${method}`, JSON.stringify(query));
});
```

### Manajemen Memory

```javascript
// Untuk data besar, gunakan cursor
const cursor = User.find().cursor();
for await (const user of cursor) {
  // Proses satu per satu, hemat memory
}

// Atau stream
User.find().stream()
  .on('data', (doc) => { /* proses */ })
  .on('error', (err) => { /* tangani */ })
  .on('end', () => { /* selesai */ });
```

### Deteksi Query Lambat

```javascript
// Monitor slow queries
mongoose.set('debug', (coll, method, query, doc, options) => {
  const start = Date.now();
  setTimeout(() => {
    const duration = Date.now() - start;
    if (duration > 100) {
      console.warn(`SLOW QUERY: ${coll}.${method} took ${duration}ms`);
    }
  }, 0);
});
```

---

## 9.3 Pertanyaan yang Sering Diajukan

### Q1: MongoDB gratis atau berbayar?

**A:** MongoDB Community Edition gratis dan open-source. MongoDB Atlas menyediakan free tier (512MB). Untuk fitur enterprise (advanced security, analytics), diperlukan lisensi berbayar.

---

### Q2: Kapan sebaiknya menggunakan MongoDB vs MySQL?

**A:**
- **MongoDB**: Data fleksibel, rapid development, horizontal scaling, real-time apps, content management
- **MySQL**: Data relasional kompleks, membutuhkan ACID strict, financial transactions, reporting kompleks

---

### Q3: Apakah MongoDB dapat digunakan untuk transaksi keuangan?

**A:** Sejak versi 4.0, MongoDB mendukung multi-document ACID transactions. Namun untuk sistem keuangan kritikal, SQL database masih lebih mature dan terbukti keandalannya.

---

### Q4: Berapa batas ukuran dokumen MongoDB?

**A:** Maksimal 16MB per dokumen. Untuk file besar, gunakan GridFS yang memecah file menjadi chunks 255KB.

---

### Q5: Apa perbedaan find() dan findOne()?

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

### Q8: Apakah Mongoose wajib digunakan?

**A:** Tidak. Mongoose adalah ODM opsional. Dapat menggunakan native MongoDB driver secara langsung. Mongoose memberikan kemudahan berupa schema validation, middleware, populate, dan lainnya. Untuk aplikasi sederhana atau yang membutuhkan performa maksimal, native driver dapat lebih cocok.

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
// Selalu tutup koneksi saat aplikasi shutdown
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
6. Update kode aplikasi (sintaks query)
7. Lakukan pengujian menyeluruh

---

<div style="page-break-after: always;"></div>



# X. REFERENSI DAN SUMBER DAYA

## 10.1 Dokumentasi Resmi

| Sumber | URL |
|--------|-----|
| MongoDB Documentation | https://www.mongodb.com/docs/ |
| MongoDB Manual | https://www.mongodb.com/docs/manual/ |
| Mongoose Documentation | https://mongoosejs.com/docs/ |
| MongoDB Node.js Driver | https://www.mongodb.com/docs/drivers/node/current/ |
| MongoDB Atlas | https://www.mongodb.com/cloud/atlas |
| MongoDB University (Kursus Gratis) | https://university.mongodb.com/ |

---

## 10.2 Rekomendasi Tools

### Manajemen Database

| Tool | Deskripsi | Platform |
|------|-----------|----------|
| **MongoDB Compass** | GUI resmi untuk MongoDB | Windows, macOS, Linux |
| **MongoDB Shell (mongosh)** | CLI interaktif | Semua platform |
| **Studio 3T** | GUI lanjutan (gratis dan berbayar) | Windows, macOS, Linux |
| **Robo 3T** | GUI ringan (gratis) | Windows, macOS, Linux |

### Tools Pengembangan

| Tool | Deskripsi |
|------|-----------|
| **Postman** | Pengujian dan dokumentasi API |
| **Thunder Client** | REST client extension untuk VS Code |
| **Nodemon** | Auto-restart server saat file berubah |
| **dotenv** | Manajemen environment variables |
| **Joi / express-validator** | Validasi input |
| **morgan** | HTTP request logger |

### Ekstensi VS Code

| Ekstensi | Fungsi |
|----------|--------|
| MongoDB for VS Code | Browse dan query MongoDB langsung dari VS Code |
| REST Client | Mengirim HTTP request dari file `.http` |
| ESLint | JavaScript linting |
| Prettier | Code formatting |

---

## 10.3 Sumber Pembelajaran

### Kursus Online (Gratis)

1. **MongoDB University** - https://university.mongodb.com/
   - M001: MongoDB Basics
   - M220JS: MongoDB for JavaScript Developers
   - M320: Data Modeling

2. **freeCodeCamp** - MongoDB dan Mongoose tutorial di YouTube

3. **The Net Ninja** - MongoDB playlist di YouTube

### Buku Rekomendasi

| Judul | Penulis |
|-------|---------|
| MongoDB: The Definitive Guide | Shannon Bradshaw, Eoin Brazil, Kristina Chodorow |
| Mongoose for Application Development | Simon Holmes |
| Node.js Design Patterns | Mario Casciaro, Luciano Mammino |

### Artikel dan Blog

- MongoDB Blog: https://www.mongodb.com/blog
- Dev.to MongoDB tag: https://dev.to/t/mongodb
- Medium MongoDB publications

---

## 10.4 Tautan Komunitas

| Platform | Tautan |
|----------|--------|
| MongoDB Community Forums | https://www.mongodb.com/community/forums/ |
| Stack Overflow (tag: mongodb) | https://stackoverflow.com/questions/tagged/mongodb |
| Reddit r/mongodb | https://www.reddit.com/r/mongodb/ |
| MongoDB GitHub | https://github.com/mongodb |
| Mongoose GitHub | https://github.com/Automattic/mongoose |
| Discord MongoDB Community | https://discord.gg/mongodb |

---

## Penutup

Laporan ini telah membahas secara komprehensif tentang MongoDB mulai dari konsep dasar NoSQL, instalasi, integrasi dengan Node.js menggunakan Mongoose, operasi CRUD, topik lanjutan (aggregation, indexing, relationships), praktik terbaik, hingga studi kasus pembuatan REST API. Dengan pemahaman materi ini, diharapkan pembaca dapat mengimplementasikan MongoDB dalam pengembangan aplikasi web modern secara efektif dan efisien.

---

*Laporan ini disusun sebagai bahan pembelajaran mata kuliah Pemrograman Web / Database Management.*  
*Tahun Akademik 2026*
