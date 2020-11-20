# Synapse Accesscontrol champion scenarios

## Creating Synapse Accesscontrol client
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

const client = new AccessControlClient("<workspace_endpoint>", defaultAzureCredential);
```

## Scenario 1: Get role assignments by Id
```typescript
let getResult = await client.getRoleAssignmentById(roleAssignmentId);
```

## Scenario 2: List role definitions of synapse
```typescript
let listResult = await client.listRoleDefinitions();
```

## Scenario 3: Create role assignments for specified user/service pricipal
```typescript
roleAssignmentId = Guid.create().toString();
let createResult = await client.createRoleAssignment(
    roleAssignmentId,
    roleId,
    principalId,
    getScope()
);
```

## Scenario 4: List role assignments under specified role definition or user/service principal
```typescript
let listResult = await client.listRoleAssignments({ roleId });
```

## Scenario 5: Delete specified role assignment using specified id
```typescript
await client.deleteRoleAssignmentById(roleAssignmentId, { scope: getScope() });
```

## Scenario 6: Check principal accessiblity
```typescript
let listResult = await client.checkPrincipalAccess(
    {
    principalId: principalId
    },
    [
    {
        id: "Microsoft.Synapse/workspaces/read",
        isDataAction: true
    }
    ],
    getScope()
);
```

