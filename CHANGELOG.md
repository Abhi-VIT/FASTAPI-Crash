# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-12

### Added

- Initial project setup with FastAPI framework
- Tea model with Pydantic validation
- Complete CRUD endpoints:
  - `GET /` - Welcome endpoint
  - `GET /teas` - Retrieve all teas
  - `POST /teas` - Create a new tea
  - `PUT /teas/{tea_id}` - Update an existing tea
  - `DELETE /teas/{tea_id}` - Delete a tea
- In-memory data storage (list-based)
- Automatic interactive API documentation (Swagger UI)
- Basic project documentation
- Requirements.txt with all dependencies

### Features

- Data validation using Pydantic models
- Type hints for better code clarity
- RESTful API design principles
- Interactive API exploration via Swagger UI

### Known Limitations

- Data is not persisted (lost on server restart)
- No authentication/authorization
- No database integration
- Error responses return 200 status code instead of appropriate HTTP codes
- No input validation beyond Pydantic types
- No logging or monitoring
- No rate limiting
- No CORS configuration

## Future Roadmap

### Planned for v1.1.0

- [ ] Database integration (SQLAlchemy + SQLite/PostgreSQL)
- [ ] Proper HTTP status codes (404 for not found, 400 for bad requests)
- [ ] Request logging
- [ ] Input validation improvements
- [ ] Unit tests with pytest

### Planned for v1.2.0

- [ ] Authentication (JWT tokens)
- [ ] Authorization (role-based access control)
- [ ] Rate limiting
- [ ] CORS support
- [ ] Pagination for list endpoints

### Planned for v2.0.0

- [ ] Docker containerization
- [ ] Docker Compose configuration
- [ ] CI/CD pipeline configuration
- [ ] API versioning
- [ ] Advanced search and filtering

## Notes

This is a learning project designed to demonstrate FastAPI fundamentals. See CONTRIBUTING.md for ways to help improve the project.
