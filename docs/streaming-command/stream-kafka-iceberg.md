# StreamKafkaIceberg Command Documentation - Coming Soon

### **Overview**

The **StreamKafkaIceberg** command facilitates the streaming ingestion of data from Apache Kafka into an Iceberg table. This command is ideal for real-time data pipelines where you want to capture streaming data from Kafka topics and store it in Iceberg tables with ACID compliance and schema evolution capabilities.

This command supports consuming data from Kafka topics in real-time and writing it to Iceberg tables, enabling you to leverage Iceberg's powerful features like partitioning, schema evolution, and efficient querying for analytical workloads.

### **StreamKafkaIceberg Command Structure**

| Parameter              | Type     | Required | Description                                                                 |
|------------------------|----------|----------|-----------------------------------------------------------------------------|
| `type`                 | String   | ✅ Yes    | Always set to `"StreamKafkaIceberg"`.                                         |
| `kafka_connection`     | String   | ✅ Yes    | The name of the Kafka connection (referenced from Connection Properties).    |
| `topic`                | String   | ✅ Yes    | The Kafka topic to consume from.                                              |
| `iceberg_table`        | String   | ✅ Yes    | The Iceberg table where the data will be written.                            |
| `checkpoint_location`  | String   | ✅ Yes    | The location for storing checkpoint information to track Kafka offsets.     |
| `group_id`             | String   | ✅ Yes    | The Kafka consumer group ID used to track message consumption.               |
| `format`               | String   | ✅ Yes    | The format to use for writing to the Iceberg table (e.g., `parquet`).        |
| `poll_timeout_ms`      | Integer  | ❌ No     | Timeout in milliseconds for polling data from Kafka (default: `1000`).       |
| `max_offset`           | Long     | ❌ No     | The maximum offset to consume up to from Kafka (default: latest offset).     |

---

### **Detailed Explanation of Parameters**

- **`type`**: Always set to `"StreamKafkaIceberg"`. This identifies the command type as a Kafka streaming ingestion command to an Iceberg table.

- **`kafka_connection`**: The name of the Kafka connection to use for consuming messages from Kafka. This connection is defined in the **Connection Properties** section, which specifies the necessary credentials and configurations to connect to the Kafka broker.

- **`topic`**: Specifies the Kafka topic to consume messages from. Kafka topics are logical channels that hold streams of data, and this parameter tells the system from which topic to read data.

- **`iceberg_table`**: The name of the Iceberg table to write the streaming data. This is where the data consumed from Kafka will be written. Iceberg tables provide strong consistency, partitioning, and support for schema evolution.

- **`checkpoint_location`**: The location to store Kafka offset information, ensuring that the consumer can resume from the last processed message in case of failure or restart. This is crucial for maintaining exactly-once processing semantics.

- **`group_id`**: The consumer group ID to track the Kafka consumer’s state. Multiple consumers can share the same group ID to divide the workload, and each group ID will independently keep track of the Kafka offset.

- **`format`**: The format for writing data to the Iceberg table. Common formats include `parquet`, `orc`, or `avro`. Parquet is often recommended due to its efficient columnar storage and compatibility with Iceberg.

- **`poll_timeout_ms`**: This optional parameter defines the timeout in milliseconds for polling new data from Kafka. The default is typically 1000ms, but you can adjust it based on the frequency of data and system responsiveness.

- **`max_offset`**: The maximum Kafka offset to consume messages up to. If not provided, it defaults to consuming from the latest offset, i.e., only new messages that arrive after the job starts.

---

### **Example StreamKafkaIceberg Command**

Below is an example configuration for streaming data from a Kafka topic into an Iceberg table:

```json
{
  "execution": [
    {
      "type": "StreamKafkaIceberg",
      "kafka_connection": "kafka_connection",
      "topic": "customer_events",
      "iceberg_table": "crm.raw.customer_events",
      "checkpoint_location": "/path/to/checkpoints",
      "group_id": "customer_events_consumer_group",
      "format": "parquet",
      "poll_timeout_ms": 2000,
      "max_offset": 1000000
    }
  ]
}

### **Conclusion**

The StreamKafkaIceberg command is an essential tool for real-time data ingestion in a data pipeline. It leverages Apache Kafka as a source for streaming data and Iceberg as the destination for structured and high-performance storage. This combination of streaming with Kafka and efficient data management with Iceberg enables the creation of scalable, reliable, and performant data pipelines.

With the ability to dynamically consume data from Kafka topics and write to Iceberg tables, you get the benefit of real-time analytics, partitioned storage, schema evolution, and ACID compliance.

By configuring checkpointing and offset management, this command supports fault tolerance and exactly-once processing semantics, ensuring your data pipeline is robust and capable of handling large volumes of real-time data.