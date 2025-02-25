
## **Default Catalog as Destination Documentation 📊**

The **DestinationDefaultCatalog** destination configuration allows you to define where the data will be written in the pipeline. The destination can specify an **table** where data will be loaded, and it supports different **modes** for managing data. It can be any **hive metastore, spark managed catalog table, iceberg, delta**. It uses default spark catalog to push data to. 


### **Parameters**

| Parameter         | Type    | Required | Description |
|-------------------|---------|----------|-------------|
| `type`            | String  | ✅ Yes    | The destination type (`DestinationDefaultCatalog` for Iceberg tables). |
| `table_name`      | String  | ✅ Yes    | The name of the Iceberg table where data will be written. |
| `mode`            | String  | ✅ Yes    | Defines how the data is written to the table. Possible values: `overwrite`, `append`, etc. |

---

### **Mode Options**

- **`overwrite`**: Replaces the data in the specified table with the new data. Any existing records in the table will be deleted.
- **`append`**: Adds the new data to the existing records in the table without modifying the existing data.

---

### **Configuring Spark with Iceberg as the Default Catalog**

Please note similar steps can be applied for Hive, delta etc 

To ensure that **Apache Spark** can interact with **Iceberg** as the default catalog when using it as a destination, you must configure Spark with the appropriate catalog settings. By default, Spark uses **Hive** as its catalog. To set Iceberg as the default, follow these steps:

1. **Add Iceberg as a dependency**:
   You need to add the **Iceberg Spark extension** to your Spark setup. Ensure the correct version of Iceberg is available in your Spark environment. Add the following dependency to your Spark session configuration:

   ```bash
   --packages org.apache.iceberg:iceberg-spark3-runtime:0.13.1
   ```

   This will include the necessary Iceberg libraries for Spark.

2. **Configure the Default Catalog**:
   To set Iceberg as the default catalog in Spark, update the **Spark session** configuration. You can set Iceberg as the default catalog by using the following settings:

   ```bash
   spark.sql.catalog.spark_catalog org.apache.iceberg.spark.SparkSessionCatalog
   spark.sql.catalog.spark_catalog.type hadoop
   spark.sql.catalog.spark_catalog.warehouse /path/to/warehouse
   ```

   - `spark_catalog` refers to the catalog in use (in this case, Iceberg).
   - The `warehouse` location should point to the directory where your Iceberg tables are stored.

   With this configuration, Spark will use **Iceberg** as the default catalog for reading and writing tables.

3. **Setting Iceberg Table for the Destination**:
   Once Iceberg is set as the default catalog, you can specify the destination table in your pipeline configuration, like so:

   ```json
   {
     "destination": [
       {
         "type": "DestinationDefaultCatalog",
         "table_name": "crm.raw.people",
         "mode": "overwrite"
       }
     ]
   }
   ```

   Here, `crm.raw.people` refers to an Iceberg table that will be written to, and **Spark** will handle the interaction with the Iceberg catalog.

---

### **Example Use Case**

**Scenario:** You want to write data to the **`crm.raw.people`** Iceberg table and overwrite any existing records.

#### **JSON Configuration:**

```json
{
  "destination": [
    {
      "type": "DestinationDefaultCatalog",
      "table_name": "crm.raw.people",
      "mode": "overwrite"
    }
  ]
}
```

---

### **Behavior**

- **`table_name`**: Specifies the Iceberg table where the data should be loaded.
- **`mode`**: Controls how the data is written to the destination table. Choose **`overwrite`** to replace existing data or **`append`** to add new records to the existing data.

---

### **Related Commands**

- **TransformSQL**: For transforming the data before writing it to the destination.

---

### **Conclusion**

The **DestinationDefaultCatalog** command provides a simple and effective way to write data into **Default catalog tables** with flexible write modes like `overwrite` and `append`. Configuring Spark with Iceberg as the default catalog makes it easier to work with Iceberg tables without needing to manually specify the catalog for each interaction. Once configured, use this command to manage your data pipeline outputs in a distributed, scalable table format.
