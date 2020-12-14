# Synapse Accesscontrol champion scenarios

## Creating Synapse Accesscontrol client
```python
from azure.identity import ClientSecretCredential
from azure.synapse.accesscontrol import AccessControlClient

credential = ClientSecretCredential(
    tenant_id = "",
    client_id = "",
    client_secret = "")

workspace_endpoint = "https://<workspace_name>.dev.azuresynapse.net"
rbac_client = AccessControlClient(credential, workspace_endpoint)
```

## Scenario 1: Get role assignments by Id
```python
rbac_client.role_assignments.get_role_assignment_by_id("roleAssignmentId")
```

## Scenario 2: List role definitions of synapse
```python
rbac_client.role_assignments.list_role_assignments()
```

## Scenario 3: Create role assignments for specified user/service pricipal
```python
rbac_client.role_assignments.create_role_assignment(
    role_assignment_id = "<GUID>",
    role_id = "<GUID>",
    principal_id = "<GUID>",
    scope = "workspaces/<workspace_name>")
```

## Scenario 4: List role assignments under specified role definition or user/service principal
```python
rbac_client.role_assignments.list_role_assignments(role_id)
```

## Scenario 5: Delete specified role assignment using specified id
```python
rbac_client.role_assignments.delete_role_assignment_by_id(role_assignment_id)
```

## Scenario 6: Check principal accessiblity
```python
subjectInfo = SubjectInfo(
    principal_id = "<GUID>")

action = Action(
    id = "Microsoft.Synapse/workspaces/read",
    is_data_action = True)

actions = [action]

rbac_client.check_principal_access(
    subject = subjectInfo, 
    actions = actions,
    scope = "workspaces/<workspace_name>")
```

