# TransformSQL Command Documentation - Coming Soon

### **TransformSQL Command Configuration Example**

The **TransformSQL** command allows you to apply SQL transformations to your data before it is written to the destination. It is useful for performing data processing, filtering, aggregations, and other SQL-based operations within your data pipeline.

```json
{
  "execution": [
    {
      "type": "TransformSQL",
      "query": "SELECT * FROM raw_data WHERE age > 18"
    }
  ]
}

```

### **Detailed Explanation of Parameters**

- **`type`**: Always set to `"TransformSQL"`. This parameter indicates that the command is executing a SQL transformation. It is used to identify the command type within the pipeline configuration.

- **`query`**: The SQL query that will be executed on the source data. This query can contain all valid SQL operations such as `SELECT`, `WHERE`, `JOIN`, `GROUP BY`, and other SQL constructs. It is the core of the transformation and allows you to filter, aggregate, or manipulate the data before it is written to the destination. It can also be a file and provide file for sql statement

---

### **Conclusion**

The **TransformSQL** command is a powerful tool that enables users to perform SQL-based transformations on data within a pipeline. It provides an easy-to-use interface for applying filters, aggregations, and other transformations using SQL queries, and the results can be stored in a designated destination. This allows data engineers to manage and manipulate data efficiently before it reaches its final destination.

The flexibility of SQL combined with the power of the pipeline framework makes **TransformSQL** an essential component for complex data workflows. By leveraging SQL, users can write complex transformations in a familiar and scalable manner, ensuring data quality and enabling the right processing logic for their applications.

Whether it's filtering records, joining tables, or performing complex aggregations, the **TransformSQL** command simplifies the integration of SQL-based logic within the data pipeline, making it an indispensable tool for data transformation.
