# Synapse Artifacts champion scenarios

### Creating client
```python
from azure.identity import ClientSecretCredential
from azure.synapse.artifacts import ArtifactsClient

credential = ClientSecretCredential(
    tenant_id = "",
    client_id = "",
    client_secret = ""
    )

workspace_endpoint = "https://<workspace_name>.dev.azuresynapse.net"

artifacts_client = ArtifactsClient(credential, workspace_endpoint)

```

## Scenario 1: Get bigdata pool/sql pool/intergartion runtimes information under current workspace.

### Get bigdata pool
```python
artifacts_client.big_data_pools.get("big_data_pool_name")
```
### Get sql pool
```python
artifacts_client.sql_pools.get("sql_pool_name")
```
### Get integration runtime
```python
artifacts_client.integration_runtimes.get("integration_runtime_name")
```


## Scenario 2: Manage notebook resource.

### Get
```python
artifacts_client.notebook.get_notebook("<notebook_name>")
```

### List
```typescript
artifacts_client.notebook.get_notebook_summary_by_work_space()
artifacts_client.notebook.get_notebooks_by_workspace()
```

### Create
```python
languageInfo = NotebookLanguageInfo(name = "Python")
metadata = NotebookMetadata(language_info = languageInfo)
notebook = Notebook(
    nbformat = 4,
    nbformat_minor = 2,
    cells = [],
    metadata = metadata
)
notebookResource = NotebookResource(name="<notebook_name>", properties=notebook)
artifacts_client.notebook.begin_create_or_update_notebook("<notebook_name>", notebookResource)
```

### Delete
```python
artifacts_client.notebook.begin_delete_notebook()
```

## Scenario 3:  Manage dateflow resource.

### Get
```python
artifacts_client.data_flow.get_data_flow("<dataflow_name>")
```

### List
```python
artifacts_client.data_flow.get_data_flows_by_workspace()
```

### Create
```python
dataflowResource = DataFlowResource(
    properties = DataFlow(type="MappingDataFlow")
    )
artifacts_client.data_flow.begin_create_or_update_data_flow("<dataflow_name>", dataflowResource)
```

### Delete
```python
artifacts_client.data_flow.begin_delete_data_flow()
```

## Scenario 4:  Manage dateset resource.

### Get
```python
artifacts_client.dataset.get_dataset("<dataset_name>")
```

### List
```python
artifacts_client.dataset.get_datasets_by_workspace()
```

### Create
```python
linkedServiceReference = LinkedServiceReference(
        type="LinkedServiceReference",
        referenceName="testLinkedService"
        )

azureTable = AzureTableDataset(
    type="AzureTable",
    table_name="testTable",
    linked_service_name = linkedServiceReference
    )
    
artifacts_client.dataset.begin_create_or_update_dataset("<dataset_name>", azureTable)
```

### Delete
```python
artifacts_client.dataset.begin_delete_dataset("<dataset_name>")
```

## Scenario 5:  Manage pipeline resource.

### Get
```python
artifacts_client.pipeline.get_pipeline("<testpipeline>")
```

### List
```python
artifacts_client.pipeline.get_pipelines_by_workspace()
```

### Create
```python
pipelineResource = PipelineResource()
artifacts_client.pipeline.begin_create_or_update_pipeline("<testpipeline>", pipelineResource)
```

### Delete
```python
artifacts_client.pipeline.begin_delete_pipeline("<testpipeline>")
```

## Scenario 6:  Manage sqlscript resource.


## Scenario 7:  Manage linkedservice resource.


## Scenario 8:  Manage sparkjobdefinition resource.


## Scenario 9:  Manage trigger resource.

### Get
```python
artifacts_client.trigger.get_trigger("<testtriger>")
```

### Create
```python
triggerPipelineReference = TriggerPipelineReference(     
        referenceName = "testPipeline",
        type = "PipelineReference"
)

scheduleTrigger = ScheduleTrigger(
    type = "ScheduleTrigger",
    recurren = ScheduleTriggerRecurrence(
        frequency = "Minute",
        interval = 4,
        startTime = datetime(2020,1,26,11,11,11),
        endTime = datetime(2020,1,27,11,11,11),
        timeZone = "UTC"
    ),
    pipelines = [triggerPipelineReference]
)

triggerResource = TriggerResource(properties=scheduleTrigger) 

```
