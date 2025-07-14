

# Deployment Procedure for Azure Static Web App: fulfiller-app

This guide provides the full procedure to provision and deploy the fulfiller-app React microfrontend to Azure Static Web Apps using the SWA CLI.

✅ Prerequisites
Ensure the following tools and services are set up:

✅ Azure account (with access to the correct subscription)

✅ Node.js and npm installed

✅ Azure CLI installed
📘 Install Azure CLI

✅ Azure Static Web Apps CLI installed:

bash
Copy
Edit
npm install -g @azure/static-web-apps-cli
🏗️ Step 1: Provision the Azure Static Web App
This is a one-time step — skip if fulfiller-app is already created.

Go to the Azure Portal
Navigate to: Create a Resource → Static Web App

Fill out the creation form:

App name: fulfiller-app

Resource group: MS_Teams_Project (use existing or create new)

Hosting Plan: Select Free

Region: Choose an appropriate region (e.g. East US)

Deployment Source: Select Other (No source) for manual CLI deployment

Click Review + Create, then Create

Once provisioned, you can find the default domain under the "Overview" tab:

bash
Copy
Edit
https://ambitious-desert-0c873a91e.1.azurestaticapps.net
🛠️ Step 2: Build the App for Deployment
From your app's root folder:

bash
Copy
Edit
npm install
npm run build
This generates your deployable files in a folder like dist/ or build/.

Ensure the output folder includes:

index.html

JavaScript bundles (remoteEntry.js, etc.)

Any assets your app needs

🚚 Step 3: Deploy to Azure using SWA CLI
Deploy the built app using the following command:

bash
Copy
Edit
swa deploy ./dist \
  --app-name fulfiller-app \
  --resource-group MS_Teams_Project \
  --env production
Add --verbose for more detailed output if needed.

This will:

Upload all files from the ./dist folder

Trigger a deployment to the production environment

🌐 Step 4: Access the Deployed App
After deployment completes, access your app using:

bash
Copy
Edit
https://ambitious-desert-0c873a91e.1.azurestaticapps.net
