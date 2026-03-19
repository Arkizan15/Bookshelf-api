# 📚 Bookshelf API

A simple REST API for managing a book collection. Built with **Node.js** and **Hapi.js**, data is stored in memory (array).

---

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: [@hapi/hapi](https://hapi.dev/) v21
- **ID Generator**: [nanoid](https://github.com/ai/nanoid) v3
- **Linter**: ESLint + airbnb-base

---

## 📁 Project Structure

```
bookshelf-api/
├── src/
│   ├── server.js      # Entry point, Hapi server configuration
│   ├── routes.js      # All route definitions
│   ├── handler.js     # Handler logic for each endpoint
│   └── books.js       # In-memory data storage (array)
├── .eslintrc.json
├── .gitignore
├── package.json
└── README.md
```

---

## 🚀 Getting Started

### 1. Clone & Install

```bash
git clone https://github.com/Arkizan15/Bookshelf-api.git
cd bookshelf-api
npm install
```

### 2. Run the Server

```bash
npm run start
```

Server runs at `http://localhost:9000`.

### 3. Development Mode (with nodemon)

```bash
npm run start-dev
```

### 4. Run Linter

```bash
npm run lint
```

---

## 📡 API Endpoints

### ➕ Add a Book

```
POST /books
```

**Request Body:**

```json
{
  "name": "Book A",
  "year": 2010,
  "author": "John Doe",
  "summary": "Lorem ipsum dolor sit amet",
  "publisher": "Dicoding Indonesia",
  "pageCount": 100,
  "readPage": 25,
  "reading": false
}
```

**Success Response (201):**

```json
{
  "status": "success",
  "message": "Buku berhasil ditambahkan",
  "data": {
    "bookId": "Qbax5Oy7L8WKf74l"
  }
}
```

---

### 📋 Get All Books

```
GET /books
```

**Optional Query Parameters:**

| Parameter  | Type    | Description |
|------------|---------|-------------|
| `name`     | string  | Filter books by name (case-insensitive) |
| `reading`  | `0`/`1` | `0` = not currently reading, `1` = currently reading |
| `finished` | `0`/`1` | `0` = not finished, `1` = finished |

**Example:**
```
GET /books?name=dicoding&reading=1
```

**Response (200):**

```json
{
  "status": "success",
  "data": {
    "books": [
      {
        "id": "Qbax5Oy7L8WKf74l",
        "name": "Book A",
        "publisher": "Dicoding Indonesia"
      }
    ]
  }
}
```

---

### 🔍 Get Book Detail

```
GET /books/{bookId}
```

**Success Response (200):**

```json
{
  "status": "success",
  "data": {
    "book": {
      "id": "Qbax5Oy7L8WKf74l",
      "name": "Book A",
      "year": 2010,
      "author": "John Doe",
      "summary": "Lorem ipsum dolor sit amet",
      "publisher": "Dicoding Indonesia",
      "pageCount": 100,
      "readPage": 25,
      "finished": false,
      "reading": false,
      "insertedAt": "2021-03-04T09:11:44.598Z",
      "updatedAt": "2021-03-04T09:11:44.598Z"
    }
  }
}
```

---

### ✏️ Update a Book

```
PUT /books/{bookId}
```

Request body is the same as POST. Success response (200):

```json
{
  "status": "success",
  "message": "Buku berhasil diperbarui"
}
```

---

### 🗑️ Delete a Book

```
DELETE /books/{bookId}
```

**Success Response (200):**

```json
{
  "status": "success",
  "message": "Buku berhasil dihapus"
}
```

---

## ⚠️ Validation Rules

| Condition | Status | Message |
|-----------|--------|---------|
| `name` is missing (POST) | 400 | `Gagal menambahkan buku. Mohon isi nama buku` |
| `readPage > pageCount` (POST) | 400 | `Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount` |
| `name` is missing (PUT) | 400 | `Gagal memperbarui buku. Mohon isi nama buku` |
| `readPage > pageCount` (PUT) | 400 | `Gagal memperbarui buku. readPage tidak boleh lebih besar dari pageCount` |
| `bookId` not found (GET) | 404 | `Buku tidak ditemukan` |
| `bookId` not found (PUT) | 404 | `Gagal memperbarui buku. Id tidak ditemukan` |
| `bookId` not found (DELETE) | 404 | `Buku gagal dihapus. Id tidak ditemukan` |

---

## 🧪 Testing with Postman

1. Import `Bookshelf_API_Test_postman_collection.json`
2. Import `Bookshelf_API_Test_postman_environment.json`
3. Select the **Bookshelf API Test** environment
4. Start the server with `npm run start`
5. Run All Tests in Postman
