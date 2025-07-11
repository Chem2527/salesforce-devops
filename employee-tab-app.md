# Manual Deployment & Automation for Azure Static Web Apps
- 1. Create Azure Static Web App (employee-tab-app)
     
## Prerequisites:
- Azure account

- Node.js and npm installed

- Azure CLI install:
  ```bash
 https://learn.microsoft.com/en-us/cli/azure/install-azure-cli
 ```

- Azure Static Web Apps CLI (swa) installed:

```bash
npm install -g @azure/static-web-apps-cli
```
## Step-by-step: Created a Static Web App in Azure

### 1. domain URL
```bash
https://orange-desert-0dd7ef91e.2.azurestaticapps.net
```
### 2. Manual Deployment Using SWA CLI
After building your frontend app:

```bash
npm install
npm run build
```
- Make sure you have a dist/ folder containing index.html.

Then, run:

```bash
swa deploy ./dist \
  --app-name employee-tab-app \
  --resource-group MS_Teams_Project \
  --env production
```

- Above command Uploads all files from the dist/ folder & deploys them to the production environment

Makes your app live at:
```bash
 https://orange-desert-0dd7ef91e.2.azurestaticapps.net
```
