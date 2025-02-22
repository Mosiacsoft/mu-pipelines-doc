# Global Properties Documentation

### **Overview**

Global properties define configuration settings that apply across the entire data pipeline or Spark job execution. These properties typically control the environment, performance settings, logging configuration, and other global settings that can be shared across different commands in the pipeline. Configuring these properties helps ensure that your pipeline operates consistently and efficiently.

### **Global Properties Structure**

| Parameter             | Type    | Required | Description                                                                 |
|-----------------------|---------|----------|-----------------------------------------------------------------------------|
| `spark_master`        | String  | ✅ Yes    | The Spark master URL that defines the cluster to run Spark jobs on.         |
| `spark_app_name`      | String  | ✅ Yes    | The name of the Spark application.                                           |
| `spark_executor_cores`| Integer | ❌ No     | Number of cores to use for each executor in the Spark job.                   |
| `spark_executor_memory`| String | ❌ No     | Amount of memory to allocate for each Spark executor (e.g., "4g").           |
| `spark_driver_memory` | String  | ❌ No     | Amount of memory to allocate for the Spark driver (e.g., "2g").              |
| `spark_sql.shuffle_partitions` | Integer | ❌ No | Number of partitions to use when shuffling data in Spark SQL.                |
| `spark_event_log_dir` | String  | ❌ No     | Directory to store the event logs for Spark jobs.                            |
| `spark_conf`          | Object  | ❌ No     | Additional Spark configurations (e.g., custom settings for the Spark cluster).|

---

### **Detailed Explanation of Parameters**

- **`spark_master`**: Specifies the master URL for the Spark cluster. This defines where the Spark job should run. The value could be:
  - `"local"` for running Spark locally.
  - A URL for a cluster manager like `"spark://<host>:<port>"`.
  - `"yarn"` or `"mesos"` for distributed execution on YARN or Mesos clusters.

- **`spark_app_name`**: A string representing the name of the Spark application. This name will appear in the Spark UI and logs. It helps in identifying the application during job execution.

- **`spark_executor_cores`**: Defines how many cores to allocate for each executor. Executors are the processes running on worker nodes that execute Spark tasks. The number of cores can affect the parallelism of your tasks.

- **`spark_executor_memory`**: Specifies how much memory to allocate to each executor. For example, `"4g"` would allocate 4 GB of memory for each executor. The appropriate memory allocation depends on the size of the data and the tasks being executed.

- **`spark_driver_memory`**: Specifies how much memory to allocate to the Spark driver. The driver is responsible for maintaining the Spark application’s state, managing jobs, and scheduling tasks on executors. A higher memory allocation might be needed for large jobs.

- **`spark_sql.shuffle_partitions`**: Defines the number of partitions to use when shuffling data in Spark SQL operations. A higher number of partitions can improve parallelism but may increase overhead.

- **`spark_event_log_dir`**: Specifies the directory where Spark logs the events for the application. These logs are helpful for debugging and understanding the execution of the job.

- **`spark_conf`**: This parameter allows you to pass additional Spark configurations that are specific to your environment or application. For example, you can set Spark settings like `spark.sql.autoBroadcastJoinThreshold` to control the size of data broadcasted in joins.

---

### **Example Global Properties for Spark**

Here’s an example of a JSON configuration for Spark global properties:

```json
{
  "global_properties": {
    "spark_master": "spark://spark-cluster:7077",
    "spark_app_name": "data_pipeline_app",
    "spark_executor_cores": 4,
    "spark_executor_memory": "8g",
    "spark_driver_memory": "4g",
    "spark_sql.shuffle_partitions": 200,
    "spark_event_log_dir": "/tmp/spark-logs",
    "spark_conf": {
      "spark.sql.autoBroadcastJoinThreshold": "10485760",
      "spark.sql.shuffle.partitions": "100"
    }
  }
}
