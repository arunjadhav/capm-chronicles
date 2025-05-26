---
layout: chapter
order: 50
title: "The Other Side of the Service"
---

The Question That Changed the Perspective
Emma leaned against Alex’s desk, sipping her coffee.
“So,” she asked casually, “you’ve gotten pretty good at providing services. But what about consuming them?”
Alex blinked. “Consuming?”
“Yeah. What if your CAP app needs data from an SAP backend? Or a public API? You’re not always the one serving.”
Alex paused. “Huh. I didn’t think about that.”
“Exactly,” Emma said. “Time to flip the script.”

________________________________________

Byte Jumps In
Byte: “Consuming services is a core part of CAP. You can connect to SAP S/4HANA, SuccessFactors, or even public OData services. CAP treats them like native models.”
“So I can use external services like I use my own entities?”
Byte: “Precisely. You define them in .cds files, bind them to destinations, and CAP handles the rest.”

________________________________________

Alex Gets Curious
“Okay Byte, show me an example.”
Byte: “Let’s use the classic: Northwind OData service. It’s public and perfect for demos.”

________________________________________

Step-by-Step: Consuming Northwind

📁 srv/external.cds
```cds
external service Northwind {
  entity Products as projection on Products;
}
```

📁 package.json (add destination)
```json
"cds": {
  "requires": {
    "Northwind": {
      "kind": "odata",
      "model": "srv/external",
      "credentials": {
        "url": "https://services.odata.org/V2/Northwind/Northwind.svc/"
      }
    }
  }
}
```

📁 srv/catalog-service.cds
```cds
using { Northwind as nw } from './external';
service CatalogService {
  entity Products as projection on nw.Products;
}
```

“That’s it?” Alex asked.
Byte: “That’s it. Now your app can read products from Northwind like they’re local.”

________________________________________

Testing the Integration
Alex added a new request to his test.http file:
```
### Get products from Northwind
GET http://localhost:4004/catalog/Products
```
He clicked Send Request.
📦 A list of products appeared—Chai, Chang, Aniseed Syrup...
“This is wild,” Alex whispered. “I’m pulling live data from a public service.”

________________________________________

Emma Wraps It Up
“Now imagine that’s not Northwind,” Emma said, “but your company’s SAP backend. You can consume services from S/4HANA, reuse existing logic, and extend it in CAP.”
“So CAP isn’t just about building apps—it’s about connecting them.”
“Exactly. It’s the glue.”
Alex smiled.
“Okay. I’m ready to connect the world.”
