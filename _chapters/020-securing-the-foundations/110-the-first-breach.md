---
layout: chapter
order: 120
title: "The First Breach"
description: "Understanding authentication basics in CAP applications."
---

(Who Goes There?)

The sun had barely risen over the digital skyline of Alex’s CAP project. The services were humming, the data was flowing, and the UI was looking slick. Everything seemed perfect.
Too perfect.

Byte, the ever-watchful AI assistant, suddenly blinked red.
“Unauthorized access attempt detected.”

Alex nearly spilled his coffee.
“Wait—what? Who’s trying to get in?”

Byte projected a log entry onto the wall:
[WARN] Anonymous request to /catalog/Books
[INFO] No authentication token provided

Emma walked in, still tying her hoodie.
“Looks like someone’s knocking on the door without a key.”

## Byte Explains: Authentication 101

“CAP services are like exclusive clubs,” Byte said. “And right now, yours has no bouncer.”

Alex frowned.
“So anyone can just walk in?”

“Exactly. Unless you set up authentication, your service is wide open.”

Byte waved a virtual wand and summoned a diagram of OAuth2, JWT tokens, and XSUAA.
“CAP integrates with identity providers like SAP BTP’s XSUAA. When a user logs in, they get a token—a digital ID badge. CAP checks that badge before letting them in.”

## Locking the Doors

Emma opened the CatalogService.cds file and added a single line:
@requires: 'authenticated-user'
service CatalogService {
  entity Books as projection on my.Books;
}

“Boom,” she said. “Now only authenticated users can access the service.”

Alex raised an eyebrow.
“That’s it? Just one line?”

“Yep. CAP handles the rest. It checks the token, verifies the user, and blocks anonymous requests.”

## Testing the Lock

Alex tried accessing the service again—this time without logging in.
403 Forbidden: Authentication required

He grinned.
“Nice. Now it’s a club with a velvet rope.”

Byte nodded.
“And soon, we’ll add a guest list.”

## What’s Next?

Emma pointed to the whiteboard.
“Now that we’ve locked the door, we need to decide who gets in and what they can do.”

Byte’s eyes glowed.
“Next stop: roles and permissions. Because not every guest gets access to the VIP lounge.”
