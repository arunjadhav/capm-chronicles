---
title: "The Role of Roles"
description: "Introducing role-based access control in CAP applications."
---
(Not All Heroes Wear Admin Badges)

The service was now locked. No more anonymous wanderers poking around the API. Alex leaned back, satisfied.

“Alright, Byte. The door’s locked. We’re safe.”

Byte blinked skeptically.
“Locked, yes. But right now, everyone with a key gets full access. Even the intern.”

Alex froze.
“Wait… even Kevin?”

Emma walked in, holding a sticky note labeled ‘Kevin’s To-Do List’. It read:
1. Deploy to production
2. Drop test data
3. Rename Books to Memes

“Yeah,” she said. “We need to talk about roles.”

## Byte Explains: Role-Based Access Control (RBAC)

“In CAP, roles are like access passes. You assign them to users, and then restrict parts of your service based on those roles.”

Byte summoned a hologram of a nightclub.
“Think of it like this: Everyone gets in the door, but only VIPs get into the lounge. And only staff can touch the DJ booth.”

Emma opened the CatalogService.cds file and added:
```cds
@requires: 'Admin'
entity Books as projection on my.Books;
```
“Now only users with the Admin role can access the Books entity.”

## Testing the VIP List

Alex tried accessing the service again—this time with a regular user token.
403 Forbidden: Insufficient privileges

“Nice,” he said. “Kevin’s locked out of the DJ booth.”

## Defining Roles in xs-security.json

Emma pulled up the xs-security.json file.
```json
{
  "role-templates": [
    {
      "name": "Admin",
      "description": "Full access to manage catalog",
      "scope-references": ["CatalogService.Admin"]
    },
    {
      "name": "Viewer",
      "description": "Read-only access to catalog",
      "scope-references": ["CatalogService.Read"]
    }
  ]
}
```

“This is where we define the roles and what they can do. Then we assign them to users in the BTP cockpit.”

## Byte’s Bonus Tip: Role Inheritance

“You can also use @restrict blocks for more fine-grained control,” Byte added.
```cds
entity Books as projection on my.Books {
  @restrict: [
    { grant: 'READ', to: 'Viewer' },
    { grant: '*', to: 'Admin' }
  ]
}
```

Now viewers can only read, and admins can do everything. Kevin? He can watch from the hallway.”

## Wrapping Up

Alex looked at the updated service definition.
“So now we’ve got a locked door and a guest list.”

Emma nodded.
“Exactly. And next, we’ll define what each guest is allowed to do.”

Byte’s eyes glowed.
“Prepare yourselves. The next chapter is about scopes and permissions—the fine print of access control.”
