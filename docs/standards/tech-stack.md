---
layout: default
title: Tech Stack
parent: Standards
---

# Tech Stack & Infrastructure

## Approved Tools

We use a specific set of tools to keep collaboration smooth.

| Category | Tool | Scope |
|----------|------|-------|
| **Design** | Figma | UI/UX Design (Company account) |
| **Code** | GitHub | Host code & CI/CD |
| **Planning** | Zoho Sprints | Project management & Backlog |
| **Docs** | Eraser.io / VitePress | Architecture flows & User guides |

## Infrastructure

We host our services on **Hostinger VPS**.

- **Containerization**: 100% Docker & Docker Compose.
- **Service Management**: Containers use `restart: always`.
- **Secrets**: Currently managed manually on the VPS (migration planned).
- **Access**: Restricted to repository owners.
