# Getting Started 🚀

Welcome! This guide helps you set up and run Mu-Pipelines.

## 1️ Install Mu-Pipelines
Ensure you have Python 3 installed, then run:
```sh
pip install mu-pipelines

## 2 Create Config files 
Our config files are divided in two section execute and destination 

Configuration Parameters:
execute-xx: This can be ingesting data from source or transforming using sql/python.
destination: The destination where data should be stored.

Refer config documentation for list of execute and destination command available 



## 3 Run a sample config file 

In your notebook/py file add below code 

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
                        { "key": "header", "value": "True" }
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
    {
        "library": "spark"
    },
    {
        "connections":[]
    }
)


##4 Run config using spark submit 


## Run config using Airflow 


## 5 Chain different config's to meet business needs 


🎯 Want to add a custom connector? Stay tuned for developer guides!