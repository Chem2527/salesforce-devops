# Deployment Procedure for Azure Static Web Apps – employee-tab-app

## Prerequisites:

- **Ensure you have the following set up:**

- Azure account 

- Node.js and npm installed

- Azure CLI installed

- Azure Static Web Apps CLI installed:

```bash
npm install -g @azure/static-web-apps-cli
```

## Step 1: Provision the Azure Static Web App


- Go to the Azure Portal

- Navigate to: Create a Resource → Static Web App

- Fill in the form:

  - App name: employee-tab-app

  - Resource group: MS_Teams_Project (create if not already present)

  - Hosting Plan: Select Free

  - Region: West US 2

  - Deployment Source: Choose Other (No source) — this allows manual deployment via CLI

  - Click Review + Create, then Create

  - Once provisioned, note the Default Domain (found in the "Overview" tab of the resource in the portal)

```bash
https://orange-desert-0dd7ef91e.2.azurestaticapps.net
```

## Step 2: Build the App for Deployment

- From your React project folder, run:

```bash
npm install
npm run build
```
- This should output your static files  into a folder like dist/

- Ensure the folder contains:

- index.html

- remoteEntry.js

- assets/ folder
- staticwebapp.config.json

## Step 3: Deploy to Azure Using SWA CLI

- Use the swa deploy command to publish your built app:

```bash
swa deploy ./dist \
  --app-name employee-tab-app \
  --resource-group MS_Teams_Project \
  --env production
```


- This command will:

- Upload contents of ./dist to Azure

- Trigger deployment to the production environment

## Step 4: Access the App
Once deployed successfully, access your app at:

```bash
https://orange-desert-0dd7ef91e.2.azurestaticapps.net
```
