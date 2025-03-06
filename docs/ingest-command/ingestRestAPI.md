
## **IngestRestAPI Documentation 📄 (Coming Soon)**

The `IngestRestAPI` command enables data ingestion from a REST API into your pipeline. It supports flexible configuration options like HTTP methods, authentication, headers, pagination, and more, making it easy to pull data from various APIs.

### **Parameters**

| Parameter              | Type    | Required   | Description |
|------------------------|---------|----------- |-------------|
| `type`                 | String  | ✅ Yes    | Specifies the type of the command (`IngestRestAPI`). |
| `endpoint`        | String  | ✅ Yes    | The URL of the API endpoint. |
| `method`            | String  | ✅ Yes    | The HTTP method to use (GET, POST, etc.).
 |
| `headers`               | Object  | ❌ No     | Key-value pairs for API headers (e.g., Authorization). |
| `body`               | Object  | ❌ No     | The request body for POST or PUT requests. Dynamic value can be calculated using a UDF function defined by customer |
| `query_params`               | Object  | ❌ No     | Key-value pairs for query parameters. |
| `pagination`               | Object  | ❌ No     | Details for handling paginated responses. |
| `additional_attributes` | Array   | ❌ No    | Optional attributes to specify additional settings. Each attribute consists of a `key` and `value` pair. For example, you can specify if the CSV has headers. |

---

### **Additional Attributes Example**

The `additional_attributes` parameter allows users to specify extra properties for the CSV file:

- **key**: The name of the attribute.
- **value**: The value associated with the attribute.

#### **Example of timeout Attribute**

```json
"additional_attributes": [
  {
    "key": "timeout",
    "value": "30"
  }
]
```

This indicates timeout connection after 30 seconds.

---

### **Pagination Example**

The `pagination` parameter helps handle APIs that return data in pages.

``` json

"pagination": {
  "type": "cursor",
  "cursor_param": "next_page_token",
  "initial_value": ""
}
```

### **Dynamic Body Example**

The `body` parameter defines body to pass during PUT or POST request. It can be dynamically calculated using python code. Return of python code is body that will be appended during API request. In case of static body return the static value in python code

``` json

"body": {
    "execution":
    {
      "type": "TransformPython",
      "code_file": "my_user_api_body.py"
    }  
}
```

User TransformSQL or TransformPython to dynamically calculate your body

---

### **Dynamic Query Params**

The `query_params` parameter defines parameters that get appended to URL. They can be static list based on key, value pair or dynamically retrived from sql query as needed

``` json

"query_params": {
  "key": "updated_at",
  "value": {
    "execution":
    {
      "type": "TransformSQL",
      "query": "SELECT max(last_call_date) from api_history_calls where type = 'my_api_users' "
    }
  }
  }

```
User TransformSQL or TransformPython to dynamically calculate your body


---

### **Example Use Case**

**Scenario:** You want to pull user data from an Rest API that requires an API key and supports pagination.


#### **JSON Configuration:**

```json
{
  "execution": [
    {
      "type": "IngestRESTAPI",
      "endpoint": "https://api.example.com/users",
      "method": "GET",
      "headers": {
        "Authorization": {
            "connection_name": "my_JWT_TOKEN"
          },
        "Content-Type": "application/json"
      },
      "query_params": {
        {"key": "status", "value": "active"}
      },
      "pagination": {
        "type": "page",
        "page_param": "page",
        "initial_value": 1
      },
      "additional_attributes": [
        {
          "key": "timeout",
          "value": "30"
        }
      ]
    }
  ]
}

```


### **Conclusion**

The **IngestRESTAPI** command makes it simple to fetch data from REST APIs, handle headers, query params, and pagination, all through configuration files — no need to write custom scripts! 🚀
