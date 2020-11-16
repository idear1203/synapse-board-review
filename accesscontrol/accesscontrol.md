## The Basics

* Service team responsible for the client library: **Synapse Analytics**
* Link to documentation describing the service: https://docs.microsoft.com/en-us/azure/synapse-analytics/overview-what-is
* Contact email (if service team, provide PM and Dev Lead):
    - PM contact email: Matthew Hicks (Matthew.Hicks@microsoft.com)
    - Dev Lead contact email: DJ Lan (djlan@microsoft.com)
    - Dev contact：Dongwei Wang(dongwwa@microsoft.com), Shangwei Sun(shangsu@microsoft.com)

## About this client library

* Name of the client library: **Synapse-Accesscontrol**
* Languages for this review: **Java/TS**
* Link to the service REST APIs: https://github.com/Azure/azure-rest-api-specs/blob/master/specification/synapse/data-plane/Microsoft.Synapse/preview/2020-02-01-preview/roleAssignments.json
https://github.com/Azure/azure-rest-api-specs/blob/master/specification/synapse/data-plane/Microsoft.Synapse/preview/2020-02-01-preview/roles.json

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

* Upload output of api-extractor as a Draft PR.  Link to PR: https://github.com/Azure/azure-sdk-for-js/pull/12487
* Upload output of api-extractor to [apiview](https://apiview.azurewebsites.net). Link: https://apiview.dev/Assemblies/Review/506992a723d342039c63e2bf1550ae84
* Link to samples for champion scenarios:

## Champion Scenarios


* **Champion Scenario 1:  List Caller's role assignments.** 
  * User wants to get all role assignments they are assigned.
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 2: List role definitions of synapse.**
  * User wants to get all role definitions. These definitions are provided by Synapse, user can't modify it.
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 3: Create role assignments for specified user/service pricipal.**
  * Workspace Admin wants to set pecified user/service pricipal as a specified role. For example, administrator can set developerA as SQL Admin using this function. 
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 4: List role assignments under specified role definition or user/service principal.**
  * Workspace Admin wants to list all role assignments information under specified role definition or user/service principal or all under current workspace. For example, administrator can list all roles of developerA.
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)

* **Champion Scenario 5: Delete specified role assignment using specified id.**
  * Workspace Admin wants to delete a role assignment from using specified id. For example, administrator delete developerA's SQL Admin role using the spcefied id--developerA' SQL Admin role assignment id.
  * Link to the code sample: [JAVA]() | [TS](./samples/Typescript/sample.md#)  


        