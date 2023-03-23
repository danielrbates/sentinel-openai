# Explain Analytic Rule

## Application logic
![image](https://user-images.githubusercontent.com/25780196/227287974-141ca5ab-5ef9-4a69-945b-9b6a24952cc4.png)

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

### Define parameters for the Azure OpenAPI request
* Get API key from Key Vault
* Define Service Endpoint variable
* Define Service deployment model name
* Define prompt variables (temperature, max_tokens, etc) - can be done in the HTTP request itself

### Write the user and system context messages:
![image](https://user-images.githubusercontent.com/25780196/227288907-b920d7bb-34e4-482c-9858-8f7c6e729435.png)

### Construct the prompt (array variable):
![image](https://user-images.githubusercontent.com/25780196/227289017-d15dd353-43ea-40b3-a294-63a016b9fdb5.png)

### Create the HTTP request to Azure OpenAI:
![image](https://user-images.githubusercontent.com/25780196/227289084-0046161a-591f-4194-bb01-8b5525fd1d53.png)

### Parse JSON from chat completion:
```json
{
    "properties": {
        "choices": {
            "items": {
                "properties": {
                    "finish_reason": {
                        "type": "string"
                    },
                    "index": {
                        "type": "integer"
                    },
                    "message": {
                        "properties": {
                            "content": {
                                "type": "string"
                            },
                            "role": {
                                "type": "string"
                            }
                        },
                        "type": "object"
                    }
                },
                "required": [
                    "index",
                    "finish_reason",
                    "message"
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

```json
body('Parse_JSON_from_chat_completion')?['choices']?[0]?['message']?['content']
```
