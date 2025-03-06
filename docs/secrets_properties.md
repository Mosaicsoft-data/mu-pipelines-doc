# Secrets Properties Documentation (Coming Soon)

### **Overview**

Mu-Pipelines makes it easy to securely manage and access secrets by integrating with your favorite secret managers. You can choose from built-in connectors or bring your own implementation. Secrets can be provided in a single JSON block, giving you flexibility and simplicity in configuration.

### **How It Works**

**Choose a Secret Manager:** Use a supported provider (AWS, Azure, Databricks) or bring your own.

**Configure the Secret Source:** Define where secrets should be retrieved from.

**Use Secrets in Connection Properties:** Access secrets directly within your connection properties configuration files. 

### **Secrets Properties Structure**

| Parameter             | Type    | Required | Description                                                                 |
|-----------------------|---------|----------|-----------------------------------------------------------------------------|
| `name`     | String  | ✅ Yes    | The unique name used to identify the sceret configuration.                 |
| `provider`                | String  | ✅ Yes    | Type of provider (Hasicorp, Databricks, AWS (Coming Soon), Azure(Coming Soon, Bring your Own (Coming Soon))) |
| `additional_attributes`       | Object  | ❌ No     | Additional options or parameters specific to the type of scret (e.g., scope, key etc). |

---

### **Detailed Explanation of Parameters**

- **`name`**: This parameter is used to uniquely identify a secret configuration. It allows you to reference the secret easily when using in a connection property.

- **`provider`**: Specifies the what you are using as you provider. You can using inbuild connectors like Hasicorp, Databricks, AWS (Coming Soon), Azure(Coming Soon, Bring your Own (Coming Soon))

- **`additional_attributes`**: An optional object to provide additional configuration settings specific to the sceret. For instance, you might need to provide scope or key or region depending on the provider.

---

### **Example Secret Configuration**

Here’s an example of how secrets properties might look in a JSON configuration for connecting to a AWS and databricks database:

```json
{
  "secrets_properties": {
    "name": "my_aws",
    "provider":"AWS",
    "additional_attributes":{
        "region": "us-west-2",
        "secret_name": ["oracle-username", "oracle-password", "postgres-user-name", "postgres-password"]
    }
  },

  {
    "name": "community_databricks",
    "provider":"Databricks",
    "additional_attributes":{
       "scope": "my-secret-scope",
       "key": ["api_access_key", "erp_access_key"]
    }
  },

  {
    "name": "certs_manager",
    "provider":"s3",
    "additional_attributes":{
       "region": "us-west-2",
       "bucket_name": "certs",
       "key": ["oracle_cert", "postgres_cert"]
    }
  }

}

```

### **Related Commands**

- **connection-properties.json**: User secrets in your connection file.

### **Conclusion**

mu-pipelines makes secrets management flexible and secure. Whether you use a cloud provider or your own system, you can easily integrate and access secrets with minimal setup.

Want more integrations or help setting up your secrets? Get in touch with us!
