# Healthcare Platform - Technical Documentation

## Overview
Healthcare platform for managing patient data, medical documents, and AI-assisted analysis. This documentation covers technical setup, architecture, and implementation details.

## System Requirements

### Development Environment
```yaml
Required Software:
  - Python 3.9+
  - Docker & Docker Compose
  - Git
  - Make (optional)

Hardware Recommendations:
  - CPU: 4+ cores
  - RAM: 16GB+
  - Storage: 50GB+
  - GPU: Optional, improves AI service performance
```

## Installation

### Local Development Setup
```bash
# Clone repository
git clone [repository-url]

# Setup virtual environment
python -m venv venv
source venv/bin/activate  # Unix
.\venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt

# Setup environment variables
cp .env.example .env

# Start services
docker-compose up -d

# Run migrations
python manage.py migrate
```

## Core Components

### Backend (Django)
```yaml
Purpose: Main application server
Features:
  - Patient data management
  - Authentication/Authorization
  - Document management
  - API endpoints
Configuration:
  - settings/
    - base.py      # Base settings
    - local.py     # Development settings
    - prod.py      # Production settings
```

### Services (FastAPI)
```yaml
Components:
  rag/
    - Document processing
    - Context retrieval
  audio/
    - Audio transcription
    - Medical terminology extraction
  search/
    - Full-text search
    - Medical term indexing
  embeddings/
    - Vector generation
    - Similarity search
  agents/
    - Medical analysis
    - Report generation
```

### Database Setup

#### PostgreSQL
```sql
-- Initialize database
CREATE DATABASE health_db;
CREATE USER health_user WITH PASSWORD 'password';
GRANT ALL PRIVILEGES ON DATABASE health_db TO health_user;
```

#### MongoDB
```javascript
// Create collections
db.createCollection("documents")
db.createCollection("audio_files")
```

#### Qdrant
```yaml
Collections:
  - medical_vectors
  - document_embeddings
```

## Configuration

### Environment Variables
```bash
# Database
DB_NAME=health_db
DB_USER=health_user
DB_PASSWORD=password
DB_HOST=localhost

# Services
RAG_SERVICE_URL=http://localhost:8001
AUDIO_SERVICE_URL=http://localhost:8002
SEARCH_SERVICE_URL=http://localhost:8003

# Queue
RABBITMQ_HOST=localhost
RABBITMQ_USER=guest
RABBITMQ_PASS=guest
```

## Development Workflows

### Adding New Features
1. Create feature branch
2. Implement changes
3. Write tests
4. Submit pull request

### Running Tests
```bash
# Backend tests
python manage.py test

# Service tests
cd services/rag && pytest
cd services/audio && pytest
```

### Common Tasks
```bash
# Create database migrations
python manage.py makemigrations

# Start development server
python manage.py runserver

# Start service
cd services/rag && uvicorn main:app --reload
```

## Troubleshooting

### Common Issues
```yaml
Database Connection:
  - Check credentials in .env
  - Ensure services are running
  - Verify network connectivity

Service Startup:
  - Check port availability
  - Verify dependencies
  - Check log files

Processing Errors:
  - Check queue status
  - Verify file permissions
  - Check service logs
```

Would you like me to elaborate on any section or add additional details?