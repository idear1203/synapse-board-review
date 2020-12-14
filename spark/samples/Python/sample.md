# Synapse Spark champion scenarios

## Creating Synapse Spark client
```python
from azure.identity import ClientSecretCredential
from azure.synapse.spark import SparkClient

credential = ClientSecretCredential(
    tenant_id = "AZURE_TENANT_ID",
    client_id = "AZURE_CLIENT_ID",
    client_secret = "AZURE_CLIENT_SECRET"
    )

workspace_endpoint = "https://<workspace_name>.dev.azuresynapse.net"
sparkpool_name = "SPARKPOOL_NAME"

spark_client = SparkClient(credential, workspace_endpoint, sparkpool_name)
```

## Scenario 1: `Spark Bacth Job` creation
```python
batchJob = SparkBatchJobOptions(
    name = "WordCount_Java", 
    file = "abfss://filesystem@adlsgen2account.dfs.core.windows.net/samples/java/wordcount/wordcount.jar",
    class_name = "WordCount",
    args = ["abfss://filesystem@adlsgen2account.dfs.core.windows.net/samples/java/wordcount/shakespeare.txt",
            "abfss://filesystem@adlsgen2account.dfs.core.windows.net/samples/java/wordcount/result/"],
    driver_memory = "4g",
    driver_cores = 4,
    executor_memory = "4g",
    executor_cores = 4,
    num_executors = 2)

create_result = spark_client.spark_batch.create_spark_batch_job(batchJob, True)
```

## Scenario 2: `Spark Bacth Job` get/list/cancel

### Get
```python
get_result = spark_client.spark_batch.get_spark_batch_job(batch_id)
```

### List
```python
list_result = spark_client.spark_batch.get_spark_batch_jobs()
```

### Cancel
```python
spark_client.spark_batch.cancel_spark_batch_job(batch_id)
```

## Scenario 3: `Spark Session` creation
```python
sparkSession = SparkSessionOptions(
    name = "sessionName",
    executorCount = 2,
    driverCores = 4,
    driverMemory = "8g",
    executorCores = 4,
    executorMemory = "8g")

create_result = spark_client.spark_session.create_spark_session(sparkSession, True)
```

## Scenario 4: `Spark Session` get/list/cancel

### Get
```python
get_result = spark_client.spark_session.get_spark_session(session_id)
```

### List
```python
list_result = spark_client.spark_session.get_spark_sessions()
```

### Cancel
```python
spark_client.spark_session.cancel_spark_session(session_id)
```


## Scenario 5: `Spark Statement` creation
```python
sparkStatement = SparkStatementOptions(
    code = "<customer running code>",
    kind = "spark")

create_result = spark_client.spark_session.create_spark_statement(session_id, sparkStatement)
```

## Scenario 6: `Spark Statement` get/list/cancel

### Get
```python
get_result = spark_client.spark_session.get_spark_statement(session_id, statement_id)
```

### List
```python
list_result = spark_client.spark_session.get_spark_statement(session_id)
```

### Cancel
```python
spark_client.spark_session.cancel_spark_statement(session_id, statement_id)
```