# 🚀 Azure Logic Apps Library

A centralized repository for enterprise-grade Azure Logic App (Consumption) templates, categorized by business function and trigger type.

---

## 📁 Repository Directory

| Category | Workflow Name | Trigger Type | Status | Path |
| :--- | :--- | :--- | :--- | :--- |
| **SecOps** | SecOps-NonUKAccess-Provisioning(Instant) | **SharePoint** (Create/Modify) | ✅ Stable | [Browse](./SecOps-NonUKAccess-Provisioning/Instant) |
| **SecOps** | SecOps-NonUKAccess-Provisioning(Scheduled) | **Recurrence** (Daily) | ✅ Stable | [Browse](./SecOps-NonUKAccess-Provisioning/Scheduled) |

---

## 🏗️ Folder Hierarchy Explained
To make finding workflows easier, this library follows a strict naming convention:
`Category-ProcessName / TriggerType / File.json`

* **Category:** The department or functional area (e.g., SecOps, FinOps, IT).
* **TriggerType:** How the app starts (e.g., `Instant` for manual buttons, `Recurrence` for schedules, `Webhook` for API calls).

---

## 🚀 Deployment Guide
1. **Pick a Workflow:** Navigate to the folder link in the table above.
2. **Copy JSON:** Open the `.json` file (e.g., `Instant.json`) and copy the raw code.
3. **Create in Azure:** - Create a **Logic App (Consumption)** in your Azure Portal.
   - Open **Logic App Designer** and switch to **Code View**.
   - Paste the JSON over the existing code.
4. **Update Variables:** Look for the `Initialize variables` actions in the designer and replace placeholders like `<YOUR_TENANT_ID>` with your actual values.
5. **Connections:** You must manually fix and "Authorize" API connections (SharePoint, Office 365, etc.) after deployment.

---

## 🔐 Security Policy
**NEVER** commit files containing:
* Actual Tenant IDs or Subscription IDs.
* Client Secrets or Passwords.
* Personal email addresses.

Always use `<PLACEHOLDERS>` before uploading.

---

## ⚖️ License
This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.
