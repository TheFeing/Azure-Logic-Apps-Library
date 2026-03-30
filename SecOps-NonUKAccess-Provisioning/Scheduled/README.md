# Non-UK Access Provisioning (Scheduled)

## Overview
This version of the workflow runs on a daily schedule (00:01 UTC). 

### What it does:
1. **Removal:** Checks for users whose `LastValidDate` was yesterday and removes them from the Entra ID Group.
2. **Provisioning:** Checks for users whose `FirstValidDate` is today and adds them to the Entra ID Group.
3. **Logging:** Queries Log Analytics for the user's managed devices and updates a Sentinel Watchlist, which can be used for suppressing a Sentinel Analytics Rule alert.

## Configuration
Update the following variables in the `Initialize variables` action:
- `GroupID`: The target Entra ID Group GUID.
- `SubscriptionID`: Your Azure Subscription ID.
- `WorkspaceID`: Your Log Analytics Workspace ID.
- `ResourceGroup`: The RG containing your Sentinel Workspace.
