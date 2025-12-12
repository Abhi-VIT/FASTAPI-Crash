# Contributing Guide

Thank you for your interest in contributing to the FastAPI Tea Management Project!

## Getting Started

1. Fork the repository
2. Clone your fork locally
3. Create a new branch for your feature or bugfix
4. Make your changes
5. Test your changes
6. Submit a pull request

## Development Setup

```bash
# Clone repository
git clone https://github.com/yourusername/FASTAPI-Crash.git
cd FASTAPI-Crash

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the application
uvicorn main:app --reload
```

## Code Style

- Follow PEP 8 guidelines
- Use meaningful variable and function names
- Keep functions small and focused
- Add docstrings to functions and classes

## Making Changes

### Creating a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### Committing Changes

```bash
git add .
git commit -m "Add description of your changes"
```

Use clear, descriptive commit messages.

## Testing

Before submitting a pull request, test your changes:

1. Verify the API runs without errors
2. Test all endpoints affected by your changes
3. Check for any validation issues

## Documentation

- Update README.md if you add new features
- Add comments to complex code sections
- Update API_REFERENCE.md for new endpoints

## Pull Request Process

1. Update the README.md with details of changes if applicable
2. Ensure your code follows the project's style guidelines
3. Provide a clear description of the changes
4. Reference any related issues

## Reporting Bugs

When reporting bugs, please include:

- Python version
- Operating system
- Steps to reproduce
- Expected behavior
- Actual behavior

## Areas for Improvement

Current limitations that could be enhanced:

- Add database persistence (currently uses in-memory list)
- Implement authentication and authorization
- Add input validation enhancements
- Implement pagination for large datasets
- Add filtering and search capabilities
- Implement proper HTTP status codes (currently returns 200 for errors)
- Add unit tests
- Add request logging and monitoring
- Implement rate limiting
- Add CORS support
- Create Docker configuration

## Questions?

Feel free to open an issue for any questions or discussions.

Thank you for contributing!
