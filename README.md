# AIpply (AI Auto-Apply)

A high-performance SaaS platform built with **Next.js 15** designed to automate the job application lifecycle—from discovery and analysis to AI-driven email outreach.

>This repository demonstrates a production-ready full-stack architecture, focusing on solving real-world challenges like serverless timeouts, database optimization, and asynchronous workflows.

---

## System Architecture & Design
Before writing a single line of code, I mapped out the system to ensure a scalable data flow.
- **High-Level Design:** Used **sequence diagrams** to define how API routes, background workers, and third-party services (OpenAI) interact.
- **Database Strategy:** Designed custom MongoDB schemas from scratch, prioritizing data and efficient relationships for a  SaaS application.

## Key Technical Implementations

### 1. Optimized Database Layer (MongoDB + Mongoose)
To handle the "cold start" and connection limit challenges in serverless environments:
- Implemented **connection caching** using a global variable to reuse the same Mongoose connection across multiple API requests.
- **Result:** Drastically reduced latency and prevented database connection spikes during high traffic.

### 2. Async Background Workers (Redis + BullMQ)
Next.js API routes have strict timeout limits. I offloaded "heavy" logic to dedicated workers to keep the platform responsive:
- **Job-Search Worker:** Handles complex scraping and API calls via webhooks.
- **Email-Compose Worker:** Generates personalized content using **OpenAI** and sends via **Postmark**.
- **The Why:** This ensures the UI stays snappy while expensive operations run safely in the background as separate processes.

### 3. Secure Auth & Payments
- **NextAuth + JWT:** Implemented a session-less auth strategy using Google OAuth and custom credentials.
- **Stripe Integration:** Managed subscription lifecycles, webhooks, and billing logic.

---

## 💻 Tech Stack

| Area | Technologies |
|------|----------------|
| **Backend** | Next.js API Routes, TypeScript, Node.js 20 |
| **Data & Cache** | MongoDB (Mongoose), Redis (IORedis) |
| **Async Queues** | BullMQ (Dedicated workers for job/email processing) |
| **Integrations** | OpenAI API, Stripe, Postmark, Google APIs |

---
