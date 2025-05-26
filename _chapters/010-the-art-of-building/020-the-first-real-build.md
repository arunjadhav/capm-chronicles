---
layout: chapter
order: 20
title: "The First Real Build"
---

The city outside buzzed with life. Inside, Alex was locked in a battle with his terminal.

He had taken Emma’s advice and decided to dive into SAP CAPM. Full of hope, he typed:

```
cds init bookshop
```

Nothing happened.

“Byte,” he muttered, summoning his AI assistant, “what am I missing?”

Byte blinked into view. “Everything. You haven’t installed CAPM yet.”

Alex sighed. “Of course.”

Byte, ever the helpful sass machine, replied, “Run this to install the CAPM CLI globally:”

```
npm install -g @sap/cds
```

“And while you’re at it, install these VS Code extensions. Trust me, your future self will thank you.”

- SAP CDS Language Support
- SAP Fiori Tools
- Prettier
- XML Tools

Alex followed the instructions, installed the tools, and tried again:

```
cds init bookshop
```

This time, magic. A folder structure appeared like a gift from the coding gods.

```
bookshop/
├── app/
├── db/
├── srv/
├── package.json
└── README.md
```
