# 📬 go-mailpool

A **lightweight, rate-limited email job system written in Go (Golang)** — built to send thousands of emails safely without hitting SMTP or Mailtrap limits.

---

## 🚀 Overview

`go-mailpool` helps you:
- Fetch user data from MongoDB  
- Automatically detect missing Aadhaar (or any specific field)  
- Send reminder emails via Gmail / Mailtrap / any SMTP server  
- Avoid email throttling using **concurrent worker pools**  
- Schedule jobs using **cron-style intervals**

Built with ❤️ in Go — focusing on simplicity, reliability, and scalability.

---

## 🧱 Architecture

```text
+-------------+
|   CRON JOB  | --> periodically triggers UserJob()
+-------------+
       ↓
+-------------+
| EMAIL QUEUE | --> buffered Go channel
+-------------+
       ↓
+---------------------------+
| WORKER POOL (goroutines)  |
| sends emails concurrently  |
| within safe rate limits    |
+---------------------------+
       ↓
+----------------+
| SMTP Provider  |
| (Gmail, etc.)  |
+----------------+
