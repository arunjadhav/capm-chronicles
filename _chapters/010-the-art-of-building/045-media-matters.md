---
layout: chapter
title: "Media Matters – Making Your Files First-Class Citizens"
---

Later that day, the UX team dropped by. “Can we show book covers in the app? Maybe even let users download sample chapters?”

Alex turned to Byte. “Can CAP do that?”

Byte grinned, “Oh, absolutely. Time to talk about serving media data!”

---

Emma leaned in, her eyes bright. “Media handling in CAP is really powerful. You can store images, PDFs, or any binary content and serve them through your service.”

Byte nodded. “Let’s start with the basics. You define an entity for your media, like this:”

```cds
entity BookCovers {
  key ID      : UUID;
  content     : LargeBinary @Core.MediaType: 'image/png';
  filename    : String;
}
```

Alex studied the code. “So the `content` field holds the image, and `@Core.MediaType` tells CAP it’s a PNG?”

“Exactly!” Byte replied. “CAP will automatically handle the right HTTP headers for uploads and downloads.”

---

Emma explained, “To upload a book cover, you POST to `/catalog/BookCovers` with the image as the body and set the right Content-Type header.”

Alex looked a bit puzzled. “But how would I actually do that? I’ve only ever uploaded JSON data.”

Byte grinned, “It’s easier than you think! Let’s walk through it step by step.”

Emma continued, “Imagine you’re using Postman, VS Code REST Client, or even curl. Here’s what you’d do:”

- **Step 1:** Open your favorite API tool (like Postman, VS Code REST Client, or even curl).
- **Step 2:** Set the request to POST and the URL to `/catalog/BookCovers`.
- **Step 3:** In the headers, add `Content-Type: image/png`.
- **Step 4:** In the body, select 'binary' and upload your image file.
- **Step 5:** (Optional) Add a `filename` property in the JSON part if your tool supports multipart/form-data.

Byte added, “Or, if you’re a command-line fan, here’s how you’d do it with curl:”

Byte added, “Or, if you’re testing locally, you can use a test.http file to make this even easier. Here’s how your request would look:”

**test.http example:**
```
### Upload a Book Cover (PNG)
POST http://localhost:4004/catalog/BookCovers
Content-Type: image/png

< ./cover.png
```

Byte smiled, “CAP will store the image in the `content` field and generate an ID. You can also send the filename as a property.”

Alex was curious. “How do I get the image back?”

Byte smiled. “Just GET `/catalog/BookCovers(ID)` and CAP will stream the image with the correct media type. You can also download it directly from the browser or a UI5 app.”

Emma replied, “It’s just as simple! Here’s how you can do it:”

- **Step 1:** Open your browser or API tool (like Postman, VS Code REST Client, or curl).
- **Step 2:** Make a GET request to `/catalog/BookCovers(ID)`, replacing `ID` with the actual ID of your uploaded image.
- **Step 3:** The response will be the binary image data, and the `Content-Type` header will be set to `image/png`.
- **Step 4:** In a browser, the image will display directly. In an API tool, you can save the file to disk.

Byte added, "Here’s how your request would look in test.http fiel for local testing:”

**test.http example:**
```
### Download a Book Cover by ID
GET http://localhost:4004/catalog/BookCovers/{{bookCoverId}}
```

Emma smiled, “Just replace `{{bookCoverId}}` with the actual ID, select the request in VS Code, and click 'Send Request'. Your image will be downloaded or previewed right in the editor!”

Emma smiled, “This way, you can easily preview or download any media file stored in your CAP service!”

Emma continued, “You can use the same approach for sample chapters, PDFs, or audio files. Just change the `@Core.MediaType` annotation.”

```cds
entity SampleChapters {
  key ID      : UUID;
  content     : LargeBinary @Core.MediaType: 'application/pdf';
  filename    : String;
}
```

---

Alex, always thinking ahead, asked, “Do I need to write any special logic for uploads or downloads?”

Byte reassured him, “CAP handles most of it for you! But if you want to add checks—like file size limits or allowed types—you can add handlers in your service JS file.”

```js
module.exports = (srv) => {
  srv.before('CREATE', 'BookCovers', (req) => {
    if (req.data.content && req.data.content.length > 5 * 1024 * 1024) {
      req.reject(400, 'File too large!');
    }
  });
};
```

Emma added, “You can also check file types, scan for viruses, or log uploads. CAP gives you the hooks.”

---

Maya from UX, who had been listening, asked, “Will this work in Fiori Elements?”

Emma nodded. “Absolutely! Media fields are recognized automatically. You can show images, preview PDFs, or let users download files—all out of the box.”

Alex grinned. “So we can build a digital library, with covers, chapters, and maybe even author interviews?”

Byte winked. “You got it. CAP makes media handling seamless—and stylish.”

---

🎯 **Wrapping Up**

Alex looked at his project with new eyes. The folders, the files—they weren’t just code. They were a carefully crafted interface between logic and the world.

“Okay,” he said, cracking his knuckles. “Let’s make this service shine—with images, stories, and all!”

Byte winked. “And remember, with CAP, your data isn’t just numbers and text—it’s an experience.”
