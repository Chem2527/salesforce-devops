#  Deployment procedure for Azure Static Web Apps for employee-tab-app
✅ Prerequisites
Ensure you have the following set up:

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
You only need to do this once — skip if employee-tab-app is already created.

Go to the Azure Portal
Navigate to: Create a Resource → Static Web App

Fill in the form:

App name: employee-tab-app

Resource group: MS_Teams_Project (create if not already present)

Hosting Plan: Select Free

Region: Choose a global region close to your users (e.g. Central US)

Deployment Source: Choose Other (No source) — this allows manual deployment via CLI

Click Review + Create, then Create

Once provisioned, note the Default Domain:

bash
Copy
Edit
https://orange-desert-0dd7ef91e.2.azurestaticapps.net
You can find this under the "Overview" tab of the resource in the portal.

🛠️ Step 2: Build the App for Deployment
From your React project folder, run:

bash
Copy
Edit
npm install
npm run build
This should output your static files (HTML, JS, assets) into a folder like dist/ or build/.

Ensure it contains:

index.html

Supporting JS files (e.g. remoteEntry.js)

Assets folder (if applicable)

🚚 Step 3: Deploy to Azure using SWA CLI
Now use the swa deploy command to publish your built app:

bash
Copy
Edit
swa deploy ./dist \
  --app-name employee-tab-app \
  --resource-group MS_Teams_Project \
  --env production
Optional: Add --verbose for detailed output.

The CLI will:

Upload contents of ./dist to Azure

Trigger deployment to the production environment

🌐 Step 4: Access the App
Once deployed successfully, access your app at:

bash
Copy
Edit
https://orange-desert-0dd7ef91e.2.azurestaticapps.net
