
# Kafka Batch Ingestion Configuration

### Kafka Batch Ingestion Configuration Example

To ingest data from a Kafka topic in **batch mode**, you would typically configure your pipeline to read data from Kafka at fixed intervals, similar to how batch jobs are run. Below is an example configuration for ingesting data in batch mode from Kafka.

```json
{
  "execution": [
    {
      "type": "IngestKafka",
      "bootstrap_servers": "localhost:9092",
      "topic": "example-topic",
      "group_id": "batch-consumer-group",
      "key_deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
      "value_deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
      "auto_offset_reset": "earliest",
      "batch_interval": 60000,  // 60 seconds, adjust as needed
      "max_poll_records": 1000,
      "additional_attributes": [
        {
          "key": "enable.auto.commit",
          "value": "false"
        }
      ]
    }
  ]
}
```

---

### Kafka Batch Ingestion Command Documentation 📥

The **KafkaReadCommand** can be used in **batch mode** to periodically read messages from a Kafka topic at specified intervals. The configuration includes parameters to handle batch timing, max poll records, and other Kafka consumer settings.

#### JSON Configuration Example

```json
{
  "execution": [
    {
      "type": "KafkaRead",
      "bootstrap_servers": "localhost:9092",
      "topic": "example-topic",
      "group_id": "batch-consumer-group",
      "key_deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
      "value_deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
      "auto_offset_reset": "earliest",
      "batch_interval": 60000,  // 60 seconds, adjust as needed
      "max_poll_records": 1000,
      "additional_attributes": [
        {
          "key": "enable.auto.commit",
          "value": "false"
        }
      ]
    }
  ]
}
```

---

### Parameters

| Parameter              | Type    | Required | Description |
|------------------------|---------|----------|-------------|
| `type`                 | String  | ✅ Yes    | The type of command (`KafkaReadCommand`). |
| `bootstrap_servers`    | String  | ✅ Yes    | The Kafka cluster address (e.g., `localhost:9092`). |
| `topic`                | String  | ✅ Yes    | The Kafka topic from which data will be consumed. |
| `group_id`             | String  | ✅ Yes    | The consumer group ID for Kafka. |
| `key_deserializer`     | String  | ✅ Yes    | Deserializer for the Kafka message key (e.g., `org.apache.kafka.common.serialization.StringDeserializer`). |
| `value_deserializer`   | String  | ✅ Yes    | Deserializer for the Kafka message value (e.g., `org.apache.kafka.common.serialization.StringDeserializer`). |
| `auto_offset_reset`    | String  | ✅ Yes    | Determines what to do when there is no initial offset or the offset is out of range (`earliest` or `latest`). |
| `batch_interval`       | Integer | ✅ Yes    | Defines the batch interval in milliseconds (e.g., `60000` for 60 seconds). |
| `max_poll_records`     | Integer | ✅ Yes    | Specifies the maximum number of records to fetch in each poll (e.g., `1000`). |
| `additional_attributes`| Array   | ❌ No     | Additional Kafka consumer settings, such as enabling auto-commit or configuring poll records. |

---

### Batch Mode Specific Parameters

- **`batch_interval`**: Specifies the frequency (in milliseconds) at which the data will be ingested in batch mode. For example, setting this to `60000` means Kafka will be polled every 60 seconds for new data.
  
- **`max_poll_records`**: Controls the maximum number of records to fetch in each batch. Adjust this based on your performance needs.

---

### Example Use Case

**Scenario:** You want to read data from the `example-topic` Kafka topic in batch mode every 60 seconds, using a consumer group called `batch-consumer-group`, with a maximum of 1000 records per poll.

#### JSON Configuration:

```json
{
  "execution": [
    {
      "type": "KafkaRead",
      "bootstrap_servers": "localhost:9092",
      "topic": "example-topic",
      "group_id": "batch-consumer-group",
      "key_deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
      "value_deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
      "auto_offset_reset": "earliest",
      "batch_interval": 60000,  // 60 seconds, adjust as needed
      "max_poll_records": 1000,
      "additional_attributes": [
        {
          "key": "enable.auto.commit",
          "value": "false"
        }
      ]
    }
  ]
}
```

---

### Behavior

- **`batch_interval`**: The frequency at which the pipeline reads messages from Kafka. In batch mode, the data is ingested periodically rather than continuously. For example, if set to `60000`, the pipeline will poll Kafka every 60 seconds for new messages.
  
- **`max_poll_records`**: Controls how many records will be fetched in a single batch. Set this based on the expected load and performance requirements.

- **`auto_offset_reset`**: Determines where to start consuming Kafka messages if no offset is committed. `earliest` means that messages will be consumed from the beginning of the topic, and `latest` means consumption will begin with the newest messages.

- **`additional_attributes`**: Allows additional settings for the Kafka consumer. For example, setting `enable.auto.commit` to `false` ensures that offsets are not automatically committed, giving you more control over when offsets are committed.

---

### Related Commands



---

### Conclusion

The **KafkaReadCommand** in **batch mode** is a powerful way to periodically ingest data from Kafka topics. By configuring parameters like **`batch_interval`**, **`max_poll_records`**, and **`auto_offset_reset`**, you can control how and when Kafka data is ingested, making it well-suited for periodic or batch-based processing in your data pipeline.
