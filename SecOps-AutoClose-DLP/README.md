# SecOps-AutoClose-DLP

## Logic Overview
This workflow automates the triage and closure of Microsoft Sentinel incidents related to Data Loss Prevention (DLP) or unauthorised external emails. It determines if an incident can be safely "AutoClosed" based on whether the suspicious emails were successfully blocked by security controls.

* **Incident Parsing:** Extracts related entities from the Microsoft Sentinel incident, specifically filtering for `MailMessage` objects.
* **Log Verification:** Queries Azure Monitor (Log Analytics) `EmailEvents` to check the `DeliveryAction` and `DeliveryLocation` of the specific `NetworkMessageId`.
* **Automated Decisioning:**
    * **AutoClose:** If all unauthorised external emails were "Blocked" or "Dropped," the incident is closed as **BenignPositive** with the reason "SuspiciousButExpected".
    * **Manual Review:** If any email was successfully delivered to an external recipient, the incident remains "New," the "AutoClose" tag is removed, and a notification is sent to the SOC Teams channel.
* **Notification:** Alerts are sent to Microsoft Teams for both successful closures and workflow failures to ensure visibility.

## Prerequisites
* **Microsoft Sentinel:** Incident trigger configured to call this Logic App.
* **Microsoft Defender for Office 365:** Required for `EmailEvents` logs in the Log Analytics workspace.
* **Managed Identity:** The Logic App must have a **System-Assigned Managed Identity** enabled for Graph and Sentinel API authentication.

## Deployment Steps
1. Copy the contents of the JSON workflow definition.
2. In the Azure Portal, create a new **Logic App (Consumption)**.
3. Navigate to **Logic App Designer** -> **Code View** and replace the existing JSON.
4. Update the following variables and placeholders within the JSON:
    * `YOUR_SUBSCRIPTION_ID`: Your Azure Subscription GUID.
    * `YOUR_RESOURCE_GROUP`: The RG containing the Sentinel Workspace.
    * `YOUR_WORKSPACE_NAME`: The name of the Log Analytics Workspace.
    * `YOUR_TENANT_DOMAIN`: Your primary email domain (e.g., company.com).
    * `YOUR_TEAMS_CHANNEL_ID`: The target channel for SOC alerts.

## Required API Permissions
After enabling Managed Identity, ensure the following roles or Graph permissions are assigned:
* **Microsoft Sentinel Responder:** To update and close incidents.
* **Log Analytics Reader:** To query `EmailEvents` data.
* **Mail.ReadWrite** (Graph): If the workflow performs additional mailbox actions.
* **Chat.ReadWrite** (Graph): For posting failure notifications to Teams.
