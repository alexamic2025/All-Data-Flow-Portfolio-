# API Documentation

## Data Pipeline API

### Authentication
All API endpoints require authentication via API key:
```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
     https://api.example.com/v1/pipelines
```

### Endpoints

#### Pipeline Management

**GET /v1/pipelines**
List all data pipelines
```json
{
  "pipelines": [
    {
      "id": "pipeline-001",
      "name": "Customer Events Pipeline",
      "status": "running",
      "last_run": "2024-12-13T10:30:00Z"
    }
  ]
}
```

**POST /v1/pipelines/{id}/trigger**
Manually trigger pipeline execution
```bash
curl -X POST \
  -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.example.com/v1/pipelines/pipeline-001/trigger
```

**GET /v1/pipelines/{id}/status**
Get pipeline execution status
```json
{
  "pipeline_id": "pipeline-001",
  "status": "running",
  "progress": 75,
  "estimated_completion": "2024-12-13T11:00:00Z"
}
```

#### Data Quality API

**GET /v1/data-quality/reports**
Get data quality reports
```json
{
  "reports": [
    {
      "dataset": "customer_events",
      "quality_score": 0.95,
      "issues": ["null_values_in_email"],
      "timestamp": "2024-12-13T10:00:00Z"
    }
  ]
}
```

#### Analytics API

**GET /v1/analytics/metrics**
Get system metrics
```json
{
  "metrics": {
    "throughput": "1000 events/sec",
    "latency_p99": "250ms",
    "error_rate": "0.01%",
    "uptime": "99.95%"
  }
}
```

### Error Handling
```json
{
  "error": {
    "code": "PIPELINE_NOT_FOUND",
    "message": "Pipeline with ID 'invalid-id' not found",
    "timestamp": "2024-12-13T10:30:00Z"
  }
}
```

### Rate Limiting
- 1000 requests per hour per API key
- Burst limit: 100 requests per minute