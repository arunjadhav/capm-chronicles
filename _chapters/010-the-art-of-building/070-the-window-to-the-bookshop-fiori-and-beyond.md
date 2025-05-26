---
layout: chapter
order: 70
title: "The Window to the Bookshop — Fiori and Beyond"
---

The backend of the Bookshop application was solid. Services were defined, entities modeled, and data flowed like a well-organized library. But Alex, ever the curious developer, stared at the terminal and asked the question that had been on his mind:

“How do we actually see this bookshop? Where’s the UI?”

Emma smiled. “You’ve already seen a glimpse of it. Remember that app/ folder?”

Alex nodded. “Yeah, I saw a Fiori preview when I ran cds watch. But I didn’t quite get how it worked.”

Byte jumped in. “That’s the magic of CAP. It automatically serves any UI placed in the app/ folder. And when that UI is built with SAP Fiori Elements, it becomes deeply integrated with your CAP services.”

---

## Understanding the Fiori UI in CAP

Emma opened the CAP documentation on Fiori and walked Alex through the essentials.

“Fiori Elements is a UI framework that builds on top of SAPUI5. It uses metadata and annotations from your CAP service to generate UIs automatically.”

She showed him how the app/ folder could contain a Fiori app scaffolded using SAP Fiori tools. For example:

```
bookshop/
├── app/
│   └── bookshop-ui/
│       ├── webapp/
│       ├── manifest.json
│       └── ...
```

“This manifest.json is the heart of the Fiori app,” she explained. “It defines the data source, the main page, and how the UI should behave.”

Alex was amazed. “So I don’t need to write much UI code?”

“Exactly,” Byte said. “You define annotations in your CDS models or metadata extensions, and Fiori Elements takes care of the rest.”

---

✨ Example: Creating a List Report Page

Emma showed Alex a simple example. Suppose the CAP service exposes a Books entity. By adding this annotation in a .cds file:

```cds
annotate CatalogService.Books with {
  @UI: {
    lineItem: [
```
