# Salesforce Demo Project

This repository demonstrates a basic Salesforce DevOps workflow using the Salesforce CLI (`sf`), Git, and GitHub. It covers creating a project, managing metadata, collaborating with feature branches, and deploying back to Salesforce.

---

## Prerequisites

- Salesforce Developer Org(s)
- [install node](https://nodejs.org/en)
- [Git](https://git-scm.com/) installed  
- [Visual Studio Code](https://code.visualstudio.com/) (recommended)
- Salesforce Extension Pack for VS Code
- run below command for sf installation
  ```bash
  npm install --global @salesforce/cli
  sf --version
  ```

---

## Setup and Usage

### 1. Create a New Salesforce Project

```bash
sf force:project:create -n salesforce-demo
cd salesforce-demo
2. Log in to Multiple Salesforce Orgs and Set Aliases

sf org login web --alias DevOrg
sf org login web --alias TestOrg
sf org login web --alias ProdOrg
3. Retrieve Apex Classes from a Specific Org

sf retrieve metadata --metadata ApexClass --target-org DevOrg
This pulls Apex classes into your local project folder, usually:


force-app/main/default/classes/
4. Initialize Git Repository and Commit Code

git init
git add .
git commit -m "Initial commit: Apex classes from DevOrg"
5. Push Your Code to GitHub
Create a new repository on GitHub (e.g., salesforce-demo).

Copy the repository remote URL.

Run:


git remote add origin https://github.com/YOUR_USERNAME/salesforce-demo.git
git push -u origin main
6. Collaborate Using Feature Branches
Create a new branch for your feature:


git checkout -b feature/login-page
Create or update your Apex class (e.g., LoginPage.cls) inside:


force-app/main/default/classes/
Add and commit your changes:


git add force-app/main/default/classes/LoginPage.cls
git commit -m "Add login page class"
git push origin feature/login-page
Open a Pull Request (PR) on GitHub to merge your feature branch into main.

7. Deploy Changes Back to Salesforce Org
After merging the PR, deploy your changes to the Salesforce org:


sf deploy metadata --source-path force-app --target-org DevOrg
Summary
Create projects with sf CLI

Manage multiple orgs with aliases

Retrieve and deploy metadata selectively

Use Git and GitHub for version control and collaboration

Deploy code back to Salesforce smoothly


