---
layout: chapter
order: 140
title: "Scopes and Permissions"
description: "Explaining scopes vs roles and their implementation in CAP applications."
---
(The Fine Print of Power)

The office was quiet. Too quiet.

Alex was sipping his third coffee when he noticed something odd in the logs.
“Hey… why is Kevin able to delete books? I thought we locked that down!”

Emma looked up from her laptop.
“We gave him the Editor role, remember?”

“Yeah, but I only wanted him to update titles—not delete entire records!”

Byte materialized with a dramatic sigh.
“Ah, the classic mistake. You gave him the keys to the car, but forgot to say don’t drive it off a cliff.”

## Byte Explains: Scopes vs Roles
“Roles are like job titles—Admin, Viewer, Editor. But scopes are the actual permissions—like CatalogService.Read, CatalogService.Update, or CatalogService.Delete.”

Byte projected a chart:
Role	Scopes Included
Admin	All scopes
Editor	Read, Update
Viewer	Read only

“Scopes are the fine print. You assign them to roles in xs-security.json, and then CAP checks them at runtime.”

## Defining Scopes in xs-security.json
Emma opened the file and added:
```json
{
  "scopes": [
    {
      "name": "$XSAPPNAME.CatalogService.Read",
      "description": "Read access to catalog"
    },
    {
      "name": "$XSAPPNAME.CatalogService.Update",
      "description": "Update access to catalog"
    },
    {
      "name": "$XSAPPNAME.CatalogService.Delete",
      "description": "Delete access to catalog"
    }
  ],
  "role-templates": [
    {
      "name": "Editor",
      "description": "Can read and update books",
      "scope-references": [
        "$XSAPPNAME.CatalogService.Read",
        "$XSAPPNAME.CatalogService.Update"
      ]
    }
  ]
}
```

“Now the Editor role can’t delete anything. Kevin’s cliff-diving days are over.”

## Enforcing Scopes in CDS
Byte added a new restriction to the service:
```cds
entity Books as projection on my.Books {
  @restrict: [
    { grant: 'READ', to: 'CatalogService.Read' },
    { grant: 'UPDATE', to: 'CatalogService.Update' },
    { grant: 'DELETE', to: 'CatalogService.Delete' }
  ]
}
```

“This way, CAP checks the user’s scopes before allowing any operation. No scope, no action.”

Alex nodded.
“So scopes are like verbs, and roles are just bundles of those verbs?”

“Exactly,” Byte said. “Roles are the lunchbox. Scopes are the snacks inside.”

## Testing the Fine Print
Alex logged in as Kevin and tried to delete a book.
403 Forbidden: Missing scope 'CatalogService.Delete'

He smiled.
“Perfect. Kevin can edit titles, but he can’t nuke the library.”

Emma raised an eyebrow.
“Let’s just hope he doesn’t find a way to rename all books to ‘Untitled’.”

## Wrapping Up
Byte hovered over the whiteboard and wrote:
Roles = Who you are
Scopes = What you can do

“And next,” he said, “we’ll explore multi-tenancy—because sometimes, you’re not just protecting data from users… you’re protecting it from other customers.”
