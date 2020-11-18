# Synapse Spark champion scenarios

## Creating Synapse Spark client
```java
// Instantiate a Spark Batch client that will be used to call the service. Notice that the client is using default Azure
// credentials. To make default credentials work, ensure that environment variables 'AZURE_CLIENT_ID',
// 'AZURE_CLIENT_KEY' and 'AZURE_TENANT_ID' are set with the service principal credentials.
SparkBatchClient batchClient = new SparkClientBuilder()
    .endpoint("https://{YOUR_WORKSPACE_NAME}.dev.azuresynapse.net")
    .credential(new DefaultAzureCredentialBuilder().build())
    .buildSparkBatchClient();

// Instantiate a Spark Session client that will be used to call the service. Notice that the client is using default Azure
// credentials. To make default credentials work, ensure that environment variables 'AZURE_CLIENT_ID',
// 'AZURE_CLIENT_KEY' and 'AZURE_TENANT_ID' are set with the service principal credentials.
SparkSessionClient sessionClient = new SparkClientBuilder()
    .endpoint("https://{YOUR_WORKSPACE_NAME}.dev.azuresynapse.net")
    .credential(new DefaultAzureCredentialBuilder().build())
    .buildSparkSessionClient();
```

## Scenario 1: `Spark Bacth Job` creation
```java
String storageAccount = "<storage-account>";
String fileSystem = "<file-system>";
String name = "<job-name>";
String file = String.format("abfss://%s@%s.dfs.core.windows.net/samples/java/wordcount/wordcount.jar", fileSystem, storageAccount);
SparkBatchJobOptions options = new SparkBatchJobOptions()
    .setName(name)
    .setFile(file)
    .setClassName("WordCount")
    .setArguments(Arrays.asList(
        String.format("abfss://%s@%s.dfs.core.windows.net/samples/java/wordcount/shakespeare.txt", fileSystem, storageAccount),
        String.format("abfss://%s@%s.dfs.core.windows.net/samples/java/wordcount/result/", fileSystem, storageAccount)
    ))
    .setDriverMemory("28g")
    .setDriverCores(4)
    .setExecutorMemory("28g")
    .setExecutorCores(4)
    .setExecutorCount(2);

SparkBatchJob jobCreated = batchClient.createSparkBatchJob(options);
```

## Scenario 2: `Spark Bacth Job` get/list/cancel

### Get
```java
SparkBatchJob actualSparkJob = client.getSparkBatchJob(expectedSparkJob.getId());
```

### List
```java
// List Spark batch jobs
SparkBatchJobCollection jobs = batchClient.getSparkBatchJobs();
for (SparkBatchJob job : jobs.getSessions()) {
    System.out.println(job.getName());
}
```

### Cancel
```java
batchClient.cancelSparkBatchJob(jobId);
```

## Scenario 3: `Spark Session` creation
```java
SparkSessionOptions sessionOptions = new SparkSessionOptions()
    .setName("session-example")
    .setDriverMemory("28g")
    .setDriverCores(4)
    .setExecutorCores(4)
    .setExecutorCount(2);

SparkSession sessionCreated = sessionClient.createSparkSession(sessionOptions);
```

## Scenario 4: `Spark Session` get/list/cancel

### Get
```java
SparkSession session = sessionClient.getSparkSession(sessionCreated.getId());
System.out.printf("Session is returned with name %s and state %s\n", session.getName(), session.getState());
```

### List
```java
SparkSessionCollection sessions = sessionClient.getSparkSessions();
for (SparkSession sparkSession : sessions.getSessions()) {
    System.out.printf("Session id: %s\n", sparkSession.getId());
}
```

### Cancel
```java
sessionClient.cancelSparkSession(sessionCreated.getId());
```


## Scenario 5: `Spark Statement` creation
```java
SparkStatementOptions sparkStatementRequest = new SparkStatementOptions()
    .setKind(SparkStatementLanguageType.SPARK)
    .setCode("print(\"\"Hello world\\n\"\")");
SparkStatement statementCreated = sessionClient.createSparkStatement(sessionCreated.getId(), sparkStatementRequest);
```

## Scenario 6: `Spark Statement` get/list/cancel

### Get
```java
SparkStatement statement = sessionClient.getSparkStatement(sessionCreated.getId(), statementCreated.getId());
System.out.printf("Statement is returned with id %s and state %s", statement.getId(),  statement.getState());
```

### List
```java
SparkStatementCollection statements = sessionClient.getSparkStatements(sessionCreated.getId());
for (SparkStatement sessionStatement : statements.getStatements()) {
    System.out.println(sessionStatement.getId());
}
```

### Cancel
```java
SparkStatementCancellationResult cancellationResult = sessionClient.cancelSparkStatement(sessionCreated.getId(), statementCreated.getId());
System.out.printf("Statement is cancelled with message %s", cancellationResult.getMsg());
```