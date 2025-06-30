# Deploy & Share ReactJS App with ngrok, Azure, and Microsoft Teams

- Exposing your local ReactJS app using **ngrok**
- Deploying your app to **Azure Static Web Apps**
- Adding it to **Microsoft Teams** 
- Connecting your app to a custom domain purchased via **GoDaddy**

---

##  STEP 1: Use ngrok for Local Testing

Use [ngrok](https://ngrok.com) to share your local React app (In my case Reactjs is already running on  `http://localhost:3000`) with a publicly accessible URL.

### 1.1 Create an ngrok Account

- Sign up at [https://ngrok.com](https://ngrok.com)

### 1.2 Get Your Auth Token

- Log in to the ngrok dashboard
- Navigate to **Your Authtoken** which is on top left
- Copy your **Auth Token**

### 1.3 Configure ngrok on Your Machine

```bash
ngrok config add-authtoken YOUR_TOKEN_HERE
```

### 1.4 Start a Tunnel for Your React App

- My React app runs on port 3000, start the tunnel:

```bash
ngrok http 3000
```
- This will generate a public URL like:

```bash
https://d3cf-157-50-100-160.ngrok-free.app
```
-  This will works till our reactjs runs in  testing env and as long as traffic forwards from app to ngrok.This is not gd for Prod env.

## STEP 2: Deploy ReactJS App to Azure + xyz.com (Custom Domain)
  
### 2.1 Create a React App

```bash
npx create-react-app my-react-app
cd my-react-app
```
### 2.2 Build for Production
```bash
npm run build
```
- This creates a build/ folder containing optimized static files.

### 2.3 Create an Azure Static Web App

- Visit https://portal.azure.com

- Click Create a Resource → Search: Static Web App → Create

- Fill in the form:

- Field	Value
- Subscription	Your Azure subscription
- Resource Group	Create new (e.g. react-rg)
- Name	react-webapp
- Region	Closest to your location
- Hosting Plan	Free
- Deployment Source	Other (manual deployment)

- Click Review + Create → then Create

### 2.4 Deploy Your React App to Azure

- Login to Azure CLI:

```bash
az login
```
Install Azure Static Web Apps CLI:

```bash
npm install -g @azure/static-web-apps-cli
```
- Deploy the built app:

```bash
swa deploy ./build --app-name react-webapp --env production
```
### 2.5 Add Your Custom Domain (e.g. xyz.com)

- Go to your Static Web App in the Azure Portal

- Click Custom domains → + Add

- Enter your domain: xyz.com

- Azure will provide required DNS records (CNAME or A Record)

### 2.6 Configure DNS in GoDaddy
- Visit https://godaddy.com

- Go to DNS settings for xyz.com

- Add a CNAME or A Record from Azure

- Field	Value from Azure
- Type	CNAME
- Host	@
- Points to	*.azurestaticapps.net
- TTL	1 hour (or default)

### 2.7 Enable HTTPS Automatically

- Wait ~30 minutes to 2 hours

Azure will verify the domain and apply a free SSL certificate

 Your ReactJS app is now live at:

```bash
https://xyz.com
```
## STEP 3: Add React App to Microsoft Teams

### 3.1 Create a manifest.json

```bash
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
```
- Replace "YOUR-GUID-HERE" with a real GUID (guidgenerator.com)

- Replace all URLs with your actual domain

### 3.2 Package Your Teams App

- Create the folder structure:

```bash
teams-app/
└── manifest.json
```
- Zip the contents:

```bash
cd teams-app
zip -r teams-app.zip *
```
### 3.3 Upload to Microsoft Teams (Individual Use)

- Go to https://dev.teams.microsoft.com

- Click Apps → + New App

- Choose Upload a custom app

- Upload teams-app.zip

- Click Install or Add to Teams

- The app will now be visible only to you

### 3.4 Publish Org-Wide (All Users) - I didnt tried this as it needs NexTurn Teams admin acess.

- Requires Teams Admin Access

- Go to https://admin.teams.microsoft.com

- Navigate to:
- Teams apps → Manage apps → Upload new app

- Upload your teams-app.zip

