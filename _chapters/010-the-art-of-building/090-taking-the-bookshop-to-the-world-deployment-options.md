---
layout: chapter
order: 90
title: "Taking the Bookshop to the World — Deployment Options"
---

As the Bookshop app neared completion, Alex asked:

Alex: “So… how do we actually deploy this?”

Emma smiled. “CAP gives you several options, depending on where you want to run it.”

---

## 🚀 SAP BTP (Business Technology Platform)
Emma: “This is the go-to for enterprise apps.”
• Uses SAP HANA and Cloud Foundry or Kyma
• Supports MTA or cf push for deployment
• Best for full SAP integration

---

## 🧪 Local Deployment
Byte: “You’ve already been doing this.”
• Run with cds watch
• Uses SQLite or local HANA
• Great for development and testing

---

## 🐳 Docker & Containers
Emma: “Want portability? Use Docker.”
• Package your app in a container
• Deploy anywhere: Kubernetes, Kyma, etc.

---

## 🌐 Third-Party Clouds
Alex: “Can I use AWS or Azure?”
Byte: “Sure!”
• Use PostgreSQL, MySQL, or managed HANA
• Deploy like any Node.js app

---

## 🛳️ Static UI Hosting
Emma: “If your UI is separate, host it on Netlify, Firebase, or SAP’s HTML5 repo.”

---

Alex: “So CAP lets me deploy wherever I want — from SAP BTP to my own cloud.”
