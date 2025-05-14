# salesforce-devops
## Salesforce DX Setup & Dreamhouse App Deployment Guide

- This guide walks through setting up a Salesforce DX environment, connecting orgs, and deploying the Dreamhouse LWC app using Salesforce CLI.

### Prerequisites
- Before you begin, make sure you have:

- A Salesforce Trailhead Playground or Developer Edition org

Salesforce CLI installed
Check version:
```bash
sf --version
```

### Steps Overview
#### Create and Launch a Salesforce Org
From Trailhead, create and launch a Trailhead Playground.

#### Connect Your Org to Salesforce CLI
Use the Salesforce CLI to authorize your org:

```bash
sf org login web -a SaiOrg
```
-a SaiOrg: Sets the alias SaiOrg for easy reference.

#### Clone the Dreamhouse App from GitHub
```bash
git clone https://github.com/trailheadapps/dreamhouse-lwc.git

cd dreamhouse-lwc/
git checkout -b my_branch
```
#### Authorize a Dev Hub Org

Dev Hub is required to create scratch orgs:

```bash
sf org login web -a DevHub
sf config set defaultdevhubusername DevHub
```

#### Create a Scratch Org

```bash
sf org create scratch -f config/project-scratch-def.json -a dreamhouse-org -d
```
-f: Path to scratch org definition file

-a: Alias for the new scratch org

-d: Set as default for this project

#### Open the Scratch Org
```bash
sf org open
```
#### Deploy Project Source to Scratch Org
```bash
sf project deploy start
```
- This pushes metadata from your local DX project to the scratch org.

#### Assign the Required Permission Set
```bash
sf org assign permset -n Dreamhouse
```
- Gives your scratch org user access to the Dreamhouse app features.

#### Import Sample Data

```bash
sf data import tree -p data/sample-data-plan.json
```
- This loads sample property and broker data into the org.

#### Open and Explore the App
```bash
sf org open
```
Navigate to the Dreamhouse app and explore listings, brokers, and more.

#### Notes
- You only need to enable Dev Hub once per org.

- Scratch orgs expire in 7 days by default.


#### Completed Flow Summary

- Connect Dev Hub	sf org login web -a DevHub
- Set Default Dev Hub	sf config set defaultdevhubusername DevHub
- Clone Project	git clone ...
- Create Scratch Org	sf org create scratch -f config/project-scratch-def.json -a dreamhouse-org -d
- Open Scratch Org	sf org open
- Deploy Source	sf project deploy start
- Assign Permissions	sf org assign permset -n Dreamhouse
- Import Data	sf data import tree -p data/sample-data-plan.json
- Launch App	sf org open

