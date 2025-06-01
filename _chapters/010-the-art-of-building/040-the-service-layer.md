---
layout: chapter
title: "The Service Layer"
---

Alex was on a roll. He had built entities, added mock data, tested services, and even sprinkled in some custom logic. But as he stared at his terminal, a new question bubbled up like a thought in a hot cup of coffee.

“Byte,” he asked, “we’ve been talking about services a lot. But what does it really mean to provide a service in CAP?”

Byte, ever the digital sage, gave a knowing blink.

---

🧠 **Byte Explains: What It Means to Provide a Service**

“In CAP,” Byte began, “providing a service means exposing your data and logic to the outside world—whether that’s a UI, another app, or an external system.”

Alex tilted his head. “So... like an API?”

“Exactly,” Byte nodded. “When you define a service in a .cds file, you’re saying: ‘Hey world, here’s what I’m offering.’ It’s like opening a shop window.”

“And the entities inside the service?”

“Those are your products. You can display them as-is, repackage them with projections, or keep some behind the counter. You’re the shopkeeper—you decide what’s on display.”

```cds
service CatalogService {
  entity Books as projection on my.Books;
}
```

“Voilà! You’ve just opened your bookstore to the world. No late fees, no overdue notices.”

---

👩‍💻 **Emma Joins the Conversation**

Just then, Emma strolled in, coffee in hand, catching the tail end of Byte’s analogy. “Talking about service provisioning?” she asked.

“Yeah,” Alex said. “Byte says it’s like opening a shop window.”

Emma smiled. “That’s a great metaphor. Think of your service as a contract. It defines what’s available, how it behaves, and what rules apply.”

Alex’s eyes lit up. “So when I write CatalogService, I’m saying: ‘Here’s the Books entity, ready to be used’?”

“Exactly,” Emma said. “And you can define multiple services for different audiences—like one for admins, another for customers. Each gets a tailored view.”

---

🛠️ **A New Requirement: Beyond CRUD**

Emma glanced at the whiteboard. “Hey, didn’t the product owner ask for a way to restock books manually?”  
Alex nodded. “Yeah, and also a report on top-selling books.”  
Byte lit up. “Perfect use case for actions and functions!”

```cds
service CatalogService {
  action restockBook(ID: UUID, amount: Integer);
  function topSellingBooks(): [Books];
  function getBookCount(): Integer; // Example: parameterless function
}
```

“Actions are like saying ‘restock this book now!’ and functions are like asking ‘what are the top sellers?’”  
Alex grinned. “So actions are bossy, and functions are curious?”  
“Exactly,” Emma said. “Just like you and Byte.”

---

📝 **Implementing the Logic**

Alex scratched his head. “Okay, I’ve defined these in my .cds file. But where do I actually write the logic for restockBook and topSellingBooks?”

Byte replied, “Great question! In CAP, you implement the logic for actions and functions in a JavaScript (or TypeScript) handler file. By convention, this file lives in your srv/ folder and is named after your service, like catalog-service.js.”

Emma added, “You register your handlers using the srv.on or srv.function methods. Here’s a simple example:”

```js
// File: srv/catalog-service.js
module.exports = (srv) => {
  // Action handler with parameters
  srv.on('restockBook', async (req) => {
    const { ID, amount } = req.data;
    await UPDATE('Books').set('stock +=', amount).where({ ID });
    return { ID, restocked: amount };
  });

  // Function handler with no parameters
  srv.on('getBookCount', async () => {
    const { count } = await SELECT.one`count(*) as count`.from('Books');
    return count;
  });

  // Function handler with parameters
  srv.on('topSellingBooks', async () => {
    const topBooks = await SELECT.from('Books').orderBy('sales desc').limit(5);
    return topBooks;
  });
};
```

Byte smiled. “Define the contract in CDS, implement the logic in JavaScript. That’s the CAP way!”

---

📝 **Consuming Actions and Functions**

Alex wondered, “How do I actually use these from a UI or API client?”

Byte explained, “You can call actions and functions via HTTP requests or from your Fiori/UI5 app. Here’s how:”

- **Calling an Action (with parameters):**
  - HTTP POST to `/catalog/restockBook`
  - Body: `{ "ID": "123", "amount": 10 }`
- **Calling a Function (with parameters):**
  - HTTP GET to `/catalog/topSellingBooks`
- **Calling a Parameterless Function:**
  - HTTP GET to `/catalog/getBookCount`

Alex asked, “So I can test these functions directly using test.http, right? Can you show me how that would look?”

Byte nodded, “Absolutely! Here’s how you’d write those requests in your test.http file for easy testing in VS Code:”

```
### Call Function: topSellingBooks
GET http://localhost:4004/catalog/topSellingBooks

### Call Parameterless Function: getBookCount
GET http://localhost:4004/catalog/getBookCount

### Call Function with Input Parameter: booksByAuthor
GET http://localhost:4004/catalog/booksByAuthor(author='J.K. Rowling')

### Call Function with Multiple Input Parameters: booksByAuthorAndYear
GET http://localhost:4004/catalog/booksByAuthorAndYear(author='J.K. Rowling',year=2007)
```

Byte smiled, “Just copy these into your test.http file, select a request, and click 'Send Request' in VS Code. You’ll see the results instantly!”

Emma added, “In Fiori Elements, actions appear as buttons, and functions can be triggered from the UI or used in analytics.”

---

## ☕ Alex’s Doubts: Can Functions Have Input Parameters?

As Alex sipped his coffee, another question popped up.

“Byte, can functions have input parameters too? Like, what if I want to search for books by author?”

Byte grinned, “Absolutely! Functions can take input parameters, just like actions. Here’s how you’d define and use one:”

```cds
service CatalogService {
  function booksByAuthor(author: String): [Books];
}
```

Emma explained, “Now, users can call this function and pass an author’s name as input. The function will return all books by that author.”

**Consuming the function:**
- HTTP GET to `/catalog/booksByAuthor(author='J.K. Rowling')`

**Implementing the logic:**
```js
srv.on('booksByAuthor', async (req) => {
  const { author } = req.data;
  const books = await SELECT.from('Books').where({ author });
  return books;
});
```

Byte added, “With input parameters, your functions become even more flexible. You can filter, search, or calculate based on user input—making your service truly interactive!”

---

## ☕ Alex’s Follow-up: What if There Are Multiple Input Parameters?

Alex, now more curious, asked, “What if I want to filter books by both author and year? Can a function have multiple input parameters?”

Byte nodded, “Of course! Just add more parameters to your function definition.”

```cds
service CatalogService {
  function booksByAuthorAndYear(author: String, year: Integer): [Books];
}
```

Emma explained, “Now, you can call the function with both parameters.”

**Consuming the function:**
- HTTP GET to `/catalog/booksByAuthorAndYear(author='J.K. Rowling',year=2007)`


**Implementing the logic:**
```js
srv.on('booksByAuthorAndYear', async (req) => {
  const { author, year } = req.data;
  const books = await SELECT.from('Books').where({ author, year });
  return books;
});
```

Byte smiled, “With multiple input parameters, your functions become even more powerful and flexible for all kinds of queries!”

---

🎯 **Wrapping Up**

Alex looked at his project with new eyes. The folders, the files—they weren’t just code. They were a carefully crafted interface between logic and the world.  
“Okay,” he said, cracking his knuckles. “Let’s make this service shine.”  
Byte winked. “And don’t forget to validate your inputs. CAP doesn’t like surprises.”
