---
title: "The Secret Keepers"
summary: "Managing secrets and credentials securely in CAP applications."
---

(Hide Your Keys, Guard Your Vault)

It was a quiet afternoon. Birds chirped. Logs were clean. No errors. No breaches.
Too quiet.

Alex was reviewing the code when he spotted something that made his stomach drop.
```javascript
const dbPassword = 'SuperSecret123!';
```

“Uhh… guys? I think I just hardcoded a password.”

Byte’s eyes turned red.
“You what?!”

Emma nearly dropped her laptop.
“Alex. That’s like taping your house key to the front door.”

## Byte Explains: Why Secrets Must Stay Secret
“Hardcoding secrets is a security nightmare. If someone gets access to your codebase, they get everything—DB credentials, API keys, admin tokens. It’s like handing them the keys to the kingdom.”

Byte summoned a vault icon.
“CAP apps should use environment variables and secure bindings to manage secrets.”

## Using Environment Variables
Emma opened the .env file:
```javascript
DB_PASSWORD=SuperSecret123!
```

Then in the code:
```javascript
const dbPassword = process.env.DB_PASSWORD;
```

“Now the secret is outside the code. We can manage it securely in deployment environments.”

Byte nodded.
“And in production, you don’t even use .env—you use VCAP_SERVICES from the platform.”

## Secure Service Bindings in SAP BTP
Byte projected a sample VCAP_SERVICES snippet:
```json
{
  "hana": [
    {
      "credentials": {
        "user": "admin",
        "password": "SuperSecret123!"
      }
    }
  ]
}
```

“When you bind a service in SAP BTP, the credentials are injected into your app’s environment. CAP reads them automatically.”

Emma added to package.json:
```json
"cds": {
  "requires": {
    "db": {
      "kind": "hana",
      "vcap": "hana"
    }
  }
}
```
“Now CAP knows where to find the credentials—without us ever touching them.”

## Testing the Vault
Alex removed the hardcoded password and restarted the app.
“It still works. And now the password’s not in the code.”

Byte smiled.
“Congratulations. You’ve just passed Secret-Keeping 101.”

## Wrapping Up
Byte floated above the whiteboard and wrote:
Secrets don’t belong in code.
Use env vars and bindings instead.

Emma added:
“Next up: logging and auditing. Because even with secrets locked away, you still need to know who did what—and when.”
