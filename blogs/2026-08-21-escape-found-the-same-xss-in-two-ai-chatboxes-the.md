---
title: "Escape found the same XSS in two AI chatboxes. The vulnerability was in the Markdown renderer."
url: "https://escape.tech/blog/escape-found-the-same-vulnerability-in-two-ai-chatboxes/"
date: "2026-08-21"
author: "Gwendal Mognier"
feed_url: "https://escape.tech/blog/feed/"
---
Weeks apart, at two unrelated companies, Escape's AI pentesting agent found the same stored XSS. Both had shipped a customer-facing chat where the model emits Markdown and the frontend renders it with raw HTML enabled and no sanitizer, so anything the model can be made to say executes
