# SecOps-NonUKAccess-Provisioning(Scheduled)

## Logic Overview
This workflow runs on a daily schedule (00:01 UTC) to manage temporary access for users working outside of the UK. It synchronises an Entra ID (Azure AD) group with a SharePoint master list to ensure access is granted and revoked on the correct dates.
* **Removal Phase**: Identifies users whose `LastValidDate` was yesterday and removes them from the Entra ID Group.
* **Provisioning Phase**: Identifies users whose `FirstValidDate` is today and adds them to the Entra ID Group.
* **Logging & Intelligence**: Queries Log Analytics for the user's managed devices and updates a Microsoft Sentinel Watchlist to suppress false-positive alerts triggered by non-UK travel.
* **Error Handling**: Includes a condition to notify a specific Microsoft Teams channel if the workflow encounters critical failures.

## Prerequisites
* **SharePoint List**: Must contain `UserUPN` (Person), `FirstValidDate` (Date), and `LastValidDate` (Date).
* **Managed Identity**: The Logic App must have a System-Assigned Managed Identity enabled.
* **Log Analytics Workspace**: Access to `SigninLogs` for device identification.

## Deployment Steps
1. Copy the contents of the JSON definition provided below.
2. In Azure, create a Logic App (Consumption).
3. Navigate to Logic App Designer -> Code View and paste the JSON.
4. Update the following variables in the Initialize variables action:
- `GroupID`: The Object ID of the target Entra ID Group.
- `SubscriptionID`: Your Azure Subscription ID.
- `WorkspaceID`: The Name/ID of your Log Analytics Workspace.
- `ResourceGroup`: The Resource Group where the workspace resides.
5. In the SharePoint actions, update the Site Address and List ID to match your environment.

## Required API Permissions
The System-Assigned Managed Identity requires the following Microsoft Graph permissions (assigned via PowerShell):
- `GroupMember.ReadWrite.All`
- `User.Read.All`
- `Chat.ReadWrite` (if using the Teams notification feature)
