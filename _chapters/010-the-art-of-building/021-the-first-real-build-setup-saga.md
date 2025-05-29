---
layout: chapter
order: 21
title: "The First Real Build – The Setup Saga (npm init... or not?)"
---

Alex sat at his desk, eyes glued to the glowing screen. The Bookshop tutorial on Capire had him hooked.

“This looks awesome,” he muttered. “Clean structure, real-world use case… I’m doing this.”

He cracked his knuckles, opened the terminal, and typed with confidence:

```
npm init bookshop
```

A second passed. Then the terminal blinked back at him:

```
npm ERR! 404 Not Found - GET https://registry.npmjs.org/bookshop - Not found
```

“Wait… what?”

A familiar shimmer danced across his screen. Byte, his AI coding companion, materialized with a grin.

“Trying to conjure a bookstore with the wrong spell, huh?”

Alex groaned. “I followed the docs! I thought this was the command.”

“Ah, rookie mistake,” Byte said, floating lazily above the terminal. “That’s just a placeholder name. But hey, you’re not far off.”

Just then, Emma appeared, arms crossed, sipping a virtual espresso.

“Let me guess—you skipped the part about setting up your environment?”

Alex blinked. “There’s an environment?”

“Oh boy,” Byte chuckled. “Okay, let’s rewind. First things first—what are you using to code?”

“Uh… I was just going to use Notepad++?”

Emma nearly dropped her espresso.

“Nope. Nope. We’re not doing that. You want to build a CAPM app, you need Visual Studio Code. It’s like… the cockpit for your spaceship.”

“And it works offline,” Byte added. “Perfect for local development. Think airplane mode, but for coding.”

Minutes later, Alex had VS Code installed and running. Byte pointed him to the Extensions tab.

“Search for ‘SAP CDS Language Support’. It’ll make your life easier.”

“Syntax highlighting, code completion, even model previews,” Emma said. “It’s like giving your editor a sixth sense.”

Alex nodded. “Alright, IDE’s ready. Now what?”

“Now,” Byte said, floating closer, “we talk about the real engine behind all this—Node.js and npm.”

“I’ve heard of them,” Alex said. “Never really used them.”

Emma summoned a floating whiteboard and scribbled:

```
Node.js – JavaScript runtime
npm – Node’s package manager
```

“Without these,” she said, “you’re basically trying to bake a cake without an oven or ingredients.”

“And CAPM,” Byte added, “is the recipe.”

Alex grinned. “Alright, let’s bake.”

They guided him through installing Node.js. A few checks later, the terminal confirmed:

```
v18.19.0
9.6.7
```

“Nice,” Byte said. “Now let’s bring in the CAPM tools.”

Inside a new folder called `bookshop`, Alex ran:

```
npm install @sap/cds --save
```

The terminal buzzed with activity. Packages downloaded. Dependencies resolved.

Byte floated a little higher, arms wide.

“Now you’re in a good place to start your application creation journey.”

“Go ahead,” he said, eyes twinkling. “Run the command 
`npm init bookshop` now. Watch the magic.”

Alex typed:

```
npm init bookshop
```

And just like that—voilà—a folder structure bloomed in his project like a digital flower:

```
bookshop/
├── app/
├── db/
├── srv/
├── package.json
├── README.md
```

Alex’s eyes lit up. “Whoa. That’s… beautiful.”

He clicked through the folders, curiosity bubbling over.

“What’s all this? What goes where? I want to understand it all!”

Emma raised a hand, smiling.

“Easy, tiger. Let’s take a tea or coffee break first. Then I’ll walk you through it.”

“Trust me,” she added, “you’ll want a clear head for what’s coming next.”

Alex leaned back, grinning.

“Make mine a strong chai. I’m all in.”