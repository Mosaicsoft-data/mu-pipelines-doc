# Connection Properties Documentation (Coming Soon)

### **Overview**

Connection properties are used to define the connection settings between the data pipeline and various external systems (e.g., databases, file storage, message queues). These properties allow you to configure how your data pipeline interacts with the source and destination systems, ensuring that it can securely and efficiently read from and write to external resources.

### **Connection Properties Structure**

Connection properties typically include the following key parameters:

| Parameter             | Type    | Required | Description                                                                 |
|-----------------------|---------|----------|-----------------------------------------------------------------------------|
| `name`     | String  | ✅ Yes    | The unique name used to identify the connection configuration.               |
| `host`                | String  | ✅ Yes    | The host URL or IP address of the external system (e.g., database or server).|
| `port`                | Integer | ✅ Yes    | The port number used for the connection.                                     |
| `username`            | String  | ✅ Yes    | The username required to authenticate to the external system.               |
| `password`            | String  | ✅ Yes    | The password associated with the username for authentication.               |
| `database_name`       | String  | ✅ Yes    | The name of the database or schema to connect to.                           |
| `ssl_enabled`         | Boolean | ❌ No     | Whether to use SSL encryption for the connection (default: `false`).         |
| `ssl_cert`         | String | ❌ No     | Path to your certificate  (default: `false`).         |
| `timeout`  | Integer | ❌ No     | The timeout value for establishing a connection (in seconds).                |
| `additional_attributes`       | Object  | ❌ No     | Additional options or parameters specific to the type of connection (e.g., pool_size). |

---

### **Detailed Explanation of Parameters**

- **`name`**: This parameter is used to uniquely identify a connection configuration. It allows you to reference the connection easily when defining sources or destinations in the pipeline configuration.

- **`host`**: Specifies the host or IP address of the external system to which the pipeline will connect. This could be a database server, cloud storage endpoint, or a message queue system.

- **`port`**: The port number used by the external system for communication. For example, databases typically use ports like `5432` for PostgreSQL or `3306` for MySQL. If no specific port is needed, the default port will be used based on the service type.

- **`username`**: The username for authentication to the external system. This credential is used to securely access the database, file system, or other resource. It is important to keep this value secure. It can be accessed from your own secret manager using secrets_properties. 

- **`password`**: The password corresponding to the username for authentication. It is important to securely store and encrypt this value in configuration files to prevent unauthorized access. It can be accessed from your own secret manager using secrets_properties. 

- **`database_name`**: The name of the database or schema you want to connect to. This parameter is especially important when working with SQL databases or systems that have multiple schemas or databases.

- **`ssl_enabled`**: A boolean value that specifies whether to use SSL (Secure Sockets Layer) encryption for the connection. This is important for securing data transmission between the pipeline and the external system. If set to `true`, SSL encryption will be used.

- **`ssl_cert`**: If ssl_enabled is true then retrive the certificate from you certificate manager. It can be accessed from your own secret manager using secrets_properties. 

- **`timeout`**: Defines the timeout period (in seconds) for establishing the connection. If the connection cannot be established within this time, the attempt will be aborted. This parameter helps manage connection failures gracefully.

- **`additional_attributes`**: An optional object to provide additional configuration settings specific to the connection. For instance, you might need to provide connection pooling settings, or other system-specific parameters.

---

### **Example Connection Configuration**

Here’s an example of how connection properties might look in a JSON configuration for connecting to a PostgreSQL database:

```json
{
  "connection_properties": {
    "name": "postgres_connection",
    "host": "db.example.com",
    "port": 5432,
    "username": {
      "secert_name": "my_aws", 
      "secret_value":"postgres-user-name"
    },
    "password": {
      "secert_name": "my_aws", 
      "secret_value":"postgres-password"
    },
    "database_name": "data_pipeline_db",
    "ssl_enabled": true,
    "ssl_cert": {
          "secert_name": "certs_manager", 
          "secret_value":"postgres_cert"
      },
    "timeout": 30,
    "additional_attributes": {
      "pool_size": 10
    }
  }
}

```
### **Conclusion**

The **Connection Properties** are essential for establishing secure and efficient connections between your data pipeline and external systems. By defining these properties, you can configure various connection settings such as authentication, encryption, timeouts, and more. This flexibility ensures your pipeline can seamlessly interact with different data sources and destinations, whether it's a database, file system, or message queue.

Proper management of connection properties is key to ensuring smooth and reliable data flow across your pipeline. Security features like SSL encryption, as well as customizable timeouts and additional settings, allow for a secure and performant connection to external resources.

Incorporating these connection properties within your pipeline configuration allows you to easily manage different environments, credentials, and connection settings, ultimately leading to a more robust and secure data integration process.
