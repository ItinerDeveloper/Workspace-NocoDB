# Itiner Workspace NocoDB Integration Addon Installation Guide

## 1. Preparation

### 1.1 System Requirements
- Windows operating system
- Internet Information Services (IIS)
- HTTPS certificate
- Installed Itiner Workspace application

### 1.2 File System
The NocodbIntegration module **must be located in the same folder as the Itiner Workspace application**. 
Recommended structure:
D:\ItinerWorkspace\NocodbIntegration\

---

## 2. Installation Steps

### 2.1 Copy the NocoDB Integration Folder
1. Unzip the `ItinerWorkspaceService_NocoDBIntegration_nocodb-x.x.x.ZIP`.
2. Copy the `NocodbIntegration` folder to `D:\ItinerWorkspace\`.

---

## 3. NocoDB Integration Setup

### 3.1 Required Files
Ensure the following files exist in the `NocodbIntegration` folder:
- `runtimes` folder
- `.dll` files
- `ProtocolNocoDBWebhook` file
- `.deps` files
- `appsettings.json`
- `Web.config`

### 3.2 IIS Application Pool
1. Open IIS Manager.
2. Create a new application pool:
   - Name: `ItinerWorkspace_NocodbIntegration` (or custom)
   - .NET CLR Version: No Managed Code
   - Managed Pipeline Mode: Integrated

### 3.3 Website Configuration
Install the NocoDB Integration on the same site as Itiner Workspace (e.g., `Default Website`).

### 3.4 Configuration
Edit the `appsettings.json` file with the following parameters:
- `Host/WebHostUrl`: Full API URL (e.g., `http://yourdomain/NocodbIntegration`)
- `Host/WSUrl`: Itiner Workspace API URL
- `NocoDB/APIUrl`: NocoDB server URL
- `NocoDB/APIToken`: NocoDB connection token
- `NocoDB/Project`: NocoDB database name
- `Storage/Password`: File encryption hash
- `Hmac`: WebHook encryption password
- `Serilog`: Logging parameters

#### Reference Filter Configuration
```json
"Reference": {
  "Filter": [] // ["key1", "key2"]
}
```
- **Purpose**: Controls which events the integration service processes based on the `Reference` value in the event.
- **Behavior**:
  - If the `Filter` list is **not empty**, the integration service will **only process events** that contain a reference included in the `Filter` list.
  - If the `Filter` list is **empty**, the service will process **all events**, regardless of their `Reference` value.
- **Usage**: Populate the `Filter` list with user-defined keys to restrict the scope of processed events.


#### Variable Prefix Configuration
```json
"Host": {
  "VariablePrefix": "prefix."
}
```
- **Purpose**: Ensures compatibility when the workflow sending events to the integration service is an embedded workflow and uses prefixed variable names.
- **Behavior**:
  - All variables in the embedded workflow will have a prefix in their names.
  - The integration service requires a matching prefix to correctly interpret these variables.
- **Usage**: Configure the `VariablePrefix` field with the appropriate prefix used in the workflow.

### 3.5 Add IIS Web Application
1. Add a new web application in IIS:
   - **Alias**: `nocodbIntegration`
   - **Application Pool**: Select the pool created in 3.2
   - **Physical Path**: `D:\ItinerWorkspace\NocodbIntegration`

---

## 4. Logging
By default, logs are sent to an SEQ server. Optionally, configure file or database logging.

---

## 5. Restart
After setup, restart the application pool in IIS Manager.

---

## 6. Updating the NocoDB Integration
1. **Stop** the application pool in IIS.
2. Replace the `NocodbIntegration` folder with the updated version.
3. Update `appsettings.json` if new keys are required.
4. **Restart** the application pool.

---

This document details a seamless integration process for NocoDB into your Itiner Workspace application. For further assistance, consult your development team or system administrator.
