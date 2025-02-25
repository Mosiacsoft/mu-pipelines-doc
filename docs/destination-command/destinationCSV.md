# DestinationCSV Command Documentation

The **DestinationCSV** command is used to specify the destination for writing data in CSV format. This can be useful when you need to store processed or ingested data into CSV files. Below is an example configuration for writing data to a CSV file.

```json
{
  "destination": [
    {
      "type": "destinationCSV",
      "file_location": "/home/data/output/processed_data.csv",
      "delimiter": ",",
      "header": true,
      "quotes": "\"",
      "additional_attributes": [
        { "key": "mode", "value": "overwrite" }
      ]
    }
  ]
}

```

# DestinationCSV Command - Parameters

### **Parameters**

| Parameter             | Type    | Required | Description                                                                 |
|-----------------------|---------|----------|-----------------------------------------------------------------------------|
| `type`                | String  | ✅ Yes    | The type of command (`destinationCSV`).                                                  |
| `file_location`       | String  | ✅ Yes    | The location of the output CSV file. This can be a relative or absolute path. |
| `delimiter`           | String  | ✅ Yes    | The delimiter used to separate values in the CSV file (e.g., `,`, `;`, `\t`). |
| `header`              | Boolean | ✅ Yes    | Whether to include a header row in the CSV file (`true` or `false`).          |
| `quotes`          | String  | ✅ Yes    | The character used to quote strings in the CSV file (e.g., `"`).              |
| `additional_attributes`| Array   | ❌ No     | Additional attributes for customization (e.g., mode, append, etc.).           |

---

### **Detailed Explanation of Parameters**

- **`type`**: Always set to `"destinationCSV"`. This indicates that the destination is a CSV file.
  
- **`file_location`**: The file path where the CSV data will be written. This can be either an absolute or a relative file path. For example, `/home/data/output/processed_data.csv`. The file will be created at the given location if it does not already exist.

- **`delimiter`**: Specifies the character used to separate values in the CSV file. The default is a comma (`,`), but other characters such as semicolons (`;`) or tabs (`\t`) can be used.

- **`header`**: If set to `true`, the CSV file will include a header row containing the column names. If set to `false`, no header row will be included.

- **`quotes`**: Defines the character used to quote string values in the CSV file. This is typically used to enclose values that contain special characters or delimiters. The default is double-quote (`"`), but you can specify other characters like single-quote (`'`).

- **`additional_attributes`**: This is an optional parameter. It allows for extra configuration. For example, you might use this to specify the `mode` of writing to the file. Common modes are:
  - `overwrite`: Replaces the existing file if it exists.
  - `append`: Adds new data to the end of the existing file.

### **Conclusion**

The **DestinationCSV** command provides an easy way to write processed data into CSV files, with full control over the formatting, delimiters, headers, and other aspects of the CSV file. This configuration is particularly useful for creating human-readable, portable data files that can be easily shared or imported into other systems. It offers a simple interface for configuring output files, making it suitable for use cases where CSV files need to be written as a part of a data pipeline.

### **Related Commands**

- **IngestCSV**: Reads data from a CSV file and uses it as input for your data pipeline. This command is helpful when you're looking to ingest data from CSV files for further processing.
