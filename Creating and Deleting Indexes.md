Here’s a **clear, practical guide** to **create and delete an index in Elasticsearch**, using REST API and common tools.

---

## 🔹 What is an Index in Elasticsearch?

An **index** is like a **database/table** where documents (JSON records) are stored and searched.

---

## ✅ Create an Index

### 1️⃣ Create a simple index (default settings)

```http
PUT my_index
```

**Response**

```json
{
  "acknowledged": true,
  "shards_acknowledged": true,
  "index": "my_index"
}
```

---

### 2️⃣ Create an index with **settings & mappings**

```http
PUT my_index
{
  "settings": {
    "number_of_shards": 3,
    "number_of_replicas": 1
  },
  "mappings": {
    "properties": {
      "name": {
        "type": "text"
      },
      "age": {
        "type": "integer"
      },
      "created_at": {
        "type": "date"
      }
    }
  }
}
```

✔ Best practice: Always define mappings for production indexes.

---

### 3️⃣ Create index using **Kibana Dev Tools**

* Open **Kibana → Dev Tools → Console**
* Paste the same `PUT` command
* Click **Run ▶**

---

## ❌ Delete an Index

### 4️⃣ Delete a single index

```http
DELETE my_index
```

**Response**

```json
{
  "acknowledged": true
}
```

⚠️ **Warning**: This permanently deletes all data in the index.

---

### 5️⃣ Delete multiple indexes

```http
DELETE index1,index2,index3
```

---

### 6️⃣ Delete all indexes (VERY DANGEROUS)

```http
DELETE _all
```

or

```http
DELETE *
```

🚨 Never run this in production unless absolutely sure.

---

## 🔍 Verify Index Exists

### List all indexes

```http
GET _cat/indices?v
```

### Check a specific index

```http
GET my_index
```

---

## 🧠 Production Best Practices (Important)

* ❌ Don’t delete indexes directly in prod
* ✅ Use **aliases** for zero-downtime changes
* ✅ Use **Index Lifecycle Management (ILM)**
* ✅ Take **snapshots** before deletion

---

## 🔑 Interview Tip (Elastic / DevOps)

> *“Indexes should be immutable in production; use versioned indexes with aliases instead of deleting directly.”*

---
