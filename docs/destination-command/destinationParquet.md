# DestinationParquet Command Documentation (Coming Soon)

The **DestinationParquet** command is used to specify the destination for writing data in parquet format. Parquet is a popular columnar storage format known for its efficient compression and fast read performance. This guide will walk you through configuring a Parquet destination for your data pipeline.

```json
{
  "destination": [
    {
      "type": "destinationParquet",
      "file_location": "/home/data_lake/contacts/",
       "partition_columns": ["date", "region"],
       "compression": "snappy",
       "additional_attributes": [
          { "key": "parquet.encryption.column.keys", "value": "SSNKey:SSN" },
          { "key": "overwrite", "value": "true" }
      ]
    }
  ]
}

```

# destinationParquet Command - Parameters

### **Parameters**

| Parameter             | Type    | Required | Description                                                                 |
|-----------------------|---------|----------|-----------------------------------------------------------------------------|
| `type`                | String  | ✅ Yes    | The type of command (`destinationParquet`).                                                  |
| `file_location`       | String  | ✅ Yes    | The location of the output parquet files. This can be a relative or absolute path. |
| `partition_columns`           | String  |  ❌ No    | Columns to partition the data by, improving query performance |
| `compression`          | String  |  ❌ No    | Compression codec for the Parquet file (snappy, gzip, brotli, etc.). Default is snappy              |
| `additional_attributes`| Array   | ❌ No     | Additional attributes for customization (e.g., mode, append, etc.).           |

---

### **Detailed Explanation of Parameters**

- **`type`**: Always set to `"destinationParquet"`. This indicates that the destination is a Parquet file.
  
- **`file_location`**: The file path where the Parquet data will be written. This can be either an absolute or a relative file path. For example, `/home/data_lake/contacts/`. Files will be created at the given location if it does not already exist.

- **`partition_columns`**: Columns to partition the data by, improving query performance.

- **`compression`**: Compression codec for the Parquet file (snappy, gzip, brotli, etc.). Default is snappy.

The `additional_attributes` parameter allows users to specify extra properties for the Parquet write file:

- **key**: The name of the attribute.
- **value**: The value associated with the attribute.

#### **Example of Header Attribute**

```json
"additional_attributes": [
  {
    "key": "overwrite",
    "value": "true"
  }
]
```

### **Conclusion**

With Mu-Pipelines, writing to Parquet becomes effortless. Just configure your destination, and the framework handles the rest. 

### **Related Commands**

- **IngestParquet**: Reads data from a Parquet file and uses it as input for your data pipeline. This command is helpful when you're looking to ingest data from Parquet files for further processing.
