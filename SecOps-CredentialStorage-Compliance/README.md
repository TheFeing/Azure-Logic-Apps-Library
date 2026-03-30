# SecOps-CredentialStorage-Compliance

## Logic Overview
This workflow automates the response to Microsoft Sentinel incidents involving insecure credential storage. It parses incident data, checks against a Sentinel Watchlist to prevent duplicate alerts, logs incident history into a SQL database, and sends a compliance notification to the user via the Microsoft Graph API.

## Prerequisites
* **Microsoft Sentinel**: Active workspace with the SecurityIncident trigger enabled.
* **Sentinel Watchlist**: A watchlist to track benign file URLs for suppressing Analytics Rule alerts.
* **SQL Database**: A table (e.g., `PasswordFiles`) must exist to store incident and contact history.
* **Managed Identity**: The Logic App must have a System-Assigned `Managed Identity` enabled for Graph API authentication.

## Deployment Steps
1. Copy the contents of the redacted JSON file.
2. In Azure, create a Logic App (Consumption).
3. Go to Logic App Designer -> Code View and replace the existing JSON.
4. Update the following parameters and placeholders within the JSON or via the Designer:
  - `Subscriptions/ResourceGroups/WorkspaceName`: Update to the environment's specific values.
  - `SQL Server/Database`: Provide the connection strings for the logging database.
  - `Email Sender`: Set the UPN of the account authorised to send notifications.

## Required API Permissions
After enabling Managed Identity, ensure the identity is granted the following Microsoft Graph permissions to allow the Logic App to send emails:
* `Mail.Send`
* `User.Read.All`
