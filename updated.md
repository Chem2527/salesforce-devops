# Salesforce Demo Project (with Source Tracking)

This repository demonstrates a modern Salesforce DevOps workflow using the Salesforce CLI (`sf`), Git, and GitHub with **source tracking** via **Scratch Orgs**. It covers creating a project, managing metadata with change tracking, collaborating with feature branches, and deploying back to Salesforce environments.

---

##   Prerequisites

- Salesforce Developer Org with **Dev Hub enabled**
- [Node.js](https://nodejs.org/en) installed
- [Git](https://git-scm.com/) installed  
- [Visual Studio Code](https://code.visualstudio.com/) (recommended)
- Salesforce Extension Pack for VS Code
- Salesforce CLI installed:
  ```bash
  npm install --global @salesforce/cli
  sf --version
  Setup and Usage
1. Create a New Salesforce DX Project
bash
Copy
Edit
sf force:project:create -n salesforce-demo
cd salesforce-demo
2. Log in to Dev Hub (Enable in your Dev Org)
bash
Copy
Edit
sf org login web --alias DevHub --set-default-dev-hub
You must enable Dev Hub in your Salesforce Dev Org via Setup → Dev Hub.

3. Create a Scratch Org with Source Tracking
bash
Copy
Edit
sf org create scratch --alias ScratchDev --definition-file config/project-scratch-def.json --duration-days 7 --set-default
Example project-scratch-def.json:

json
Copy
Edit
{
  "orgName": "Salesforce Demo",
  "edition": "Developer",
  "features": ["AuthorApex", "API"],
  "settings": {
    "orgPreferenceSettings": {
      "s1DesktopEnabled": true
    }
  }
}
4. Push Local Source to the Scratch Org
bash
Copy
Edit
sf project deploy start --target-org ScratchDev
# OR (legacy)
sfdx force:source:push
5. Make Metadata Changes (Apex, Flows, etc.)
Either directly in Scratch Org via the UI

Or locally in the force-app folder (VS Code, etc.)

6. Pull Changes from Scratch Org (Tracked)
bash
Copy
Edit
sf project retrieve start --target-org ScratchDev
# OR (legacy)
sfdx force:source:pull
This pulls only changed metadata thanks to source tracking.

7. Initialize Git Repository and Commit Source
bash
Copy
Edit
git init
git add .
git commit -m "Initial commit: pulled from ScratchDev"
8. Push Your Code to GitHub
Create a GitHub repository and push:

bash
Copy
Edit
git remote add origin https://github.com/YOUR_USERNAME/salesforce-demo.git
git push -u origin main
9. Collaborate via Feature Branches
bash
Copy
Edit
git checkout -b feature/login-page
Update or create an Apex class, for example:

force-app/main/default/classes/LoginPage.cls

Then commit and push:

bash
Copy
Edit
git add force-app/main/default/classes/LoginPage.cls
git commit -m "Add login page Apex class"
git push origin feature/login-page
Create a Pull Request (PR) to merge into main.

10. Deploy to Sandbox or Production (No Tracking Here)
After the PR is merged:

bash
Copy
Edit
sf deploy metadata --target-org ProdOrg --source-path force-app
You can also authenticate and alias other orgs:

bash
Copy
Edit
sf org login web --alias ProdOrg
sf org login web --alias TestOrg
  Summary
Build DX project with sf

Use Scratch Orgs for development with source tracking

Push/pull changes via source:push/pull or project deploy/retrieve

Version control with Git + GitHub

Collaborate using feature branches + PRs

Deploy to permanent orgs (Prod, Test) with sf deploy metadata
