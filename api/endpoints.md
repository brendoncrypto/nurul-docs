# API Endpoints

This document outlines all available endpoints in the Nurul API.

## Base URL

All API requests should be made to:
```
https://api.nurul.ai/v1
```

## Prompts

### Generate a Prompt
`POST /prompts`

Generate a new therapeutic prompt based on provided parameters.

#### Request Body
```json
{
  "primaryConcern": "anxiety",
  "therapeuticApproach": "cbt",
  "sessionContext": "follow_up",
  "clientBackground": "Experiencing workplace stress",
  "goals": ["identify_triggers", "develop_coping_strategies"],
  "preferences": {
    "tone": "supportive",
    "length": "medium",
    "focus": "practical"
  }
}
```

#### Response
```json
{
  "id": "prompt_123abc",
  "prompt": "How have recent workplace situations affected your anxiety levels? Let's explore specific triggers and identify which coping strategies have been most effective for you.",
  "metadata": {
    "approach": "cbt",
    "context": "follow_up",
    "created_at": "2024-03-20T10:30:00Z"
  }
}
```

### List Saved Prompts
`GET /prompts`

Retrieve a list of your saved prompts.

#### Query Parameters
- `limit` (optional): Number of prompts to return (default: 10, max: 100)
- `offset` (optional): Pagination offset
- `filter` (optional): Filter by approach, concern, or date

#### Response
```json
{
  "prompts": [
    {
      "id": "prompt_123abc",
      "prompt": "...",
      "metadata": {
        "approach": "cbt",
        "created_at": "2024-03-20T10:30:00Z"
      }
    }
  ],
  "total": 45,
  "has_more": true
}
```

### Get a Specific Prompt
`GET /prompts/{prompt_id}`

Retrieve a specific prompt by ID.

#### Response
```json
{
  "id": "prompt_123abc",
  "prompt": "...",
  "metadata": {
    "approach": "cbt",
    "created_at": "2024-03-20T10:30:00Z"
  }
}
```

## Templates

### List Templates
`GET /templates`

Retrieve available prompt templates.

#### Query Parameters
- `approach` (optional): Filter by therapeutic approach
- `category` (optional): Filter by category
- `limit` (optional): Number of templates to return

#### Response
```json
{
  "templates": [
    {
      "id": "template_xyz789",
      "name": "CBT Thought Record",
      "description": "Template for identifying and challenging negative thoughts",
      "approach": "cbt",
      "category": "thought_patterns"
    }
  ],
  "total": 25,
  "has_more": false
}
```

## Analytics

### Get Usage Statistics
`GET /analytics/usage`

Retrieve usage statistics for your account.

#### Query Parameters
- `start_date`: Start date for the analysis period
- `end_date`: End date for the analysis period
- `metrics`: Comma-separated list of requested metrics

#### Response
```json
{
  "total_prompts": 145,
  "prompts_by_approach": {
    "cbt": 80,
    "act": 45,
    "motivational": 20
  },
  "usage_by_date": {
    "2024-03-19": 15,
    "2024-03-20": 12
  }
}
```

## Error Responses

All endpoints may return the following error responses:

### 400 Bad Request
```json
{
  "error": {
    "code": "invalid_request",
    "message": "Invalid parameters provided",
    "details": {
      "primaryConcern": "Required field missing"
    }
  }
}
```

### 401 Unauthorized
```json
{
  "error": {
    "code": "unauthorized",
    "message": "Invalid API key provided"
  }
}
```

### 429 Too Many Requests
```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "Rate limit exceeded",
    "reset_at": "2024-03-20T11:00:00Z"
  }
}
```

## Webhooks

### Register Webhook
`POST /webhooks`

Register a new webhook for event notifications.

#### Request Body
```json
{
  "url": "https://your-domain.com/webhook",
  "events": ["prompt.created", "prompt.updated"],
  "secret": "your_webhook_secret"
}
```

#### Response
```json
{
  "id": "webhook_456def",
  "url": "https://your-domain.com/webhook",
  "events": ["prompt.created", "prompt.updated"],
  "created_at": "2024-03-20T10:30:00Z"
}
```

## Next Steps

- Learn about [Rate Limits](./rate-limits.md)
- Understand [Error Handling](./error-handling.md)
- Review [Authentication](./authentication.md)
- Explore [Integration Guides](../integrations/practice-management.md) 