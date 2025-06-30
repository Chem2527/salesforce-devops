 Deploy ReactJS App to Azure & Microsoft Teams (Org-Wide + Personal Use)
This guide walks you through how to:

 Deploy a ReactJS app to Azure Static Web Apps

 Connect it to a custom domain like xyz.com

 Integrate it into Microsoft Teams as a personal tab

 Share it with your entire organization or use it individually

 PART 1: Deploy ReactJS App to Azure + xyz.com
 STEP 1: Create a React App
bash
Copy
Edit
npx create-react-app my-react-app
cd my-react-app
 STEP 2: Build for Production
bash
Copy
Edit
npm run build
This creates a build/ folder containing static production-ready files.

STEP 3: Create an Azure Static Web App
Go to  https://portal.azure.com

Click "Create a Resource" → Search: Static Web App → Click Create

Fill in the form:

Field	Value
Subscription	Your Azure subscription
Resource Group	Create new (e.g. react-rg)
Name	sai-react-webapp
Region	Closest to your location
Hosting Plan	Free
Deployment Source	Other (manual deployment)

Click Review + Create → then Create

 STEP 4: Deploy React App to Azure
Install Azure CLI
 Install Guide

Login to Azure

bash
Copy
Edit
az login
Install Azure Static Web Apps CLI

bash
Copy
Edit
npm install -g @azure/static-web-apps-cli
Deploy your build

bash
Copy
Edit
swa deploy ./build --app-name sai-react-webapp --env production
 STEP 5: Add Your Custom Domain (xyz.com)
Go to the Static Web App in Azure Portal

Click Custom domains → + Add

Enter your domain: xyz.com

Azure will show DNS records (CNAME or A record) you need to add in GoDaddy

 STEP 6: Configure DNS in GoDaddy
Go to  https://godaddy.com

Open DNS Settings for xyz.com

Add a CNAME record:

Field	Value from Azure
Type	CNAME
Host	@
Points to	*.azurestaticapps.net
TTL	1 hour (or default)

If Azure gave you an A record, use that IP instead.

 STEP 7: Enable HTTPS (Auto)
Wait 30 minutes to 2 hours.

Azure will detect your domain

Automatically verify ownership

 Enable HTTPS with a free SSL certificate


Your ReactJS app is now live at:

arduino
Copy
Edit
https://xyz.com
 PART 2: Add React App to Microsoft Teams
 STEP 1: Create the manifest.json
json
Copy
Edit
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.16/MicrosoftTeams.schema.json",
  "manifestVersion": "1.16",
  "version": "1.0.0",
  "id": "YOUR-GUID-HERE",
  "packageName": "com.sai.reactapp",
  "developer": {
    "name": "Saikrishna",
    "websiteUrl": "https://xyz.com",
    "privacyUrl": "https://xyz.com/privacy",
    "termsOfUseUrl": "https://xyz.com/terms"
  },
  "name": {
    "short": "SaiApp",
    "full": "Sai React App in Teams"
  },
  "description": {
    "short": "React app in Teams",
    "full": "This ReactJS application is embedded inside Microsoft Teams as a personal tab."
  },
  "accentColor": "#FFFFFF",
  "staticTabs": [
    {
      "entityId": "home",
      "name": "Sai App",
      "contentUrl": "https://xyz.com",
      "scopes": [ "personal" ]
    }
  ],
  "permissions": [ "identity" ],
  "validDomains": [ "xyz.com" ]
}
 Replace "YOUR-GUID-HERE" with a generated GUID (use guidgenerator.com)
 Replace URLs with your actual domain and pages

 STEP 2: Package the Teams App
Create a folder called teams-app:

pgsql
Copy
Edit
teams-app/
└── manifest.json
Zip it:

bash
Copy
Edit
cd teams-app
zip -r teams-app.zip *
 PART 3A: Upload to Microsoft Teams (Individual)
Go to  https://dev.teams.microsoft.com

Click Apps → + New App

Choose Upload a custom app

Upload your teams-app.zip

Click Install or Add to Teams

 The app is now available only for you.

PART 3B: Publish Org-Wide (All Users)
Requires Teams Admin access.

 STEP 1: Upload to Teams Admin Center
Go to  https://admin.teams.microsoft.com

Navigate to:
Teams apps → Manage apps → Upload new app

Upload your teams-app.zip

