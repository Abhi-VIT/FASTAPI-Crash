# API Reference

Complete reference for all endpoints in the FastAPI Tea Management API.

## Base URL

```
http://127.0.0.1:8000
```

## Authentication

This API does not require authentication in its current implementation.

---

## Endpoints

### 1. Welcome Endpoint

**GET** `/`

Returns a welcome message.

**Response:** `200 OK`

```json
{
  "message": "Welcome to chai code"
}
```

**Example:**
```bash
curl http://127.0.0.1:8000/
```

---

### 2. Get All Teas

**GET** `/teas`

Retrieves a list of all teas currently stored in the system.

**Response:** `200 OK`

```json
[
  {
    "id": 1,
    "name": "Green Tea",
    "origin": "China"
  },
  {
    "id": 2,
    "name": "Black Tea",
    "origin": "India"
  }
]
```

**Example:**
```bash
curl http://127.0.0.1:8000/teas
```

---

### 3. Create a New Tea

**POST** `/teas`

Adds a new tea to the collection.

**Request Headers:**
```
Content-Type: application/json
```

**Request Body:**
```json
{
  "id": 1,
  "name": "Oolong Tea",
  "origin": "Taiwan"
}
```

**Response:** `200 OK`

```json
{
  "id": 1,
  "name": "Oolong Tea",
  "origin": "Taiwan"
}
```

**Validation Rules:**
- `id` (required, integer): Must be a positive integer
- `name` (required, string): Cannot be empty
- `origin` (required, string): Cannot be empty

**Example:**
```bash
curl -X POST http://127.0.0.1:8000/teas \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "Jasmine Tea",
    "origin": "China"
  }'
```

---

### 4. Update a Tea

**PUT** `/teas/{tea_id}`

Updates an existing tea by its ID. Replaces all fields with the new values.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `tea_id` | integer | The unique ID of the tea to update |

**Request Headers:**
```
Content-Type: application/json
```

**Request Body:**
```json
{
  "id": 1,
  "name": "Premium Oolong",
  "origin": "Taiwan"
}
```

**Response:** `200 OK`

```json
{
  "id": 1,
  "name": "Premium Oolong",
  "origin": "Taiwan"
}
```

**Response (Not Found):** `200` (Note: Returns error object instead of 404)

```json
{
  "error": "Tea not found"
}
```

**Example:**
```bash
curl -X PUT http://127.0.0.1:8000/teas/1 \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "Premium Oolong",
    "origin": "Taiwan"
  }'
```

---

### 5. Delete a Tea

**DELETE** `/teas/{tea_id}`

Removes a tea from the collection by its ID.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `tea_id` | integer | The unique ID of the tea to delete |

**Response:** `200 OK` (Success)

```json
{
  "id": 1,
  "name": "Oolong Tea",
  "origin": "Taiwan"
}
```

**Response (Not Found):** `200` (Returns error object)

```json
{
  "error": "Tea not found"
}
```

**Example:**
```bash
curl -X DELETE http://127.0.0.1:8000/teas/1
```

---

## Data Models

### Tea Object

Represents a single tea item in the collection.

```json
{
  "id": 1,
  "name": "Green Tea",
  "origin": "China"
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique identifier for the tea |
| `name` | string | Name of the tea |
| `origin` | string | Geographic origin/region of the tea |

---

## HTTP Status Codes

The API uses the following HTTP status codes:

| Code | Meaning |
|------|---------|
| 200 | OK - Request succeeded |
| 400 | Bad Request - Invalid input |
| 404 | Not Found - Resource not found |
| 422 | Unprocessable Entity - Validation error |

---

## Error Handling

Errors are returned as JSON objects:

**Example Error Response:**
```json
{
  "error": "Tea not found"
}
```

**Validation Error Response:**
```json
{
  "detail": [
    {
      "loc": ["body", "name"],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

---

## Rate Limiting

No rate limiting is currently implemented.

---

## CORS

CORS (Cross-Origin Resource Sharing) is not configured by default. To enable CORS, you would need to add middleware to the FastAPI application.

---

## Pagination

Pagination is not implemented. The `/teas` endpoint returns all teas in the collection.

---

## Filtering & Sorting

Filtering and sorting capabilities are not implemented in the current version.

---

## Query Parameters

Query parameters are not used in this API version.

---

## Request/Response Examples

### Complete CRUD Workflow

**1. Create a tea:**
```bash
curl -X POST http://127.0.0.1:8000/teas \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "Green Tea",
    "origin": "Japan"
  }'
```

**2. Get all teas:**
```bash
curl http://127.0.0.1:8000/teas
```

**3. Update the tea:**
```bash
curl -X PUT http://127.0.0.1:8000/teas/1 \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "Premium Green Tea",
    "origin": "Japan"
  }'
```

**4. Delete the tea:**
```bash
curl -X DELETE http://127.0.0.1:8000/teas/1
```

---

## Using Python Requests

```python
import requests

BASE_URL = "http://127.0.0.1:8000"

# Create
response = requests.post(
    f"{BASE_URL}/teas",
    json={"id": 1, "name": "Matcha", "origin": "Japan"}
)
print("Create:", response.json())

# Read
response = requests.get(f"{BASE_URL}/teas")
print("Read:", response.json())

# Update
response = requests.put(
    f"{BASE_URL}/teas/1",
    json={"id": 1, "name": "Premium Matcha", "origin": "Japan"}
)
print("Update:", response.json())

# Delete
response = requests.delete(f"{BASE_URL}/teas/1")
print("Delete:", response.json())
```
