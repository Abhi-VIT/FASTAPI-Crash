# FastAPI Tea Management API

A simple FastAPI project demonstrating basic CRUD operations for managing a tea collection. This is a learning project for understanding FastAPI fundamentals.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Data Models](#data-models)
- [Project Structure](#project-structure)
- [Examples](#examples)

## Features

- 🍵 Create, Read, Update, and Delete (CRUD) operations for tea items
- 📚 RESTful API design using FastAPI
- ✅ Data validation using Pydantic models
- 🎯 Interactive API documentation (Swagger UI)
- 📖 OpenAPI specification support

## Prerequisites

- Python 3.7 or higher
- pip (Python package manager)

## Installation

1. **Clone the repository** (if using git):
```bash
git clone <repository-url>
cd FASTAPI-Crash
```

2. **Create a virtual environment** (recommended):
```bash
python -m venv venv
# On Windows
venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate
```

3. **Install dependencies**:
```bash
pip install -r requirements.txt
```

## Running the Application

Start the FastAPI development server with hot-reload enabled:

```bash
uvicorn main:app --reload
```

The server will start on `http://127.0.0.1:8000`

### Access the API Documentation

- **Swagger UI**: http://127.0.0.1:8000/docs
- **ReDoc**: http://127.0.0.1:8000/redoc

## API Endpoints

### 1. Welcome Endpoint

**GET** `/`

Returns a welcome message.

**Response**:
```json
{
  "message": "Welcome to chai code"
}
```

---

### 2. Get All Teas

**GET** `/teas`

Retrieves a list of all teas in the collection.

**Response**:
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

---

### 3. Create a New Tea

**POST** `/teas`

Adds a new tea to the collection.

**Request Body**:
```json
{
  "id": 1,
  "name": "Oolong Tea",
  "origin": "Taiwan"
}
```

**Response**: Returns the created tea object with status code 200.

---

### 4. Update a Tea

**PUT** `/teas/{tea_id}`

Updates an existing tea by its ID.

**Path Parameter**:
- `tea_id` (int): The ID of the tea to update

**Request Body**:
```json
{
  "id": 1,
  "name": "Premium Oolong",
  "origin": "Taiwan"
}
```

**Response**: Returns the updated tea object or an error if not found.

---

### 5. Delete a Tea

**DELETE** `/teas/{tea_id}`

Deletes a tea from the collection by its ID.

**Path Parameter**:
- `tea_id` (int): The ID of the tea to delete

**Response**: Returns the deleted tea object or an error if not found.

## Data Models

### Tea Model

```python
class Tea(BaseModel):
    id: int           # Unique identifier for the tea
    name: str         # Name of the tea
    origin: str       # Origin/region of the tea
```

**Validation**: All fields are required and use Pydantic's built-in validation.

## Project Structure

```
FASTAPI-Crash/
├── main.py              # Main application file with all endpoints
├── requirements.txt     # Project dependencies
├── README.md           # Project documentation
└── __pycache__/        # Python cache directory
```

## Examples

### Using cURL

**Get all teas**:
```bash
curl http://127.0.0.1:8000/teas
```

**Add a new tea**:
```bash
curl -X POST http://127.0.0.1:8000/teas \
  -H "Content-Type: application/json" \
  -d '{"id": 1, "name": "Jasmine Tea", "origin": "China"}'
```

**Update a tea**:
```bash
curl -X PUT http://127.0.0.1:8000/teas/1 \
  -H "Content-Type: application/json" \
  -d '{"id": 1, "name": "Premium Jasmine", "origin": "China"}'
```

**Delete a tea**:
```bash
curl -X DELETE http://127.0.0.1:8000/teas/1
```

### Using Python Requests

```python
import requests

# Base URL
BASE_URL = "http://127.0.0.1:8000"

# Get all teas
response = requests.get(f"{BASE_URL}/teas")
print(response.json())

# Add a new tea
new_tea = {"id": 1, "name": "Puer Tea", "origin": "China"}
response = requests.post(f"{BASE_URL}/teas", json=new_tea)
print(response.json())

# Update a tea
updated_tea = {"id": 1, "name": "Aged Puer", "origin": "China"}
response = requests.put(f"{BASE_URL}/teas/1", json=updated_tea)
print(response.json())

# Delete a tea
response = requests.delete(f"{BASE_URL}/teas/1")
print(response.json())
```

## Dependencies

- **FastAPI** (0.124.2): Web framework for building APIs with Python
- **Uvicorn** (0.38.0): ASGI server for running FastAPI applications
- **Pydantic** (2.12.5): Data validation library for Python

See `requirements.txt` for the complete list of dependencies.

## Notes

- This project uses an in-memory list to store tea data. Data will be reset when the server restarts.
- For production use, consider integrating a database (e.g., PostgreSQL, MongoDB).
- Add authentication and authorization for production environments.

## Learning Objectives

This project demonstrates:
- Creating FastAPI applications
- Defining and using Pydantic models for data validation
- Implementing CRUD operations
- Using decorators for route definition
- Path and request body parameters
- API documentation generation