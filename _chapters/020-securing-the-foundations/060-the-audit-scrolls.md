---
title: "The Audit Scrolls"
summary: "Implementing logging and auditing in CAP applications."
---

(Every Action Leaves a Trace)

The app was live. The tenants were isolated. The secrets were safe.
Alex leaned back, proud.

“I think we’ve finally secured everything.”

Byte raised an eyebrow.
“Have you?”

Emma looked up from her screen.
“What if someone with access does something they shouldn’t? Like delete all the books?”

Alex blinked.
“Oh no. Kevin.”

## Byte Explains: Why Logging Matters
“Security isn’t just about keeping bad actors out. It’s also about tracking what happens inside—especially when things go wrong.”

Byte summoned a glowing scroll labeled Audit Trail.
“CAP lets you log important events, track user actions, and even integrate with external audit systems.”

## Logging User Actions
Emma opened the service handler and added a simple log:
srv.before(['CREATE', 'UPDATE', 'DELETE'], 'Books', (req) => {
  console.log(`[AUDIT] ${req.user.id} is performing ${req.event} on Books`);
});

“Now we’ll know who’s doing what. And when Kevin tries to delete everything again, we’ll have proof.”

Alex nodded.
“So this is like a security camera for our service?”

“Exactly,” Byte said. “Except it doesn’t need batteries.”

## Logging with Context
Byte added more detail:
srv.before('*', (req) => {
  console.log(`[AUDIT] ${req.user.id} called ${req.event} on ${req.target.name} at ${new Date().toISOString()}`);
});

“This logs every event, with timestamps and target entities. You can even store these logs in a secure table if needed.”

## Integrating with External Systems
Emma pointed to the architecture diagram.
“In production, we can forward logs to systems like SAP Cloud Logging, Elastic Stack, or Splunk for real-time monitoring and alerts.”

Byte nodded.
“And don’t forget to sanitize sensitive data before logging. Never log passwords, tokens, or personal info.”

## Wrapping Up
Byte floated above the whiteboard and wrote:
If it’s not logged, it didn’t happen.
Audit everything. Trust, but verify.

Emma added:
“Next up: hardening the fortress. We’ve built the walls—now let’s reinforce them.”
