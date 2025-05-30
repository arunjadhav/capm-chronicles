---
title: "The Final Firewall"
summary: "Hardening CAP applications against real-world threats."
---

(Hardening the Fortress)

The app was live. The logs were clean. The tenants were isolated. The secrets were safe.
Alex leaned back, arms behind his head.

“We’ve done it. We’ve secured everything.”

Byte hovered ominously.
“Have you… hardened it?”

Alex blinked.
“Hardened it? Like… with concrete?”

Emma chuckled.
“He means security hardening—making sure the app is protected against real-world threats.”

## Byte Explains: What Is Hardening?
“Hardening is the process of reducing vulnerabilities by tightening configurations, disabling unnecessary features, and enforcing best practices.”

Byte summoned a checklist titled The Final Firewall.

## Enforce HTTPS
“Always use HTTPS in production. No exceptions.”

Emma checked the deployment settings in SAP BTP.
“Done. All traffic is encrypted.”

## Enable CSRF Protection
“CAP has CSRF protection built-in for web apps. Just make sure it’s not disabled.”
```json
"cds": {
  "csrf": {
    "enabled": true
  }
}
```

Alex nodded.
“No cross-site shenanigans allowed.”

## Disable Unused Endpoints
“If you’re not using certain services or entities, don’t expose them.”

Emma commented out a test service:
```cds
// service DevToolsService { ... }
```

“No need to leave the dev tools lying around in production.”

## Sanitize Logs
“Never log sensitive data—like passwords, tokens, or personal info.”

Alex updated the logging middleware:
if (req.data.password) delete req.data.password;

“Now our logs are clean and safe.”

## Validate Everything
“Even if you trust your UI, always validate on the backend.”

Emma added a custom check:
```javascript
if (req.data.stock < 0) {
  req.reject(400, 'Stock cannot be negative');
}
```

“Because users will find creative ways to break things.”

## Regularly Update Dependencies
Byte flashed a warning.
“Outdated libraries are like unlocked windows. Keep your dependencies up to date.”

Alex ran: npm audit fix

“All patched up.”

## Wrapping Up
Byte floated above the whiteboard and wrote:
Security isn’t a one-time task.
It’s a mindset.

Emma added:
“We’ve built the app. We’ve secured it. We’ve hardened it. Now it’s ready for the real world.”

Alex smiled.
“Let’s deploy it. And maybe… start planning the next adventure?”

Byte winked.
“CAP Chronicles: Part 3 — The Rise of Automation?”
