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

---

Byte Jumps In
Byte: “Consuming services is a core part of CAP. You can connect to SAP S/4HANA, SuccessFactors, or even public OData services. CAP treats them like native models.”
“So I can use external services like I use my own entities?”
Byte: “Precisely. You define them in .cds files, bind them to destinations, and CAP handles the rest.”

---

Alex Gets Curious
“Okay Byte, show me an example.”
Byte: “Let’s use the classic: Northwind OData service. It’s public and perfect for demos.”

---

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
