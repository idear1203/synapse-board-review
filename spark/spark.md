## The Basics

* Service team responsible for the client library: **Synapse Analytics**
* Link to documentation describing the service: https://docs.microsoft.com/en-us/azure/synapse-analytics/overview-what-is
* Contact email (if service team, provide PM and Dev Lead):
    - PM contact email: Matthew Hicks (Matthew.Hicks@microsoft.com)
    - Dev Lead contact email: DJ Lan (djlan@microsoft.com)
    - Dev contact：Dongwei Wang(dongwwa@microsoft.com), Shangwei Sun(shangsu@microsoft.com)

## About this client library

* Name of the client library: **Synapse-Spark**
* Languages for this review: **C#/Python/Java/TS**
* Link to the service REST APIs: https://github.com/Azure/azure-rest-api-specs/blob/master/specification/synapse/data-plane/Microsoft.Synapse/preview/2019-11-01-preview/sparkJob.json

## Artifacts required (per language)

We use an API review tool ([apiview](https://apiview.azurewebsites.net)) to support .NET and Java API reviews.  For Python and TypeScript, use the API extractor tool, then submit the output as a Draft PR to the relevant repository (azure-sdk-for-python or azure-sdk-for-js).

### .NET

* Upload DLL to [apiview](https://apiview.azurewebsites.net).  Link: https://apiview.dev/Assemblies/Review/780fa825c2d54a669c17051c32c3192c <!--TODO: idear1203: update DLL-->
* Link to samples for champion scenarios:

### Java

* Upload JAR to [apiview](https://apiview.azurewebsites.net).  Link: https://apiview.dev/Assemblies/Review/e9a7a8b7554e499c9800574a43bad5f3 <!--TODO: idear1203: update DLL-->
* Link to samples for champion scenarios:

### Python

* Upload the api as a Draft PR.  Link: https://apiview.dev/Assemblies/Review/c8636b5e4eec433781ccdc48f987b122 <!--TODO: idear1203: update DLL-->
* Link to samples for champion scenarios:

### TypeScript

* Upload output of api-extractor as a Draft PR.  Link to PR: https://github.com/Azure/azure-sdk-for-js/pull/12487
* Upload output of api-extractor to [apiview](https://apiview.azurewebsites.net). Link: https://apiview.dev/Assemblies/Review/506992a723d342039c63e2bf1550ae84
* Link to samples for champion scenarios:

## Champion Scenarios


* **Champion Scenario 1:  Create/Submit a spark batch job.** Developer wants to run a Spark job Once the job is complete, they need to see the results
  * Customer wants to submit a spark batch job to the spark pool of azure synapse workspace to do some analytics work by using apache spark.
  * Customer who want to run spark batch job must use this api, so more than 80% of developers using the service who would use the champion scenario
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-1-spark-bacth-job-creation) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-1-spark-bacth-job-creation) | [TS](./samples/Typescript/sample.md#scenario-1-spark-bacth-job-creation)

* **Champion Scenario 2**: Developer/Administrator needs to maintain the pool of workers; for this they need to be able to list the jobs in queue, including finding which one is currently running and potentially cancel or delete them from the list. 
* Champion Scenario 2.1: Get a spark batch job
  * Customer wants to get the information of a submitted spark batch job. For example, customer wants to know whether the job has been ran successfully, where the log is etc.
  * Customer who will submit job to spark pool must use this api to check whether the job's state and other information. So more than 80% of developers using the service who would use the champion scenario
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-2-spark-bacth-job-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-2-spark-bacth-job-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-2-spark-bacth-job-get-list-cancel)

* Champion Scenario 2.2: List all spark batch jobs under the specific spark pool
  * Customer wants to list all submitted spark batch jobs under a specific spark pool of azure synapse
  * Customer wants to manage the submitted spark batch jobs will use this api, so more than 30% of developers using the service who would use the champion scenario
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-2-spark-bacth-job-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-2-spark-bacth-job-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-2-spark-bacth-job-get-list-cancel)
* Champion Scenario 2.3:  Cancel a spark batch job
  * Customer wants to cancel a submitted spark batch job. For example, customer may want to cancel a job when there is a logic error in the program or the job is in a unexpected state for a long time.
  * Customer will this api when they find that there is a logic error or the job is not needed will use api, so more than 40% of developers using the service who would use the champion scenario
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-2-spark-bacth-job-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-2-spark-bacth-job-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-2-spark-bacth-job-get-list-cancel)

* **Champion Scenario 3:  Create a spark session.** Developer wants to run a Spark session for interective analytics.
  * Customer wants to create a spark session to the spark pool of azure synapse workspace to do some analytics work by using apache spark.
  * Customer who want to create spark session must use this api, so more than 80% of developers using the service who would use the champion scenario
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-3-spark-session-creation) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-3-spark-session-creation) | [TS](./samples/Typescript/sample.md#scenario-3-spark-session-creation)

* **Champion Scenario 4**: Developer/Administrator needs to maintain the pool of workers; for this they need to be able to list the jobs in queue, including finding which one is currently running and potentially cancel or delete them from the list. 
* Champion Scenario 4.1: Get a spark session
  * Customer wants to get the information of a submitted spark session. For example, customer wants to know whether the state of specified session.
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-4-spark-session-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-4-spark-session-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-4-spark-session-get-list-cancel)

* Champion Scenario 4.2: List all spark sessions under the specific spark pool
  * Customer wants to list all submitted spark sessions under a specific spark pool of azure synapse
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-4-spark-session-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-4-spark-session-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-4-spark-session-get-list-cancel)
* Champion Scenario 4.3:  Cancel a spark session
  * Customer wants to cancel a submitted session. For example, customer may want to cancel a session when there is a logic error in the program or the session is in a unexpected state for a long time.
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-4-spark-session-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-4-spark-session-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-4-spark-session-get-list-cancel)

* **Champion Scenario 5:  Create a spark statement**. Developer wants to run a Spark statement based on spcefied session for interective analytics.
  * Customer wants to create a spark statement based on spcefied session to the spark pool of azure synapse workspace to do some analytics work by using apache spark.
  * Customer who want to create spark statement based on spcefied session must use this api, so more than 80% of developers using the service who would use the champion scenario
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-5-spark-statement-creation) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-5-spark-statement-creation) | [TS](./samples/Typescript/sample.md#scenario-5-spark-statement-creation)

* **Champion Scenario 6**: Developer/Administrator needs to maintain the pool of workers; for this they need to be able to list the jobs in queue, including finding which one is currently running and potentially cancel or delete them from the list. 
* Champion Scenario 6.1: Get a spark statement from session
  * Customer wants to get the information of a submitted spark statement. For example, customer wants to know whether the result of specified statement.
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-6-spark-statement-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-6-spark-statement-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-6-spark-statement-get-list-cancel)

* Champion Scenario 6.2: List all spark statements under the specific session
  * Customer wants to list all submitted spark statements under a specific session.
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-6-spark-statement-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-6-spark-statement-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-6-spark-statement-get-list-cancel)
* Champion Scenario 6.3:  Cancel a spark statement
  * Customer wants to cancel a submitted statement. For example, customer may want to cancel a statement when there is a logic error in the program or the statement is in a unexpected state for a long time.
  * Link to the code sample: [C#](./samples/DotNet/sample.md#scenario-6-spark-statement-get-list-cancel) | [Python]() | [JAVA](./samples/Java/sample.md#scenario-6-spark-statement-get-list-cancel) | [TS](./samples/Typescript/sample.md#scenario-6-spark-statement-get-list-cancel)
        