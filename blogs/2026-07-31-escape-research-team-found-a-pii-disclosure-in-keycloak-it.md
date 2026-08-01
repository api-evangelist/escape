---
title: "Escape Research team found a PII disclosure in Keycloak. It's now CVE-2026-17059."
url: "https://escape.tech/blog/escape-research-pii-disclosure-keycloak-cve-2026-17059/"
date: "2026-07-31"
author: "Enzo Mongin"
feed_url: "https://escape.tech/blog/feed/"
---
Keycloak filters its main users list so a restricted admin sees nothing. The endpoint that lists a role's members skips that filter and hands the same account everyone's email and name. Escape research found it, reported it, and it's now tracked as CVE-2026-17059.
