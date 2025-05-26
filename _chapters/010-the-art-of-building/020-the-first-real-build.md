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

“Whoa,” Alex whispered. “It created everything.”

Byte smirked. “Welcome to CAPM.”

Feeling bold, Alex ran:

```
cds run
```

Boom. Error.

💥 ERROR: No models found.

Emma peeked over her monitor. “You forgot the schema, didn’t you?”

Alex groaned. “Yup. Wait—what exactly is a schema file?”

Emma smiled. “It’s where you define your data model. Think of it like the blueprint for your database—entities, fields, relationships. CAP reads it to generate the backend.”

With Byte’s help, he created a new file: db/schema.cds.

```
// db/schema.cds
namespace my.bookshop;

entity Books {
  key ID: Integer;
  title: String;
  stock: Integer;
  author: Association to Authors;
}

entity Authors {
  key ID: Integer;
  name: String;
}
```

📁 Folder structure now:
```
bookshop/
├── app/
├── db/
│   └── schema.cds
├── srv/
├── package.json
└── README.md
```

He tries cds run on terminal again. Another error.

💥 ERROR: Missing service definitions!

Alex sighed. “Okay, what’s a service file then?”

Emma leaned over. “It’s how you expose your data model. You define which entities are available to the outside world—like APIs. CAP uses it to generate endpoints and even the Fiori preview.”

Byte chimed in, “Time to define your services. Create two files in the srv/ folder.”

In srv/admin-service.cds:

```
// srv/admin-service.cds
using { my.bookshop as my } from '../db/schema';

service AdminService {
  entity Books as projection on my.Books;
  entity Authors as projection on my.Authors;
}
```

And in srv/cat-service.cds:

```
// srv/cat-service.cds
using { my.bookshop as my } from '../db/schema';

service CatalogService {
  entity Books as projection on my.Books;
}
```
📁 Folder structure now:
```
bookshop/
├── app/
├── db/
│   └── schema.cds
├── srv/
│   ├── admin-service.cds
│   └── cat-service.cds
├── package.json
└── README.md
```

He ran the app again:

```
cds run
```

This time, success.

This time, the terminal lit up with a new kind of magic:

```
🎉 [cds] - loaded model from 3 file(s)...
using sqlite database...
serving CatalogService at /catalog... AdminService at /admin
[cds] - server listening on http://localhost:4004
```

He blinked. “Wait… SQLite?”

Byte popped in. “Yep. CAPM uses SQLite by default for local development. No setup, no database server, no config files. It just works.”

“So I’m running a full backend with a database… and I didn’t even install a database?”

“Exactly. It’s lightweight, file-based, and perfect for prototyping. You can even inspect the data if you want—it’s all stored in a local .sqlite file.”

Alex nodded slowly. “Okay, that’s actually pretty cool.”

Then he noticed the link in the terminal: http://localhost:4004

He clicked it.

And that’s when it hit him.

A full Fiori preview opened in his browser. Tables. Buttons. Filters. A clean, responsive UI—automatically generated from his service definitions.

“I didn’t write a single line of frontend code,” he whispered.

Byte grinned. “You didn’t have to. CAPM gives you a Fiori preview out of the box. It reads your service metadata and builds a working UI for you.”

Alex clicked around, stunned. “This is… amazing. I can test my services visually, right here.”

“Exactly. It’s not just backend—it’s full-stack scaffolding. And you’re still on localhost.”

But something was missing.

“I’ve got services,” Alex said, “but where’s the data? It’s like opening a bookstore with no books.”

Byte, ever ready with a metaphor, replied, “Exactly. You’ve built the shelves. Now let’s stock them.”

“Can I add some mock data?”

“Of course. Just drop a couple of .csv files into db/data/. Want me to generate them?”

“Yes, please.”

Byte conjured up two files like a magician pulling rabbits from a repo:

📄 db/data/my.bookshop-Authors.csv

```
ID;name  
1;J.K. Rowling  
2;George R.R. Martin  
3;Haruki Murakami  
```

📄 db/data/my.bookshop-Books.csv

```
ID;title;stock;author_ID  
101;Harry Potter and the Philosopher's Stone;100;1  
102;A Game of Thrones;50;2  
103;Kafka on the Shore;75;3  
```

Alex dropped them into place and restarted the app. Then he opened the Fiori preview.

A clean, responsive UI appeared—tables for Books and Authors, complete with Create, Read, Update, and Delete operations.

“WOAH. It’s all there!” he said, eyes wide.

Byte nodded. “CAPM does the heavy lifting. You just need to speak its language.”

---

## Automating the Workflow

Alex was feeling good. Confident, even. But then he made a small change in the code and had to restart the server manually.

“Byte, do I have to restart every time I change something?”

Byte rolled its virtual eyes. “Nope. Use this instead:”

```
cds watch
```

Alex tried it. He made a change, hit save, and watched the server restart automatically.

“This is amazing,” he whispered.

---

## Testing Like a Pro

Emma, overhearing the excitement, leaned over. “You know you can test your services without even opening the browser, right?”

Alex blinked. “How?”

Byte answered before she could. “With .http files. Already set one up for you.”

📄 test.http

```
### Get all books  
GET http://localhost:4004/catalog/Books  

### Get all authors  
GET http://localhost:4004/admin/Authors  
```

Alex clicked “Send Request.” JSON responses popped up instantly.

“I feel like a real backend developer now.”

Emma grinned. “You are.”

Alex leaned back in his chair, proud. “Okay. Let’s build this bookstore.”

---

## The Realization: Fast Inner Loops

As he worked, Alex noticed something. The terminal refreshed automatically. The Fiori preview updated in real time. The .http tests returned fresh data with every change.

No redeployments. No waiting. No cloud connection needed.

“Emma,” he said, eyes still on the screen, “I think I finally get it.”

She looked up. “Get what?”

“Why they call it fast inner loops.”

Emma smiled. “Ah. That moment.”

“I’ve been coding, testing, and seeing results in seconds. No pipelines. No delays. Just… build, save, test. It’s like flying in airplane mode.”

“Exactly,” she nodded. “CAP is designed for that. You work locally, iterate fast, and only go hybrid or cloud when you’re ready. It’s not just about speed—it’s about flow.”

Alex nodded slowly, the pieces clicking into place.

“So this is what they meant when they said CAPM makes development faster. It’s not just the tools—it’s the experience.”

Emma raised her coffee in a toast. “Welcome to the loop.”

Alex raised his mug in return.

“Let’s build something amazing.”

---
