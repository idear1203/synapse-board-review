# Synapse Spark champion scenarios

## Creating Synapse Spark client
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

const client = new SparkClient("<workspace_endpoint>", "spark_pool_name", defaultAzureCredential);
```

## Scenario 1: `Spark Bacth Job` creation
```typescript
let file:string = "abfss://${fileSystem}@${storageAccount}.dfs.core.windows.net/samples/java/wordcount/wordcount.jar";

let sparkBatchJob: SparkBatchJobOptions = {
    name: "SampleBatchJob",
    file: file,
    className: "WordCount",
    arguments: [
        "abfss://${fileSystem}@${storageAccount}.dfs.core.windows.net/samples/java/wordcount/shakespeare.txt",
        "abfss://${fileSystem}@${storageAccount}.dfs.core.windows.net/samples/java/wordcount/result/",
    ],
    driverMemory : "28g",
    driverCores : 4,
    executorMemory : "28g",
    executorCores : 4,
    executorCount : 2
};

let options: CreateSparkBatchJobOptions = {
    detailed: true
};

let createResult = await client.createSparkBatchJob(sparkBatchJob, options);
```

## Scenario 2: `Spark Bacth Job` get/list/cancel

### Get
```typescript
let options: GetSparkBatchOptions = {
    detailed: true
};
let getResult = await client.getSparkBatch(batchId, options);
```

### List
```typescript
let options: ListSparkBatchJobsOptions = {
    fromParam: batchId,
    size: size,
    detailed: true
};
let listResult = await client.listSparkBatchJobs(options);
```

### Cancel
```typescript
client.cancelSparkBatchJob(options);
```

## Scenario 3: `Spark Session` creation
```typescript
let sparkSession: SparkSessionOptions = {
    name: sessionName,
    executorCount: 2,
    driverCores: 4,
    driverMemory: "8g",
    executorCores: 4,
    executorMemory: "8g"
};
let options: CreateSparkSessionOptions = {
    detailed: true
};

let createResult = await client.createSparkSession(sparkSession, options);
```

## Scenario 4: `Spark Session` get/list/cancel

### Get
```typescript
let options: GetSparkSessionOptions = {
    detailed: true
};
let getResult = await client.getSparkSession(sessionId, options);
```

### List
```typescript
let options: ListSparkSessionsOptions = {
    fromParam: sessionId,
    size: size,
    detailed: true
};
let listResult = await client.listSparkSessions(options);
```

### Cancel
```typescript
client.cancelSparkSession(options);
```


## Scenario 5: `Spark Statement` creation
```typescript
let sparkStatement: sparkStatementOptions = {
    code: "<customer running code>",
    kind: "spark"
};

let createResult = await client.createSparkStatement(sessionId, options);
```

## Scenario 6: `Spark Statement` get/list/cancel

### Get
```typescript
let getResult = await client.getSparkStatement(sessionId, statementId);
```

### List
```typescript
let listResult = await client.listSparkStatements(sessionId);
```

### Cancel
```typescript
client.cancelSparkSession(options);
```