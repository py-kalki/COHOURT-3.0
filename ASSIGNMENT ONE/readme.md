# 🚀 Pending — AI-Powered Customer Support System (MongoDB Edition)

> Build once. Scale forever.  
> AI-native, real-time, multi-tenant support infrastructure powered by MongoDB.

---

## 🧠 Overview

**Pending** is a next-generation customer support platform that combines:

- 🤖 AI-first response automation  
- 👨‍💻 Human agent escalation  
- ⚡ Real-time messaging  
- 🏢 Multi-tenant architecture  
- 📊 Intelligent analytics  

Now upgraded with **MongoDB**, enabling flexible schema design, faster iteration, and horizontal scalability.

---

## 🎯 Why MongoDB?

We moved from relational DB → MongoDB for:

- Flexible schema (AI + dynamic messages)
- Faster development cycles
- Better support for nested conversation data
- Horizontal scaling (sharding ready)
- Natural fit for chat + event-driven systems

---

## 🏗️ System Architecture

```

Frontend (React)
↓
Socket.io + REST API
↓
Backend (Node.js / Express)
↓
AI Engine + Decision Engine
↓
MongoDB + Redis

````

---

## ⚙️ Tech Stack

### Frontend
- React (Vite)
- Tailwind CSS
- Zustand
- Socket.io Client

### Backend
- Node.js + Express
- Socket.io
- MongoDB (Mongoose)
- JWT Authentication
- Redis (ioredis)
- AI Integration (Claude API)

---

## 🗄️ MongoDB Data Modeling (Production-Grade)

---

### 🏢 Tenant Collection

```js
{
  _id: ObjectId,
  name: "ShopEasy",
  plan: "pro",
  createdAt: Date
}
````

---

### 👤 User Collection

```js
{
  _id: ObjectId,
  name: "Abhishek",
  email: "user@email.com",
  password: "hashed",
  role: "customer" | "agent" | "admin",
  tenantId: ObjectId,
  isActive: true,
  createdAt: Date
}
```

---

### 🎫 Ticket Collection

```js
{
  _id: ObjectId,
  tenantId: ObjectId,
  customerId: ObjectId,
  assignedAgentId: ObjectId | null,

  status: "open" | "in_progress" | "resolved" | "closed",
  priority: "low" | "medium" | "high",

  lastMessageAt: Date,
  createdAt: Date,
  updatedAt: Date
}
```

---

### 💬 Message Collection

```js
{
  _id: ObjectId,
  ticketId: ObjectId,
  tenantId: ObjectId,

  senderId: ObjectId,
  senderType: "customer" | "agent" | "ai",

  content: "text message",
  isAI: true | false,

  createdAt: Date
}
```

---

### 🤖 AI Result Collection

```js
{
  _id: ObjectId,
  messageId: ObjectId,

  intent: "refund_request",
  emotion: "angry",
  confidence: 0.82,

  shouldEscalate: true,
  suggestedReply: "We’re sorry for the inconvenience...",

  createdAt: Date
}
```

---

## 🔥 Critical Indexing Strategy

```js
db.tickets.createIndex({ tenantId: 1, status: 1 })
db.messages.createIndex({ ticketId: 1, createdAt: 1 })
db.users.createIndex({ tenantId: 1, role: 1 })
```

---

## 🔐 Multi-Tenancy Enforcement

Every query MUST include:

```js
{ tenantId: user.tenantId }
```

❗ This is **non-negotiable** for security.

---

## ⚡ Real-Time Architecture

### Socket Rooms

```
user:{userId}
agent:{agentId}
tenant:{tenantId}
ticket:{ticketId}
```

---

## 🔄 Message Flow

```
User → Message
   ↓
AI Engine (analyze)
   ↓
Decision Engine
   ↓
AI reply OR Ticket created
   ↓
Agent assigned
   ↓
Real-time communication
```

---

## ⚡ Performance Strategy

### Redis Usage

* AI response caching
* Agent availability tracking
* Analytics caching
* Session store

---

### MongoDB Optimization

* Indexed queries
* Lean queries (`.lean()`)
* Pagination (cursor-based)
* Projection (select only needed fields)

---

## 🔁 Async Processing (Scalable)

Future upgrade:

```
Message → Queue → Worker → AI → Decision
```

Using:

* BullMQ + Redis

---

## 🔐 Security

* JWT Authentication
* Role-based access control
* Input validation (Zod/Joi)
* Rate limiting
* Audit logs

---

## 📦 Project Structure

```
server/
 ├── models/
 │    ├── user.model.js
 │    ├── ticket.model.js
 │    ├── message.model.js
 │    └── tenant.model.js
 ├── routes/
 ├── services/
 ├── socket/
 ├── middleware/
 ├── lib/
 └── utils/
```

---

## 🚀 Getting Started

### Backend

```bash
cd server
npm install
```

Create `.env`:

```
MONGO_URI=
JWT_SECRET=
REDIS_URL=
AI_API_KEY=
```

Run:

```bash
npm run dev
```

---

### Frontend

```bash
cd client
npm install
npm run dev
```

---

## 📊 Future Enhancements

* MongoDB Change Streams (real-time DB triggers)
* Sharding for massive scale
* AI conversation memory layer
* Vector search (AI semantic understanding)
* Multi-channel support (Email, WhatsApp)

---

## 💰 Monetization

* Free → Limited usage
* Pro → Full AI + analytics
* Enterprise → Custom infra + SLA

---

## 📏 Success Metrics

* AI Resolution Rate > 60%
* Response Time < 2s
* CSAT > 90%
* Agent Load Reduction > 40%

---

## 🧨 What Makes This Powerful?

* MongoDB handles dynamic AI data effortlessly
* Real-time system built from day one
* AI + human workflow deeply integrated
* Scales horizontally without redesign

---

## 🚀 Final Thought

> This is not just a project.
> This is a scalable AI-powered support infrastructure.
