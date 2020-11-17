## The Basics

* Service team responsible for the client library: **Synapse Analytics**
* Link to documentation describing the service: https://docs.microsoft.com/en-us/azure/synapse-analytics/overview-what-is
* Contact email (if service team, provide PM and Dev Lead):
    - PM contact email: Matthew Hicks (Matthew.Hicks@microsoft.com)
    - Dev Lead contact email: DJ Lan (djlan@microsoft.com)
    - Dev contact：Dongwei Wang(dongwwa@microsoft.com), Shangwei Sun(shangsu@microsoft.com)

## About this client library

* Name of the client library: **Synapse-Artifacts**
* Languages for this review: **Java/TS**
* Link to the service REST APIs: https://github.com/Azure/azure-rest-api-specs/tree/master/specification/synapse/data-plane/Microsoft.Synapse/preview/2019-06-01-preview

## Artifacts required (per language)

We use an API review tool ([apiview](https://apiview.azurewebsites.net)) to support .NET and Java API reviews.  For Python and TypeScript, use the API extractor tool, then submit the output as a Draft PR to the relevant repository (azure-sdk-for-python or azure-sdk-for-js).

### .NET

* Upload DLL to [apiview](https://apiview.azurewebsites.net).  Link:
* Link to samples for champion scenarios:

### Java

* Upload JAR to [apiview](https://apiview.azurewebsites.net).  Link:
* Link to samples for champion scenarios:

### Python

* Upload the api as a Draft PR.  Link to PR:
* Link to samples for champion scenarios:

### TypeScript

* Upload output of api-extractor as a Draft PR.  Link to PR: https://github.com/Azure/azure-sdk-for-js/pull/12485
* Upload output of api-extractor to [apiview](https://apiview.azurewebsites.net). Link: https://apiview.dev/Assemblies/Review/9c9903a56f5f46e59eaa995d5b09342b
* Link to samples for champion scenarios:

## Champion Scenarios


* **Champion Scenario 1:  Get bigdata pool/sql pool/intergartion runtimes information under current workspace.** 
  * User who only have read permission can get basic resource information under current workspace. These requests are belong to data plane instead of management plane, that means these needn't routed by ARM. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 2:  Manage notebook resource.** 
  * Developer manage notebook resource under current workspace. For example, create a new notebook using customized parameter and retrieve/delete exsiting notebook. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 3:  Manage dateflow resource.** 
  * Developer manage dateflow resource under current workspace. For example, create a new dateflow using customized parameter and retrieve/delete exsiting dateflow. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 4:  Manage dateset resource.** 
  * Developer manage dateset resource under current workspace. For example, create a new dateset using customized parameter and retrieve/delete exsiting dateset. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)


* **Champion Scenario 5:  Manage pipeline resource.** 
  * Developer manage pipeline resource under current workspace. For example, create a new pipeline using customized parameter and retrieve/delete exsiting pipeline. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 6:  Manage sqlscript resource.** 
  * Developer manage sqlscript resource under current workspace. For example, create a new sqlscript using customized parameter and retrieve/delete exsiting sqlscript. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 7:  Manage linkedservice resource.** 
  * Developer manage linkedservice resource under current workspace. For example, create a new linkedservice using customized parameter and retrieve/delete exsiting linkedservice. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 8:  Manage sparkjobdefinition resource.** 
  * Developer manage sparkjobdefinition under current workspace. For example, create a new sparkjobdefinition using customized parameter and retrieve/delete exsiting sparkjobdefinition. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 9:  Manage trigger resource.** 
  * Developer manage trigger resource under current workspace. For example, create a new trigger using customized parameter and retrieve/delete exsiting trigger. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

        