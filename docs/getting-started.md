# Welcome to Mu-Pipelines!

This guide will help you set up and run Mu-Pipelines.

## 1️⃣ Install Mu-Pipelines
Ensure you have Python 3 installed, then run:

```sh
pip install 'mu-pipelines-driver[spark]'
```

## 2️⃣ Create Config Files
Our config files are divided into three sections: `ingest`, `transform` and `destination`.

### Configuration Parameters:
- **Ingestxx**: This is the source from where data needs to be ingested
- **Transformxx**: This is where you want to transform data
- **Destinationxx**: The destination where data should be stored.

Coming Soon 

- **Executexx**: Run any python execute commands. e.g. ExecuteZIP, ExecuteFileCopy, ExecuteFileEncrypt etc 
- **Validation**: Ability to run data quality checks based on parameters defined
- **Alerts**: Configure where you want to send alerts to 
- **Schedule**: Add a schedule for your job 
- **Dependency**: List of config's that the job is dependant on 

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

You can run a config in production spark by using spark submit 

Create a sample python script o import module 

``` Sample app_args.py file 
from mu_pipelines_driver.__main__ import main

main()

```

``` spark submit command
spark-submit /home/scripts/app_args.py --global-properties /home/scripts/global-properties.json --connection-properties /home/scripts/connection-properties.json /home/scripts/raw/people/people.json

```

## 5️⃣ Run Config Using Airflow

Execute the config using Airflow for workflow orchestration. Use spark connector in airflow to create issue a spark submit command 

## 6️⃣ Chain Different Configurations to Meet Business Needs

Mu-pipelines allows you to chain multiple configurations together to address complex business requirements.

---
🎯 **Want to add a custom connector?** Stay tuned for developer guides!

Need to connect with our team or have requests for specific connectors please email us at mupipelines@gmail.com

For more details please visit our website: https://mosaicsoft.wixsite.com/mu-pipelines

