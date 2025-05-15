Documentation: Retrieve and Commit Salesforce Metadata Using sf project retrieve start Command
Objective
Use the sf project retrieve start command to retrieve metadata for custom objects and fields from a Salesforce org, and then commit these changes to version control (Git) using a feature branch.

Steps
1. Create a Salesforce DX Project in VS Code
Open VS Code.

Press Ctrl+Shift+P to open the Command Palette.

Type and select SFDX: Create Project with Manifest.

Provide the name of the project, e.g., language-course-project, and choose a directory where the project will be created.

This will generate a Salesforce DX project structure, including the manifest/package.xml file for specifying which metadata to retrieve.

2. Authorize Your Salesforce Org
Press Ctrl+Shift+P and run SFDX: Authorize an Org.

When prompted, choose Login URL as https://login.salesforce.com (or https://test.salesforce.com for a sandbox).

Enter an alias for your org (e.g., languageCourseOrg).

Log in via the browser when prompted.

Note: This step authenticates your Salesforce org to the project, allowing you to retrieve metadata from it.

3. Create Custom Objects and Fields (via Salesforce Setup UI)
In your Salesforce org (via the Salesforce UI):

Navigate to Setup > Object Manager > Click Create > Custom Object.

Create the custom object Language_Course__c.

Create the custom object Language_Course_Instructor__c.

For the Language_Course__c object:

Create a Lookup or Master-Detail field to the Language_Course_Instructor__c object:

Field API Name: Course_Instructor__c.

4. Retrieve Metadata Using sf project retrieve start Command
Open the integrated terminal in VS Code (Ctrl+ `).

Run the following command to retrieve the metadata for the custom objects and fields:

bash
Copy
Edit
sf project retrieve start \
  --metadata CustomObject:Language_Course_Instructor__c \
  --metadata CustomObject:Language_Course__c \
  --metadata CustomField:Language_Course__c.Course_Instructor__c
This command will:

Retrieve Language_Course__c and Language_Course_Instructor__c custom objects.

Retrieve the Course_Instructor__c field from Language_Course__c.

The metadata files will be saved in the following directory structure:

swift
Copy
Edit
force-app/main/default/objects/
You can verify the changes in the VS Code Explorer.

5. Create a New Git Branch for Feature
Open the terminal in VS Code (Ctrl+ `).

Run the following Git command to create a new feature branch:

bash
Copy
Edit
git checkout -b feature/add-language-course-metadata
6. Commit the Retrieved Metadata
Stage the changes by adding the metadata to the staging area:

bash
Copy
Edit
git add force-app/main/default/objects/
Commit the changes with a clear commit message:

bash
Copy
Edit
git commit -m "Retrieve metadata for Language_Course and Language_Course_Instructor custom objects, and Course_Instructor field"
Push the changes to your remote repository:

bash
Copy
Edit
git push origin feature/add-language-course-metadata
7. Create a Pull Request
Go to your GitHub (or GitLab, Bitbucket) repository.

Click on Compare & Pull Request for your newly pushed branch.

In the PR description, add a brief explanation of the changes (e.g., added metadata for Language_Course__c, Language_Course_Instructor__c, and the related Course_Instructor__c field).

Submit the pull request for review.
