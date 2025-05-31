---
layout: chapter
title: "The First Real Build – The Schema Chronicles (In a Nutshell)"
---

Alex returned from his tea break, eyes gleaming with excitement.

“Okay, I’m ready. Let’s build something real!”

Emma smiled warmly.

“Love the energy. But before we start writing code, let’s fire up the engine.”

“Engine?” Alex asked.

“Run `cds watch` in your terminal,” she said, pointing.

Alex typed it in. The terminal came alive.

> “This command watches your project for changes,” Emma explained. “Every time you save a file, it automatically restarts the server and redeploys your app.”

“So I don’t have to restart anything manually?” Alex asked.

“Exactly,” Byte chimed in. “Now, let’s feed it something to watch.”

## Step 1: Define the Data Model

Emma guided Alex to the `db/` folder.

> “This is where we define your data model. Let’s create a file called `schema.cds`.”

Alex created the file, and Byte floated in with a glowing code snippet.

 “Here’s a simple entity to get us started.”
```cds
namespace my.bookshop;

entity Books {
  key ID: Integer;
  title: String;
  stock: Integer;
  author_ID: Integer;
}

entity Authors {
  key ID: Integer;
  name: String;
}
```

---

Emma smiled. “It’s where you define your data model. Think of it like the blueprint for your database—entities, fields, relationships. CAP reads it to generate the backend.”

He saved the file—and the terminal reacted instantly:

```
[cds] - loaded model from 1 file(s):

  db\schema.cds

[cds] - connect using bindings from: { registry: '~/.cds-services.json' }
[cds] - connect to db > sqlite { url: ':memory:' }
/> successfully deployed to in-memory database. 


[cds] - server listening on { url: 'http://localhost:4004' }
[cds] - server launched in: 790.725ms
[cds] - [ terminate with ^C ]


    No service definitions found in loaded models.
    Waiting for some to arrive...
```

“Whoa,” Alex said. “It just… worked?”

“Yup,” Byte said. “CAPM uses an in-memory SQLite database by default.”

Emma leaned in, drawing a quick sketch in the air.

> “Think of it like a mock version of your real database—super fast, temporary, and perfect for development. It’s like using a whiteboard instead of carving into stone.”

“So it’s not permanent?” Alex asked.

“Right,” Byte nodded. “It resets every time you restart. But it drastically speeds up development. It’s not meant for production, but it’s perfect for mocking your target database—like SAP HANA—while you build.”

> “And the best part?” Emma added. “You don’t have to configure anything. It just works.”

“You’ve just exposed your data model,” Byte said. “Now open your browser and go to http://localhost:4004.”
![image](https://github.com/user-attachments/assets/8aa569db-f2ad-4622-9e75-8beb3c173dd8)

Alex grinned and whispered, "Thank you, CAPM, for making local testing so easy."

### 📁 Updated Folder Structure

```
bookshop/
├── app/
├── db/
│   └── schema.cds
├── srv/
├── package.json
├── README.md
```

## Step 2: Provide Services

But then the terminal added:

> No service definitions found in loaded models.
> Waiting for some to arrive...

“That’s CAPM’s way of saying: ‘Cool bookshelf, but how do I let people browse it?’” Emma said.

“Let’s define two services,” Byte suggested. “One for admins to manage books, and one for users to browse them.”

Emma guided Alex to the `srv/` folder.

> “Create two files: `admin-service.cds` and `catalog-service.cds`.”

Alex did, and Byte helped with the code.
admin-service.cds
```cds
using { my.bookshop as my } from '../db/schema';

service AdminService {
  entity Books as projection on my.Books;
  entity Authors as projection on my.Authors;
}
```

catalog-service.cds
```cds
using { my.bookshop as my } from '../db/schema';

service CatalogService {
  entity Books as projection on my.Books;
  entity Authors as projection on my.Authors;
}
```


---

> “So this is like creating two doors to the same bookshelf,” Alex said. “One for staff, one for customers?”

“Exactly!” Emma beamed. “You’re getting it.”

Alex saved both files. The terminal lit up again:

```
[cds] - serving AdminService { at: '/odata/v4/admin' }
[cds] - serving CatalogService { at: '/browse' }
[cds] - server listening on { url: 'http://localhost:4004' }
```

“You’ve just exposed your data as OData services,” Byte said. “Now open your browser and go to http://localhost:4004.”
![image](https://github.com/user-attachments/assets/e134ae3b-94f4-4cee-babf-b7acae4acf1f)

Alex did—and his jaw dropped.

> “Whoa… what is this?”

“That,” Emma said proudly, “is the Fiori Preview. CAPM gives you a built-in UI to test your services. Click around—you can explore your data, test endpoints, even simulate queries.”

“This is amazing,” Alex said. “I didn’t even build a UI, and it’s already working!”

“CAPM gives you a generic UI for free,” Byte said. “Perfect for testing and exploring your services.”

### 📁 Final Folder Structure for Part 2

```
bookshop/
├── app/
├── db/
│   └── schema.cds
├── srv/
│   ├── admin-service.cds
│   └── catalog-service.cds
├── package.json
├── README.md
```

Emma leaned back, satisfied.

> “You’ve now completed the core CAPM flow: model, deploy, serve, and preview.”

---
![image](https://github.com/user-attachments/assets/447ccabd-9062-4a1f-8b6a-0228c66ea08b)

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
