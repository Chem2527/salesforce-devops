# Set Up ngrok for Local Testing and Sharing

If you want to expose your local React app running on port 3000 to the internet for demos or testing, follow these steps to set up ngrok properly:

- Step 1: Create an ngrok Account
Visit https://ngrok.com and sign up for a free account.

- Step 2: Find Your ngrok Auth Token

- After signing in, navigate to the Dashboard.

- Locate your Auth Token (under Setup & Installation).



- Step 3: Configure ngrok with Your Auth Token
- 
- Run below command in your terminal, replacing YOUR_TOKEN_HERE with your actual token:

```bash
ngrok config add-authtoken YOUR_TOKEN_HERE
```

- Step 4: Start an ngrok Tunnel to Your Local React App
- For my case React app runs locally on port 3000, run:

```bash
ngrok http 3000
```
- ngrok will generate a publicly accessible URL for my case: its ( **https://d3cf-157-50-100-160.ngrok-free.app**) that tunnels traffic to your local app.
