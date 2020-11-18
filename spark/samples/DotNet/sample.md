# Synapse Spark champion scenarios

## Creating Synapse Spark client
```csharp
// Environment variable with the Synapse workspace endpoint.
string workspaceUrl = TestEnvironment.WorkspaceUrl;

// Environment variable with the Synapse Spark pool name.
string sparkPoolName = TestEnvironment.SparkPoolName;

// Create a new access Spark batch client using the default credential from Azure.Identity using environment variables previously set,
// including AZURE_CLIENT_ID, AZURE_CLIENT_SECRET, and AZURE_TENANT_ID.
SparkBatchClient batchClient = new SparkBatchClient(endpoint: new Uri(workspaceUrl), sparkPoolName: sparkPoolName, credential: new DefaultAzureCredential());

// Create a new access Spark session client using the default credential from Azure.Identity using environment variables previously set,
// including AZURE_CLIENT_ID, AZURE_CLIENT_SECRET, and AZURE_TENANT_ID.
SparkSessionClient sessionClient = new SparkSessionClient(endpoint: new Uri(workspaceUrl), sparkPoolName: sparkPoolName, credential: new DefaultAzureCredential());
```

## Scenario 1: `Spark Bacth Job` creation
```csharp
string name = $"batchSample";
string file = string.Format("abfss://{0}@{1}.dfs.core.windows.net/samples/java/wordcount/wordcount.jar", fileSystem, storageAccount);
SparkBatchJobOptions options = new SparkBatchJobOptions(name: name, file: file)
{
    ClassName = "WordCount",
    Arguments =
    {
        string.Format("abfss://{0}@{1}.dfs.core.windows.net/samples/java/wordcount/shakespeare.txt", fileSystem, storageAccount),
        string.Format("abfss://{0}@{1}.dfs.core.windows.net/samples/java/wordcount/result/", fileSystem, storageAccount),
    },
    DriverMemory = "28g",
    DriverCores = 4,
    ExecutorMemory = "28g",
    ExecutorCores = 4,
    ExecutorCount = 2
};

SparkBatchJob jobCreated = batchClient.CreateSparkBatchJob(options);
```

## Scenario 2: `Spark Bacth Job` get/list/cancel

### Get
```csharp
SparkBatchJob actualSparkJob = SparkBatchClient.GetSparkBatchJob(expectedSparkJob.Id);
```

### List
```csharp
Response<SparkBatchJobCollection> jobs = batchClient.GetSparkBatchJobs();
foreach (SparkBatchJob job in jobs.Value.Sessions)
{
    Console.WriteLine(job.Name);
}
```

### Cancel
```csharp
Response operation = batchClient.CancelSparkBatchJob(jobId);
```

## Scenario 3: `Spark Session` creation
```csharp
string name = test.Recording.GenerateName("dotnetsession");
SparkSessionOptions createParams = new SparkSessionOptions(name)
{
    DriverMemory = "28g",
    DriverCores = 4,
    ExecutorMemory = "28g",
    ExecutorCores = 4,
    ExecutorCount = 2
};

SparkSession sessionCreateResponse = (await SparkSessionClient.CreateSparkSessionAsync(createParams)).Value;
```

## Scenario 4: `Spark Session` get/list/cancel

### Get
```csharp
SparkSessionCollection sparkSessions = (await SparkSessionClient.GetSparkSessionsAsync()).Value;
```

### List
```csharp
Response<SparkStatementCollection> listStatementResponse = await SparkSessionClient.GetSparkStatementsAsync(sessionCreateResponse.Id);
```

### Cancel
```csharp
await SparkSessionClient.CancelSparkSessionAsync(sessionCreateResponse.Id);
```


## Scenario 5: `Spark Statement` creation
```csharp
SparkStatement createStatementResponse = (await SparkSessionClient.CreateSparkStatementAsync(
    getSessionResponse.Id,
    new SparkStatementOptions
    {
        Kind = SparkStatementLanguageType.Spark,
        Code = @"print(""Hello world\n"")"
    })).Value;
```

## Scenario 6: `Spark Statement` get/list/cancel

### Get
```csharp
SparkSession actualSparkSession = await SparkSessionClient.GetSparkSessionAsync(expectedSparkSession.Id);
```

### List
```csharp
SparkSessionCollection sparkSessions = (await SparkSessionClient.GetSparkSessionsAsync()).Value;
```

### Cancel
```csharp
await SparkSessionClient.CancelSparkStatementAsync(sessionCreateResponse.Id, createStatementResponse.Id);
```