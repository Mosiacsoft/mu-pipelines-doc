# Welcome to Mu-Pipelines!

This guide will help you set up and run Mu-Pipelines.

## 1️⃣ Install Mu-Pipelines
Ensure you have Python 3 installed, then run:

```sh
pip install mu-pipelines
```

## 2️⃣ Create Config Files
Our config files are divided into two sections: `execute` and `destination`.

### Configuration Parameters:
- **execute-xx**: This can be ingesting data from a source or transforming using SQL/Python.
- **destination**: The destination where data should be stored.

Refer to the config documentation for a list of available `execute` and `destination` commands.

## 3️⃣ Run a Sample Config File
In your notebook or Python file, add the following code:

```python
from mu_pipelines_driver.run_config import run_config

df = run_config(
    [
        {
            "execution": [
                {
                    "type": "CSVReadCommand",
                    "file_location": "/home/iceberg/data/file/people.csv",
                    "delimiter": ",",
                    "quotes": "\"",
                    "additional_attributes": [
                        {"key": "header", "value": "True"}
                    ]
                }
            ],
            "destination": [
                {
                    "type": "table",
                    "table_name": "crm.raw.people",
                    "mode": "overwrite"
                }
            ]
        }
    ],
    {"library": "spark"},
    {"connections": []}
)
```

## 4️⃣ Run Config Using Spark Submit

Run your configuration using Spark Submit.

## 5️⃣ Run Config Using Airflow

Execute the config using Airflow for workflow orchestration.

## 6️⃣ Chain Different Configurations to Meet Business Needs

Mu-Pipelines allows you to chain multiple configurations together to address complex business requirements.

---
🎯 **Want to add a custom connector?** Stay tuned for developer guides!
