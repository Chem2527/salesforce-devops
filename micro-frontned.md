# Deployment Procedure for Azure Static Web App: micro-frontend

## Prerequisites
- Azure account

- Node.js and npm

- Azure CLI

- Azure Static Web Apps CLI:

```bash
npm install -g @azure/static-web-apps-cli
```

## Step 1: Provision the Azure Static Web App
- Go to the Azure Portal

- Navigate to: Create a Resource → Static Web App

- Fill in the form:

- App name: sf-tab-app

- Resource group: MS_Teams_Project (create if it doesn't exist)

- Hosting Plan: Free

- Region: West US 2

- Deployment Source: Choose "Other

- Click "Review + Create", then "Create"

- After provisioning, note the Default Domain:

```bash
https://purple-mushroom-05d06d31e.1.azurestaticapps.net
```
## Step 2: Prepare Your App for Deployment

From your micro frontend project directory, run:

```bash
npm install
npm run build
```
Ensure the dist/ folder contains:
```bash
index.html
remoteEntry.js
staticwebapp.config.json
```

## Step 3: Deploy with SWA CLI
Deploy your app using the following command:

```bash
swa deploy ./dist \
  --app-name sf-tab-app \
  --resource-group MS_Teams_Project \
  --env production
```

- This command will  upload the contents of ./dist to Azure

## Step 4: Access the Live App
Once deployed, your app will be available at:

```bash
https://purple-mushroom-05d06d31e.1.azurestaticapps.net
```
