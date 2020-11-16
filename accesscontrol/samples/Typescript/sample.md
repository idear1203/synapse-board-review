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

## Scenario 1: List Caller's role assignments
```typescript
let listResult = await client.getCallerRoleAssignments();
```

## Scenario 2: List role definitions of synapse
```typescript
const list: string[] = [];
for await (const roleDefinition of client.listRoleDefinitions()) {
    list.push(roleDefinition.id!);
}
```

## Scenario 3: Create role assignments for specified user/service pricipal
```typescript
 let createResult = await client.createRoleAssignment(roleId, principalId);
```

## Scenario 4: List role assignments under specified role definition or user/service principal
```typescript
let listResult = await client.listRoleAssignments(roleId);
```

## Scenario 5: Delete specified role assignment using specified id
```typescript
client.deleteRoleAssignmentById(roleAssignmentId);
```

