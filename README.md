# wso2ei-references
## Input json
```
{
  "config": {
    "request": {
      "method": "GET",
      "URL": "https://localhost:8244/test/0.0.1/get",
      "header": {
        "accept": "Accept",
        "contentType": "application/json",
        "acceptEncoding": "gzip, deflate, br",
        "connection": "keep-alive"
      },
      "authen": {
        "type": "oauth2",
        "basic": {
          "username": "admin",
          "password": "admin"
        },
        "oauth2": {
          "type": "client_credential",
          "flows": {
            "client_credential": {
              "token_url": "https://localhost:9444/oauth2/token",
              "client_id": "4sXmeiGEbiF3OHEHWydAMZoS_S8a",
              "client_secret": "jpU6Y6WpOxVIOQW1u6_q6n4yfx0a"
            }
          }
        }
      },
      "body": "$.payload"
    }
  },
  "payload": {
    "status": "DONE",
    "step": "image-converters",
    "xml": "<key></key>",
    "link": ""
  },
  "variable2": "value",
  "variable3": "value",
  "variable4": "value"
}

```
