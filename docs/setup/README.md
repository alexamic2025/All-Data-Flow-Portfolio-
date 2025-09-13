# Setup Instructions

## Prerequisites
- Python 3.8+
- Docker & Docker Compose
- Git
- AWS CLI (for cloud projects)

## Local Development Environment

### 1. Python Environment
```bash
# Create virtual environment
python -m venv venv

# Activate (Linux/Mac)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Docker Setup
```bash
# Install Docker (Ubuntu)
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Start services
docker-compose up -d
```

### 3. Database Setup
```bash
# PostgreSQL
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=password \
  -p 5432:5432 \
  postgres:14

# MongoDB
docker run -d \
  --name mongodb \
  -p 27017:27017 \
  mongo:latest
```

## Cloud Environment Setup

### AWS Configuration
```bash
# Install AWS CLI
pip install awscli

# Configure credentials
aws configure

# Set default region
aws configure set default.region us-east-1
```

### Infrastructure Deployment
```bash
# Terraform
cd terraform/
terraform init
terraform plan
terraform apply

# CloudFormation
aws cloudformation deploy \
  --template-file template.yaml \
  --stack-name data-pipeline \
  --capabilities CAPABILITY_IAM
```

## Environment Variables
```bash
# .env file template
DATABASE_URL=postgresql://user:pass@localhost:5432/db
REDIS_URL=redis://localhost:6379
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
KAFKA_BROKERS=localhost:9092
```

## Verification
```bash
# Test database connection
python scripts/test_db_connection.py

# Verify services
docker ps
curl http://localhost:8000/health

# Run smoke tests
pytest tests/smoke/
```