# API Authentication

This guide explains how to authenticate with the Nurul API and manage your API keys.

## Overview

Nurul uses API keys to authenticate requests. You can view and manage your API keys in the [Dashboard](https://nurul.ai/dashboard/settings/api).

## Getting Your API Key

1. Log in to your Nurul account
2. Navigate to Dashboard → Settings → API
3. Click "Generate New API Key"
4. Save your API key securely - it won't be shown again

## Using Your API Key

Include your API key in the Authorization header of your requests:

```bash
curl https://api.nurul.ai/v1/prompts \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## API Key Best Practices

### Security
- Never share your API key
- Don't commit API keys to version control
- Rotate keys periodically
- Use environment variables

### Key Management
- Use different keys for development and production
- Name your keys descriptively
- Monitor key usage
- Revoke unused keys

## Rate Limits

Rate limits are based on your subscription tier:

| Tier    | Requests/Day | Burst Limit |
|---------|-------------|-------------|
| Free    | 1           | 1/min       |
| Premium | 50          | 10/min      |
| Teams   | 500         | 50/min      |

## Error Handling

### Authentication Errors

```json
{
  "error": {
    "code": "unauthorized",
    "message": "Invalid API key provided"
  }
}
```

### Common Status Codes
- 401: Invalid API key
- 403: Valid key, but insufficient permissions
- 429: Rate limit exceeded

## Example Implementation

### JavaScript/Node.js
```javascript
const NURUL_API_KEY = process.env.NURUL_API_KEY;

async function generatePrompt(params) {
  const response = await fetch('https://api.nurul.ai/v1/prompts', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${NURUL_API_KEY}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(params),
  });
  
  return response.json();
}
```

### Python
```python
import os
import requests

NURUL_API_KEY = os.environ.get('NURUL_API_KEY')

def generate_prompt(params):
    response = requests.post(
        'https://api.nurul.ai/v1/prompts',
        headers={
            'Authorization': f'Bearer {NURUL_API_KEY}',
            'Content-Type': 'application/json',
        },
        json=params,
    )
    
    return response.json()
```

## Next Steps

- Review the [API Endpoints](./endpoints.md) documentation
- Learn about [Rate Limits](./rate-limits.md)
- Understand [Error Handling](./error-handling.md)
- Check out our [Integration Guides](../integrations/practice-management.md) 