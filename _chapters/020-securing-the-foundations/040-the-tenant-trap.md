---
title: "The Tenant Trap"
summary: "Exploring multi-tenancy in CAP applications."
---

(One App, Many Worlds)

The team was celebrating their latest deployment with cupcakes and confetti when Byte suddenly froze mid-bite (virtually, of course).

“We have a problem.”

Alex blinked.
“What kind of problem?”

Byte projected a screen full of logs.
Tenant A accessed data from Tenant B

Emma dropped her cupcake.
“That’s… not supposed to happen.”

## Byte Explains: What Is Multi-Tenancy?
“Multi-tenancy means one app serves multiple customers—tenants—but each tenant should only see their data.”

Byte summoned a diagram of parallel universes.
“Think of each tenant as a separate dimension. Same app, different data. But right now, our dimensions are leaking.”

## CAP’s Tenant Isolation
“CAP supports multi-tenancy out of the box,” Byte said. “But you need to activate it.”

Emma opened the package.json and added:
"cds": {
  "requires": {
    "db": {
      "kind": "sql",
      "vcap": "...",
      "multiTenant": true
    }
  }
}

“This tells CAP to isolate data per tenant. Each tenant gets their own schema or data partition.”

## Simulating Tenants
Alex spun up two test tenants: tenant-a and tenant-b. He added books to each.
cf create-service-instance myapp tenant-a
cf create-service-instance myapp tenant-b

Then he queried the data from each tenant’s context.
“Nice! Tenant A sees only their books. Tenant B sees theirs. No crossover.”

Byte nodded.
“The multiverse is stable again.”

## Bonus: Tenant-Aware Logic
Emma added a custom handler to log tenant-specific actions:
srv.before('READ', 'Books', (req) => {
  console.log(`Tenant ${req.tenant} is reading books`);
});

“Now we can track who’s doing what, and where.”

Alex grinned.
“So we’re not just building apps—we’re building parallel realities.”

## Wrapping Up
Byte floated above the whiteboard and wrote:
Multi-Tenancy = One App, Many Worlds
CAP = The Guardian of Dimensions

“Next,” he said, “we’ll explore secrets and credentials—because even in your own world, you don’t want to leave the vault open.”
