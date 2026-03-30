# SecOps-NonUKAccess-Provisioning(Instant)

## Logic Overview
This workflow automates the addition of users to an Entra ID (Azure AD) group based on a SharePoint list trigger. It includes date validation to ensure users are only added during their active window.

## Prerequisites
* **SharePoint List:** Must contain columns `UserUPN` (Person), `FirstValidDate` (Date), and `LastValidDate` (Date).
* **Managed Identity:** The Logic App must have a **System-Assigned Managed Identity** enabled.

## Deployment Steps
1. Copy the contents of `Instant.json`.
2. In Azure, create a **Logic App (Consumption)**.
3. Go to **Logic App Designer** -> **Code View** and replace the JSON.
4. Update the following parameters in the `Initialize variables` actions:
   - `GroupID`: The Object ID of your target AD Group.
   - `SubscriptionID`: Your Azure Subscription ID.
   - `WorkspaceID`: Your Log Analytics Workspace ID.

## Required API Permissions
After enabling Managed Identity, run the script in `/_scripts/` to grant these Graph permissions:
* `GroupMember.ReadWrite.All`
