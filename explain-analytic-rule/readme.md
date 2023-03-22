# Explain Analytic Rule

## Application logic
![image](https://user-images.githubusercontent.com/25780196/226946078-9e03c39a-2795-4d51-a52f-aa719c741506.png)

### Get alert rule:
![image](https://user-images.githubusercontent.com/25780196/226946240-dc80d0c1-f00b-4636-9dc6-7e3cc0dd979d.png)

### Parse alert rule JSON with the following schema:
```json
{
    "properties": {
        "id": {
            "type": "string"
        },
        "kind": {
            "type": "string"
        },
        "properties": {
            "properties": {
                "description": {
                    "type": "string"
                },
                "displayName": {
                    "type": "string"
                },
                "lastModifiedUtc": {
                    "type": "string"
                },
                "query": {
                    "type": "string"
                },
                "severity": {
                    "type": "string"
                },
                "tactics": {},
                "techniques": {}
            },
            "type": "object"
        },
        "type": {
            "type": "string"
        }
    },
    "type": "object"
}
```

### Construct the prompt:
![image](https://user-images.githubusercontent.com/25780196/226946641-b53f0e9a-9536-4a98-8df8-343901baf129.png)

### Create the HTTP request to Azure OpenAI:
![image](https://user-images.githubusercontent.com/25780196/226947204-7b191797-d2e2-4cba-aef5-92ca946831b3.png)

### Parse JSON from chat completion:
```json
{
    "properties": {
        "choices": {
            "items": {
                "properties": {
                    "finish_reason": {},
                    "index": {
                        "type": "integer"
                    },
                    "logprobs": {},
                    "text": {
                        "type": "string"
                    }
                },
                "required": [
                    "text",
                    "index",
                    "finish_reason",
                    "logprobs"
                ],
                "type": "object"
            },
            "type": "array"
        },
        "created": {
            "type": "integer"
        },
        "id": {
            "type": "string"
        },
        "model": {
            "type": "string"
        },
        "object": {
            "type": "string"
        },
        "usage": {
            "properties": {
                "completion_tokens": {
                    "type": "integer"
                },
                "prompt_tokens": {
                    "type": "integer"
                },
                "total_tokens": {
                    "type": "integer"
                }
            },
            "type": "object"
        }
    },
    "type": "object"
}
```

### Define the response:
![image](https://user-images.githubusercontent.com/25780196/226947615-6380c553-07fa-4fee-9d40-acf1200ebba9.png)
