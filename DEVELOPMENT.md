# Development Guide

Guide for developers working on this FastAPI Tea Management project.

## Project Structure

```
FASTAPI-Crash/
├── main.py                 # Main application file
├── requirements.txt        # Project dependencies
├── README.md              # Project overview and quick start
├── INSTALLATION.md        # Installation instructions
├── API_REFERENCE.md       # Complete API documentation
├── CONTRIBUTING.md        # Contribution guidelines
├── DEVELOPMENT.md         # This file - development guide
├── CHANGELOG.md           # Version history and roadmap
└── __pycache__/          # Python cache directory
```

## Technology Stack

- **FastAPI** (0.124.2): Modern web framework for building APIs
- **Uvicorn** (0.38.0): ASGI server
- **Pydantic** (2.12.5): Data validation library
- **Python** (3.7+): Programming language

## Running the Application

### Development Mode

```bash
uvicorn main:app --reload
```

The `--reload` flag enables hot-reloading (automatically restarts when code changes).

### Production Mode

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

## Code Structure Overview

### main.py

The application is structured in a single file:

```python
# 1. Imports
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List

# 2. App initialization
app = FastAPI()

# 3. Data models
class Tea(BaseModel):
    id: int
    name: str
    origin: str

# 4. In-memory storage
teas: List[Tea] = []

# 5. Route handlers
@app.get("/")
def read_root(): ...

@app.get("/teas")
def get_teas(): ...

@app.post("/teas")
def add_tea(tea: Tea): ...

@app.put("/teas/{tea_id}")
def update_tea(tea_id: int, updated_tea: Tea): ...

@app.delete("/teas/{tea_id}")
def delete_tea(tea_id: int): ...
```

## API Documentation

### Interactive Documentation

**Swagger UI**: http://127.0.0.1:8000/docs
**ReDoc**: http://127.0.0.1:8000/redoc

These are automatically generated from your code.

## Development Workflow

### 1. Making Code Changes

Edit `main.py` and save. With `--reload` enabled, the server automatically restarts.

### 2. Testing Changes

Use the Swagger UI (http://127.0.0.1:8000/docs) to test endpoints manually.

Or use cURL:
```bash
curl -X GET http://127.0.0.1:8000/teas
```

Or use Python requests:
```python
import requests
response = requests.get("http://127.0.0.1:8000/teas")
print(response.json())
```

### 3. Version Control

```bash
# Check status
git status

# Stage changes
git add main.py

# Commit changes
git commit -m "Describe your changes"

# Push to remote
git push origin feature-branch
```

## Common Development Tasks

### Adding a New Endpoint

1. Define the route with appropriate decorator
2. Add request/response models if needed
3. Implement the handler function
4. Test in Swagger UI

Example:
```python
@app.get("/teas/{tea_id}")
def get_tea_by_id(tea_id: int):
    for tea in teas:
        if tea.id == tea_id:
            return tea
    return {"error": "Tea not found"}
```

### Modifying Data Models

Update the `Tea` class to add/remove fields:

```python
class Tea(BaseModel):
    id: int
    name: str
    origin: str
    year: int  # New field
    type: str  # New field
```

### Improving Error Handling

Current approach returns 200 with error object. Better approach:

```python
from fastapi import HTTPException, status

@app.put("/teas/{tea_id}")
def update_tea(tea_id: int, updated_tea: Tea):
    for index, tea in enumerate(teas):
        if tea.id == tea_id:
            teas[index] = updated_tea
            return updated_tea
    raise HTTPException(
        status_code=status.HTTP_404_NOT_FOUND,
        detail="Tea not found"
    )
```

## Debugging

### Using print() for debugging

```python
@app.get("/teas")
def get_teas():
    print(f"Current teas: {teas}")  # Debug output
    return teas
```

Output appears in the terminal where `uvicorn` is running.

### Using a Debugger

To use Python's built-in debugger:

```python
import pdb

@app.get("/teas")
def get_teas():
    pdb.set_trace()  # Debugger stops here
    return teas
```

Or use an IDE's debugger with breakpoints.

## Performance Considerations

- Current in-memory list is fine for small datasets
- For large datasets, use a database
- Consider caching for read-heavy operations
- Profile code for bottlenecks using `cProfile`

## Security Considerations

Current implementation lacks:
- Authentication
- Authorization
- Input sanitization
- Rate limiting
- HTTPS (in development, HTTP is fine)

For production, add security features.

## Logging

Add logging for better debugging:

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@app.get("/teas")
def get_teas():
    logger.info("Fetching all teas")
    return teas
```

## Next Steps for Improvement

1. **Database Integration**: Replace in-memory list with a database
2. **Better Error Handling**: Use appropriate HTTP status codes
3. **Testing**: Add unit tests with pytest
4. **Authentication**: Add JWT-based authentication
5. **Logging**: Implement proper logging
6. **Docker**: Create Docker configuration for containerization
7. **Documentation**: Add docstrings to all functions

## Useful Commands

```bash
# Start development server
uvicorn main:app --reload

# Start with custom port
uvicorn main:app --reload --port 8001

# Check code syntax
python -m py_compile main.py

# Install development dependencies
pip install pytest pytest-asyncio httpx

# Run tests (after adding tests)
pytest

# Format code (if using black)
black main.py

# Lint code (if using flake8)
flake8 main.py
```

## Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com)
- [Pydantic Documentation](https://docs.pydantic.dev)
- [Uvicorn Documentation](https://www.uvicorn.org)
- [HTTP Status Codes](https://httpwg.org/specs/rfc7231.html#status.codes)

## Questions or Issues?

Refer to the CONTRIBUTING.md file for how to report issues or ask questions.
