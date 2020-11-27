# Synapse Accesscontrol champion scenarios

## Creating Synapse Accesscontrol client
```csharp
RoleAssignmentsClient roleAssignmentsClient = new RoleAssignmentsClient(new Uri(workspaceUrl), new DefaultAzureCredential());
RoleDefinitionsClient roleDefinitionsClient = new RoleDefinitionsClient(new Uri(workspaceUrl), new DefaultAzureCredential());
```

## Scenario 1: Get role assignments by Id
```csharp
RoleAssignmentDetails roleAssignment = roleAssignmentsClient.GetRoleAssignmentById(roleAssignmentId);
```

## Scenario 2: List role definitions of synapse
```csharp
IReadOnlyList<SynapseRoleDefinition> roleDefinitions = roleDefinitionsClient.ListRoleDefinitions().Value;
foreach (SynapseRoleDefinition roleDefinition in roleDefinitions)
{
    Console.WriteLine(roleDefinition.Id);
}
```

## Scenario 3: Create role assignments for specified user/service pricipal
```csharp
string workspaceName = TestEnvironment.WorkspaceName;
Guid principalId = new Guid(TestEnvironment.PrincipalId);
Guid sqlAdminRoleId = roleDefinitionsClient.ListRoleDefinitions().Value.AsEnumerable().Single(role => role.Name == "Sql Admin").Id.Value;
string roleAssignmentId = Guid.NewGuid().ToString();
string scope = $"workspaces/{workspaceName}";

RoleAssignmentDetails roleAssignment = roleAssignmentsClient.CreateRoleAssignment(roleAssignmentId, sqlAdminRoleId, principalId, scope);
```

## Scenario 4: List role assignments under specified role definition or user/service principal
```csharp
IReadOnlyList<RoleAssignmentDetails> roleAssignments = roleAssignmentsClient.ListRoleAssignments().Value.Value;
foreach (RoleAssignmentDetails assignment in roleAssignments)
{
    Console.WriteLine(assignment.Id);
}
```

## Scenario 5: Delete specified role assignment using specified id
```csharp
roleAssignmentsClient.DeleteRoleAssignmentById(roleAssignment.Id);
```

## Scenario 6: Check principal accessibility
```csharp
string workspaceName = TestEnvironment.WorkspaceName;
string scope = $"workspaces/{workspaceName}";
Guid principalId = new Guid(TestEnvironment.PrincipalId);
CheckPrincipalAccessResponse result = roleAssignmentsClient.CheckPrincipalAccess(
    new SubjectInfo(principalId),
    new List<RequiredAction>()
    {
        new RequiredAction
        (
            id: "Microsoft.Synapse/workspaces/read",
            isDataAction: true
        )
    },
    scope);

foreach (CheckAccessDecision accessDecision in result.AccessDecisions)
{
    Console.WriteLine(accessDecision.AccessDecision);
}
```

