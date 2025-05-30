---
layout: chapter
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
      { value: ID },
      { value: title },
      { value: author.name }
    ]
  }
};
```

Fiori Elements would automatically generate a List Report Page showing a table of books with their ID, title, and author.

“It’s like declarative UI,” Alex said. “I describe what I want, and Fiori builds it.”

Emma nodded. “And it’s enterprise-ready out of the box — responsive, accessible, and SAP-compliant.”

---

🧭 But What If You Want More Control?

Alex, still curious, asked, “What if I want to build something more custom? Like a modern, interactive UI with animations or a different design system?”

Byte smiled. “That’s where React and Vue come in. CAP doesn’t lock you in.”

He explained that while Fiori is the default and deeply integrated option, developers can use any frontend framework. For example:

- React: Use create-react-app, build your app, and place it in app/react-ui/. Use a proxy to connect to CAP’s OData services.
- Vue: Use vite or vue-cli to scaffold a Vue app, then serve it similarly.

Alex appreciated the flexibility.

“So Fiori is great when I want to move fast and stay close to SAP standards. But if I want full creative freedom, I can go with React or Vue.”

“Exactly,” Emma said. “Fiori is the express train. React and Vue are scenic routes — more work, but more control.”

---

🧩 Wrapping Up

By the end of the day, Alex had a clear picture:

- Fiori Elements: Best for SAP-aligned apps, fast to build, powered by annotations.
- React/Vue: Great for custom UIs, more flexible, but requires manual integration.

He looked at the app/ folder with new eyes.

“It’s not just a folder,” he said. “It’s the window to the Bookshop.”

Emma smiled. “And now you know how to open it — with Fiori, or with your own brush.”
