# Synapse Artifacts champion scenarios



## Scenario 1: Get bigdata pool/sql pool/intergartion runtimes information under current workspace.

### Creating client
```typescript
// Azure AD Credential information is required to run this sample:
if (
!process.env.AZURE_TENANT_ID ||
!process.env.AZURE_CLIENT_ID ||
!process.env.AZURE_CLIENT_SECRET
) {
console.warn(
    "Azure AD authentication information not provided, but it is required to run this sample. Exiting."
);
return;
}

const defaultAzureCredential = new DefaultAzureCredential();

const client = new ArtifactsClient("<workspace_endpoint>", defaultAzureCredential);

```

### Get bigdata pool
```typescript
let getResult = await client.getBigDataPool("<bigdata_pool_name>");
```


## Scenario 2: Manage notebook resource.

### Creating client
```typescript
// Azure AD Credential information is required to run this sample:
if (
!process.env.AZURE_TENANT_ID ||
!process.env.AZURE_CLIENT_ID ||
!process.env.AZURE_CLIENT_SECRET
) {
console.warn(
    "Azure AD authentication information not provided, but it is required to run this sample. Exiting."
);
return;
}

const defaultAzureCredential = new DefaultAzureCredential();

const notebookClient = new NotebookClient("<workspace_endpoint>", defaultAzureCredential);
```

### Get
```typescript
let getResult = await notebookClient.get("<notebook_name>");
```

### List
```typescript
let listResult = await notebookClient.list();
```

### Create
```typescript
let notebook: NotebookResource = {
    name: "<notebook_name>",
    properties: {
    nbformat: 4,
    nbformatMinor: 2,
    metadata: {
        languageInfo:{
            name:"Python"
        }
    },
    cells : []
    }
};
let getResult = await notebookClient.beginUpsert("<notebook_name>", notebook);
const response = await getResult.pollUntilDone();
```

### Delete
```typescript
await notebookClient.beginDelete("<notebook_name>");
```

## Scenario 3:  Manage dateflow resource.

### Creating client
```typescript
// Azure AD Credential information is required to run this sample:
if (
!process.env.AZURE_TENANT_ID ||
!process.env.AZURE_CLIENT_ID ||
!process.env.AZURE_CLIENT_SECRET
) {
console.warn(
    "Azure AD authentication information not provided, but it is required to run this sample. Exiting."
);
return;
}

const defaultAzureCredential = new DefaultAzureCredential();

const dataflowClient = new DataflowClient("<workspace_endpoint>", defaultAzureCredential);
```


### Get
```typescript
let getResult = await dataflowClient.get("<dataflow_name>");
```

### List
```typescript
let listResult = await dataflowClient.list();
```

### Create
```typescript
let dataflow: DataFlowResource = {
    properties: {
    type: "MappingDataFlow"
    }
};
let getResult = await dataflowClient.beginUpsert("<dataflow_name>", dataflow);
const response = await getResult.pollUntilDone();
```

### Delete
```typescript
let deleteResult = await dataflowClient.beginDelete("testdataset");
await deleteResult.pollUntilDone();
```

## Scenario 4:  Manage dateset resource.

### Creating client
```typescript
// Azure AD Credential information is required to run this sample:
if (
!process.env.AZURE_TENANT_ID ||
!process.env.AZURE_CLIENT_ID ||
!process.env.AZURE_CLIENT_SECRET
) {
console.warn(
    "Azure AD authentication information not provided, but it is required to run this sample. Exiting."
);
return;
}

const defaultAzureCredential = new DefaultAzureCredential();

const datasetClient = new DatasetClient("<workspace_endpoint>", defaultAzureCredential);
```

### Get
```typescript
let getResult = await datasetClient.get("<dataset_name>");
```

### List
```typescript
let listResult = await datasetClient.list();
```

### Create
```typescript
let azureTable: AzureTableDataset = {
    type:"AzureTable",
    tableName:"testTable",
    linkedServiceName:{
        type: "LinkedServiceReference",
        referenceName:"testLinkedService",
    } 
};
let dataset: DatasetResource = {
    properties:azureTable
}
let getResult = await datasetClient.beginUpsert("testdataset", dataset);
const response = await getResult.pollUntilDone();
```

### Delete
```typescript
let deleteResult = await datasetClient.beginDelete("testdataset");
await deleteResult.pollUntilDone();
```

## Scenario 5:  Manage pipeline resource.

### Creating client
```typescript
// Azure AD Credential information is required to run this sample:
if (
!process.env.AZURE_TENANT_ID ||
!process.env.AZURE_CLIENT_ID ||
!process.env.AZURE_CLIENT_SECRET
) {
console.warn(
    "Azure AD authentication information not provided, but it is required to run this sample. Exiting."
);
return;
}

const defaultAzureCredential = new DefaultAzureCredential();

const pipelineClient = new PipelineClient("<workspace_endpoint>", defaultAzureCredential);
```

### Get
```typescript
let getResult = await pipelineClient.get("<testpipeline>");
```

### List
```typescript
let listResult = await pipelineClient.list();
```

### Create
```typescript
let pipeline: PipelineResource = {};
let getResult = await pipelineClient.beginUpsert("testpipeline", pipeline);
const response = await getResult.pollUntilDone();
```

### Delete
```typescript
let deleteResult = await pipelineClient.beginDelete("testpipeline");
await deleteResult.pollUntilDone();
```

## Scenario 6:  Manage sqlscript resource.


## Scenario 7:  Manage linkedservice resource.


## Scenario 8:  Manage sparkjobdefinition resource.


## Scenario 9:  Manage trigger resource.

### Creating client
```typescript
// Azure AD Credential information is required to run this sample:
if (
!process.env.AZURE_TENANT_ID ||
!process.env.AZURE_CLIENT_ID ||
!process.env.AZURE_CLIENT_SECRET
) {
console.warn(
    "Azure AD authentication information not provided, but it is required to run this sample. Exiting."
);
return;
}

const defaultAzureCredential = new DefaultAzureCredential();

const trigerClient = new TrigerClient("<workspace_endpoint>", defaultAzureCredential);
```

### Get
```typescript
let getResult = await trigerClient.get("testtriger");
let trigger = getResult.properties as ScheduleTrigger;
```

### Create
```typescript
let scheduleTrigger: ScheduleTrigger = {
    type: "ScheduleTrigger",
    recurrence: {
    frequency: "Minute",
    interval: 4,
    startTime: new Date("2018-06-16T00:39:13.8441801Z"),
    endTime: new Date("2018-06-16T00:55:13.8441801Z"),
    timeZone: "UTC"
    },
    pipelines: [
    {
        pipelineReference: {
        referenceName: "testPipeline",
        type: "PipelineReference"
        }
    }
    ]
};
let trigger: TriggerResource = {
    properties: scheduleTrigger
};

let getResult = await trigerClient.beginUpsert("testtriger", trigger);
const response = await getResult.pollUntilDone();
```
