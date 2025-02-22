
## **IngestCSV Documentation 📄**

The `IngestCSV` is used to read and load data from a **CSV file** into the pipeline. It provides configuration options like **file location**, **delimiter**, **quote characters**, and **headers** to accommodate different CSV formats.

### **JSON Configuration Example**

```json
{
  "execution": [
    {
      "type": "IngestCSV",
      "file_location": "/home/iceberg/data/file/people.csv",
      "delimiter": ",",
      "quotes": """,
      "additional_attributes": [
        {
          "key": "header",
          "value": "True"
        }
      ]
    }
  ]
}
```

---

### **Parameters**

| Parameter              | Type    | Required   | Description |
|------------------------|---------|----------- |-------------|
| `type`                 | String  | ✅ Yes    | Specifies the type of the command (`CSVReadCommand`). |
| `file_location`        | String  | ✅ Yes    | The path to the CSV file to be read. Can be absolute or relative. |
| `delimiter`            | String  | ❌ No     | The character used to separate columns in the CSV (default is `,`). |
| `quotes`               | String  | ❌ No     | The character used for quoting text in CSV (default is `"`). |
| `additional_attributes` | Array   | ❌ No    | Optional attributes to specify additional settings. Each attribute consists of a `key` and `value` pair. For example, you can specify if the CSV has headers. |

---

### **Additional Attributes Example**

The `additional_attributes` parameter allows users to specify extra properties for the CSV file:

- **key**: The name of the attribute.
- **value**: The value associated with the attribute.

#### **Example of Header Attribute**

```json
"additional_attributes": [
  {
    "key": "header",
    "value": "True"
  }
]
```

This indicates that the first row in the CSV file should be treated as column headers.

---

### **Example Use Case**

**Scenario:** You need to read a CSV file named `people.csv` that has headers and uses commas as delimiters.

#### **JSON Configuration:**

```json
{
  "execution": [
    {
      "type": "CSVRead",
      "file_location": "/home/iceberg/data/file/people.csv",
      "delimiter": ",",
      "quotes": """,
      "additional_attributes": [
        {
          "key": "header",
          "value": "True"
        }
      ]
    }
  ]
}
```

---

### **Behavior**

- **`file_location`**: Specifies the file to be read. Ensure the path is correct.
- **`delimiter`**: By default, CSV files are comma-delimited, but this can be customized for other formats (e.g., semicolons).
- **`quotes`**: Handles quoted values in CSV files (e.g., `"John, Doe"`).
- **`header`**: If set to `True`, the first row is treated as column headers.

---

### **Related Commands**

- **destinationCSV**: For writing data back into a CSV file.
- **TransformSQL**: For transforming the data after reading it.

---

### **Conclusion**

The **CSVRead** is a flexible and configurable way to read CSV files into your pipeline, allowing for custom delimiters, quotes, and handling of headers.
