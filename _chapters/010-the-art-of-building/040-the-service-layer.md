---
layout: chapter
order: 40
title: "The Service Layer"
---

Alex was on a roll. He had built entities, added mock data, tested services, and even sprinkled in some custom logic. But as he stared at his terminal, a new question bubbled up like a thought in a hot cup of coffee.

“Byte,” he asked, “we’ve been talking about services a lot. But what does it really mean to provide a service in CAP?”

Byte, ever the digital sage, gave a knowing blink.

“Ah, the philosophical phase of development. Let’s unpack that.”

________________________________________

🧠 Byte Explains: What It Means to Provide a Service

“In CAP,” Byte began, “providing a service means exposing your data and logic to the outside world—whether that’s a UI, another app, or an external system.”
Alex tilted his head.
“So... like an API?”
“Exactly,” Byte nodded. “When you define a service in a .cds file, you’re saying: ‘Hey world, here’s what I’m offering.’ It’s like opening a shop window.”
“And the entities inside the service?”
“Those are your products. You can display them as-is, repackage them with projections, or keep some behind the counter. You’re the shopkeeper—you decide what’s on display.”

```cds
service CatalogService {
  entity Books as projection on my.Books;
}
```

“Voilà! You’ve just opened your bookstore to the world. No late fees, no overdue notices.”

________________________________________

👩‍💻 Emma Joins the Conversation

Just then, Emma strolled in, coffee in hand, catching the tail end of Byte’s analogy.
“Talking about service provisioning?” she asked.
“Yeah,” Alex said. “Byte says it’s like opening a shop window.”
Emma smiled.
“That’s a great metaphor. Think of your service as a contract. It defines what’s available, how it behaves, and what rules apply.”
Alex’s eyes lit up.
“So when I write CatalogService, I’m saying: ‘Here’s the Books entity, ready to be used’?”
“Exactly,” Emma said. “And you can define multiple services for different audiences—like one for admins, another for customers. Each gets a tailored view.”

________________________________________

🧪 A Bug Appears: The Input Validation Moment

Just as Alex was about to test his service, an error popped up in the console.
“Hmm… it says ‘title is mandatory’—but I did send a title… oh wait, I didn’t.”
Byte chuckled.
“Welcome to the world of input validation. CAP is like a very picky maître d’. If your data doesn’t meet the dress code, it’s not getting in.”

```cds
entity Books {
  key ID     : UUID;
  title      : String(100) @mandatory;
  stock      : Integer     @assert.range: [0, 999];
}
```

Here, title is mandatory, and stock must be between 0 and 999. Try sending a book with no title and -5 stock, and CAP will politely slam the door in your face.”
Alex laughed.
“So CAP is basically my mom when I tried to wear flip-flops to a wedding.”

________________________________________

🛠️ A New Requirement: Beyond CRUD

Emma glanced at the whiteboard.
“Hey, didn’t the product owner ask for a way to restock books manually?”
Alex nodded.
“Yeah, and also a report on top-selling books.”
Byte lit up.
“Perfect use case for actions and functions!”

```cds
service CatalogService {
  action restockBook(ID: UUID, amount: Integer);
  function topSellingBooks(): [Books];
}
```

“Actions are like saying ‘restock this book now!’ and functions are like asking ‘what are the top sellers?’”
Alex grinned.
“So actions are bossy, and functions are curious?”
“Exactly,” Emma said. “Just like you and Byte.”
________________________________________

📝 Where Do You Implement Actions and Functions?

Alex scratched his head. “Okay, I’ve defined these in my .cds file. But where do I actually write the logic for restockBook and topSellingBooks?”

Byte replied, “Great question! In CAP, you implement the logic for actions and functions in a JavaScript (or TypeScript) handler file. By convention, this file lives in your `srv/` folder and is named after your service, like `catalog-service.js`.”

Emma added, “You register your handlers using the `srv.on` or `srv.function` methods. Here’s a simple example:”

```js
// File: srv/catalog-service.js
module.exports = (srv) => {
  // Action handler
  srv.on('restockBook', async (req) => {
    const { ID, amount } = req.data;
    // Your logic to update the stock for the book with the given ID
    // For example:
    await UPDATE('Books').set('stock +=', amount).where({ ID });
    return { ID, restocked: amount };
  });

  // Function handler
  srv.on('topSellingBooks', async (req) => {
    // Your logic to fetch top-selling books
    const topBooks = await SELECT.from('Books').orderBy('sales desc').limit(5);
    return topBooks;
  });
};
```

Byte smiled. “Define the contract in CDS, implement the logic in JavaScript. That’s the CAP way!”

________________________________________

🖼️ A Design Sprint: Serving Media

Later that day, the UX team dropped by.
“Can we show book covers in the app? Maybe even let users download sample chapters?”
Alex turned to Byte.
“Can CAP do that?”
“Oh, absolutely,” Byte said. “Time to talk about serving media data.”

```cds
entity BookCovers {
  key ID     : UUID;
  content    : LargeBinary @Core.MediaType: 'image/png';
  filename   : String;
}
```

“With this setup, you can upload, stream, and download media files like a pro. CAP handles the heavy lifting.”
Alex’s eyes widened.
“So I could build a digital library with book covers and sample chapters?”
“Absolutely,” Byte said. “CAP makes it seamless. And stylish.”

________________________________________

🎯 Wrapping Up

Alex looked at his project with new eyes. The folders, the files—they weren’t just code. They were a carefully crafted interface between logic and the world.
“Okay,” he said, cracking his knuckles. “Let’s make this service shine.”
Byte winked.
“And don’t forget to validate your inputs. CAP doesn’t like surprises.”
