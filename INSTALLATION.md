# Installation Guide

## Prerequisites

- Python 3.7 or higher
- pip (Python package manager)
- Git (optional, for cloning the repository)

## Step-by-Step Installation

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd FASTAPI-Crash
```

### Step 2: Create a Virtual Environment

Creating a virtual environment is strongly recommended to avoid dependency conflicts.

**On Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**On macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

This will install all required packages:
- **FastAPI**: Web framework for building APIs
- **Uvicorn**: ASGI server
- **Pydantic**: Data validation

### Step 4: Verify Installation

To verify that everything is installed correctly, run:

```bash
python -c "import fastapi; import uvicorn; import pydantic; print('All dependencies installed successfully!')"
```

## Running the Application

Start the development server:

```bash
uvicorn main:app --reload
```

You should see output similar to:
```
INFO:     Uvicorn running on http://127.0.0.1:8000
INFO:     Application startup complete
```

## Accessing the Application

- **API**: http://127.0.0.1:8000
- **Swagger UI Documentation**: http://127.0.0.1:8000/docs
- **ReDoc Documentation**: http://127.0.0.1:8000/redoc

## Troubleshooting

### Python not found
Ensure Python is installed and added to your system PATH. Check with:
```bash
python --version
```

### ModuleNotFoundError
Make sure your virtual environment is activated and all dependencies are installed:
```bash
pip install -r requirements.txt
```

### Port 8000 already in use
Use a different port:
```bash
uvicorn main:app --reload --port 8001
```

## Environment Setup for Development

To make development easier, you can create a `.env` file (optional):

```
PYTHONUNBUFFERED=1
```

This ensures that Python output is sent straight to logs without being buffered.

## Deactivating the Virtual Environment

When you're done working, deactivate the virtual environment:

```bash
deactivate
```

## Updating Dependencies

To update all packages to their latest versions:

```bash
pip install --upgrade -r requirements.txt
```

To see which packages have updates available:

```bash
pip list --outdated
```
