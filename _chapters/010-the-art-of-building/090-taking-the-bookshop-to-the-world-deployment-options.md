---
layout: chapter
title: "Taking the Bookshop to the World — Deployment Options"
---

As the Bookshop app neared completion, Alex asked:

Alex: “So… how do we actually deploy this?”

Emma smiled. “CAP gives you several options, depending on where you want to run it.”

Alex: “I want to deploy to Cloud Foundry. Can you break it down for me?”

Emma: “Absolutely! Here’s a simple, real-world guide based on the official SAP steps.”

---

## 🚀 Deploying Your CAP App to Cloud Foundry (CF)

### 1. Prerequisites
- **SAP BTP trial or subaccount** with SAP HANA Cloud database running
- **Cloud Foundry CLI** (cf) and MTA plugin installed
- **Latest @sap/cds-dk** globally and @sap/cds in your project
- **Cloud MTA Build Tool (mbt)** installed globally

### 2. Prepare Your Project for Production
Open PowerShell in your project folder and run:

```powershell
# Add SAP HANA for production
cds add hana --for production

# Add authentication/authorization (XSUAA)
cds add xsuaa --for production

# Add MTA deployment descriptor
cds add mta

# (Optional) Add App Router if you want a custom entry point
cds add approuter
```

### 3. Build the MTA Archive
```powershell
mbt build
```
This creates an `mta_archives` folder with a `.mtar` file (your deployable app package).

### 4. Log in to Cloud Foundry
```powershell
cf login -a https://api.<your-cf-endpoint> -u <username> -p <password>
```

### 5. Deploy to Cloud Foundry
```powershell
cf deploy mta_archives/*.mtar
```

### 6. Check Your App
- Go to the SAP BTP Cockpit > Your Subaccount > Cloud Foundry > Spaces > Applications
- Find your app and open the URL provided

### 7. (Optional) Assign Roles
If you use admin APIs, assign the required roles to your user in the BTP Cockpit.

---

Alex: “So, just follow these steps and my Bookshop is live in the cloud?”

Byte: “Exactly! For more details, check the [official CAP deployment guide](https://cap.cloud.sap/docs/guides/deployment/to-cf).”

Emma: “And remember, you can always update your app by rebuilding and redeploying the .mtar file.”

Alex: “Thanks! That makes it super clear.”
