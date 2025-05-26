---
layout: chapter
order: 30
title: "The Setup (Immediate Destruction of Confidence)"
---

Alex was in the zone. His bookstore app was shaping up, and for once, he wasn’t stuck in a sea of red error messages.

“Byte,” he said, “can we add some standard fields to the Books entity? Like createdBy, createdAt, modifiedBy, modifiedAt?”

Byte popped up with a grin. “Sure. But instead of typing those out every time, how about I show you a smarter way?”

Alex raised an eyebrow. “Smarter than copy-paste?”

“Much smarter. Ever heard of aspects?”

Alex shook his head. “Sounds like something from a sci-fi movie.”

Byte chuckled. “In CAP, aspects are like reusable traits. You define them once and plug them into any entity. Watch this.”

He projected a snippet into the air:

```cds
entity Books : managed {
  key ID : Integer;
  title  : String;
  stock  : Integer;
}
```

“And then,” Byte continued, “you just attach it like this:”

```cds
entity Books : managed {
  key ID : Integer;
  title  : String;
  stock  : Integer;
}
```

Alex blinked. “That’s it?”

“That’s it. And CAP even gives you a built-in managed aspect that does this automatically—plus it fills in those fields when you create or update records.”

Alex leaned back, impressed. “Okay, that’s cool. Are there other aspects like this?”

Byte’s eyes lit up. “Oh, you’re going to love this. Let me show you a few more.”

He snapped his fingers, and a virtual whiteboard appeared.
