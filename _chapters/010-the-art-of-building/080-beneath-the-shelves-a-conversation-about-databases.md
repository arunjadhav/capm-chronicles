---
layout: chapter
order: 80
title: "Beneath the Shelves — A Conversation About Databases"
---

> *"The right database is like the right foundation for a building — invisible, but everything depends on it."*

---

The sun was setting outside the office window, casting a warm glow over the whiteboard filled with entity diagrams and service definitions. Alex leaned back in his chair, a thoughtful look on his face.

**Alex:**
> So far, we’ve been using SQLite for our Bookshop app. It’s been smooth, but… is that what we’d use in production too?

Emma looked up from her laptop and smiled.

**Emma:**
> Great question. SQLite is perfect for development — it’s lightweight, file-based, and requires zero setup. But for production? We’ve got options.

Byte, who had been quietly sipping virtual coffee, perked up.

**Byte:**
> Let’s explore them! CAP supports multiple databases, and switching between them is easier than you think.

---

## 🧑‍🔬 SQLite — The Developer’s Playground

**Emma:**
> Let’s start with what you already know — SQLite. It’s the default in CAP. You don’t even need to configure it explicitly, but here’s what it looks like in `package.json` or `.cdsrc.json`.

**Alex:**
> So that’s why it just worked when I ran `cds deploy`!

**Byte:**
> Exactly. It stores data in a local `.sqlite` file. Great for prototyping, but not for scaling.

```json
"cds": {
  "requires": {
    "db": {
      "kind": "sqlite",
      "model": ["db"]
    }
  }
}
```

---

## 🚀 SAP HANA — The Enterprise Powerhouse

**Emma:**
> Now, let’s talk about SAP HANA. It’s a beast — in a good way. It’s in-memory, column-oriented, and designed for high performance.

**Alex:**
> Sounds expensive…

**Byte:**
> Not just that. It’s powerful for sure, but with great power comes… you know the rest. Let’s look at how you’d configure it.

**Emma:**
> Right. You’d typically use it in larger, more critical applications. Here’s a basic setup:

```json
"cds": {
  "requires": {
    "db": {
      "kind": "hana",
      "model": ["db"]
    }
  }
}
```

---

## ☁️ PostgreSQL — The Open-Source Hero

**Emma:**
> PostgreSQL is another fantastic option. It’s open-source, highly stable, and has a strong community backing it.

**Alex:**
> And it’s not just for developers, right?

**Byte:**
> Exactly. It’s versatile. You can use it for everything from simple apps to complex, data-driven websites. Configuration example? Here you go:

```json
"cds": {
  "requires": {
    "db": {
      "kind": "postgresql",
      "model": ["db"]
    }
  }
}
```

---

## Conclusion

**Emma:**
> To wrap up, your choice of database in CAP depends on your specific needs — development speed, performance, scalability, or cost.

**Alex:**
> Thanks, Emma and Byte. This was enlightening!
