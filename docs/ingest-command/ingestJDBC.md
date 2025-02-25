# IngestJDBC Command Documentation - Coming Soon

### **Overview**

The **IngestJDBC** command is used to ingest data from a JDBC-compatible database into your pipeline. This command allows you to extract data from relational databases and bring it into your data pipeline. It supports **incremental loading**, dynamically fetching the last processed value from the source database. This improves performance by only processing new or modified data since the last execution.

With the ability to define **lower** and **upper bounds**, the system can dynamically query the source database for the incremental values based on a specific column, ensuring only the relevant data is ingested.

### **IngestJDBC Command Structure**

| Parameter              | Type     | Required | Description                                                                 |
|------------------------|----------|----------|-----------------------------------------------------------------------------|
| `type`                 | String   | ✅ Yes    | The type of command, always set to `IngestJDBC`.                            |
| `connection_name`      | String   | ✅ Yes    | The name of the connection to the database (referenced from Connection Properties). |
| `query`                | String   | ✅ Yes    | The SQL query to retrieve data from the source database.                    |
| `lower_bound_query`    | String   | ❌ No     | The SQL query used to get the lower bound value for incremental loading.    |
| `upper_bound_query`    | String   | ❌ No     | The SQL query used to get the upper bound value for incremental loading.    |
| `destination`          | Object   | ✅ Yes    | The destination configuration where the ingested data will be written.     |
| `batch_size`           | Integer  | ❌ No     | The number of rows to fetch per batch during data ingestion.                |

---

### **Detailed Explanation of Parameters**

- **`type`**: Always set to `"IngestJDBC"`. This identifies the command type as a JDBC ingestion command.

- **`connection_name`**: Specifies the connection to be used for connecting to the source database. The connection name must correspond to a pre-defined connection in the **Connection Properties** section.

- **`query`**: The SQL query used to retrieve data from the source database. It should include a condition based on the **incremental_column** if incremental loading is enabled.

- **`lower_bound_query`**: An optional SQL query that dynamically fetches the lower bound (the starting point) for the incremental load. This value can be used to determine the beginning of the range of data to be fetched. For example, it could be the maximum value of the `incremental_column` from the previous ingestion.

- **`upper_bound_query`**: An optional SQL query that dynamically fetches the upper bound (the ending point) for the incremental load. This value can be used to determine the end of the range for data to be fetched. This ensures that only data within this range will be ingested in the next execution.

- **`batch_size`**: Defines the number of rows to fetch per batch from the source database. Fetching data in batches can improve performance and prevent memory overload.

---

### **Example IngestJDBC Command with Dynamic Incremental Load**

Here’s an example of how the **IngestJDBC** command might be configured to perform incremental loading with dynamically fetched lower and upper bounds:

```json
{
  "execution": [
    {
      "type": "IngestJDBC",
      "name": "jdbc_connection_customers",
      "connection_name": "jdbc_connection",
      "query": "SELECT * FROM crm.customers WHERE updated_at BETWEEN '{{lower_bound_value}}' AND '{{upper_bound_value}}'",
      "lower_bound_query": "SELECT last_run from stats.incremental where name='jdbc_connection_customers'",
      "upper_bound_query": "SELECT MAX(updated_at) FROM crm.customers",
      "incremental_value_storage": {
        "type": "table",
        "connection": "stats.incremental",
      }
      "batch_size": 1000
    }
  ]
}
```

### **Conclusion**

The "IngestJDBC" command with dynamic lower and upper bound queries enables more flexible and efficient incremental data loading. By querying the database for the appropriate range of data (via lower_bound_query and upper_bound_query), this approach avoids redundant data loads and ensures that only relevant data is processed.

This dynamic approach to handling incremental data ingestion is ideal for large databases or when frequent data loads are required, as it reduces the amount of data ingested and improves pipeline performance.

By leveraging SQL queries for both incremental bounds and the actual data fetch, you gain fine-grained control over the data extraction process. This configuration is highly customizable, allowing you to handle a variety of data sources and update scenarios.


