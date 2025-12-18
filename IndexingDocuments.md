## Indexing Documents in Elasticsearch

![Image](https://duydo.me/images/posts/es_index_operations.png?utm_source=chatgpt.com)

![Image](https://smnh.me/resized-images/elasticsearch/elasticsearch-arbitrary-data-sharp-768x702.webp?utm_source=chatgpt.com)

![Image](https://miro.medium.com/1%2A3z9uZh68kT2kvTCaDFDB3g.png?utm_source=chatgpt.com)

Indexing a document means **adding or updating a JSON document** so it becomes **searchable**.

---

## 1️⃣ Index a Document with Auto-Generated ID

Elasticsearch creates the `_id` automatically.

```http
POST my_index/_doc
{
  "name": "Suresh",
  "role": "DevOps Engineer",
  "experience": 19,
  "skills": ["Kubernetes", "AWS", "Elasticsearch"]
}
```

✔ Use `POST` when you don’t care about the document ID.

---

## 2️⃣ Index a Document with Custom ID

You control the document `_id`.

```http
PUT my_index/_doc/1
{
  "name": "Ravi",
  "role": "SRE",
  "experience": 12
}
```

📌 Re-using the same ID **updates** the document (overwrite).

---

## 3️⃣ Create or Update (Upsert)

Updates if exists, creates if not.

```http
POST my_index/_update/1
{
  "doc": {
    "experience": 13
  },
  "doc_as_upsert": true
}
```

---

## 4️⃣ Bulk Indexing (Best for Performance)

Used for **large data ingestion**.

```http
POST _bulk
{ "index": { "_index": "my_index", "_id": "2" } }
{ "name": "Anita", "role": "Cloud Architect" }
{ "index": { "_index": "my_index", "_id": "3" } }
{ "name": "Kiran", "role": "Platform Engineer" }
```

⚠️ Rules:

* Each line must end with a newline
* No commas between JSON objects

---

## 5️⃣ Indexing via cURL

```bash
curl -X POST "http://localhost:9200/my_index/_doc" \
-H 'Content-Type: application/json' \
-d '{
  "name": "Rahul",
  "location": "Hyderabad"
}'
```

---

## 6️⃣ Verify Indexed Documents

### Get document by ID

```http
GET my_index/_doc/1
```

### Search all documents

```http
GET my_index/_search
{
  "query": {
    "match_all": {}
  }
}
```

---

## 7️⃣ Refresh Behavior (Important)

Documents are **not immediately searchable**.

### Force refresh (not recommended frequently)

```http
POST my_index/_refresh
```

⏱ Default refresh interval: **1 second**

---

## 8️⃣ Common Indexing Errors & Fixes

| Error                        | Cause               | Fix                         |
| ---------------------------- | ------------------- | --------------------------- |
| `mapper_parsing_exception`   | Field type mismatch | Fix mapping                 |
| `index_not_found_exception`  | Index missing       | Create index                |
| `document_missing_exception` | Update without ID   | Use upsert                  |
| Slow indexing                | Too many refreshes  | Disable refresh temporarily |

---

## 9️⃣ Production Best Practices

✔ Use **bulk API**
✔ Define **explicit mappings**
✔ Disable refresh during heavy ingestion
✔ Use **ILM** for time-based data
✔ Monitor shard size (20–50GB ideal)

---

## 🎯 Interview-Ready Answer

> *“Indexing in Elasticsearch involves adding JSON documents using REST APIs. For high throughput, we use the Bulk API, control mappings, and manage refresh intervals. Updates are handled via document IDs or upserts.”*

---

If you want next, I can explain:

* Indexing **logs / metrics**
* Indexing via **Logstash / Beats**
* Mapping design for **search vs analytics**
* **Reindex API**
* Real **production indexing issues**

Just tell me 👍
