# Software Architecture Document (SAD)
## Project: Personal Learning Coach Agent

---

## 1. Overview

The Personal Learning Coach Agent is an AI-powered assistant designed to help individuals stay on track with their learning goals. It provides personalized learning paths, resource suggestions, progress tracking, and motivational nudges.

---

## 2. Architecture Overview

### 2.1 High-Level Components

- **Frontend (React + TypeScript)**: User interface to interact with the agent.
- **Backend (.NET 8 Web API)**: Handles API requests, user data, and analytics.
- **AI Agent (Python or Azure Function with LangChain/LLM)**: Core logic for planning, recommendation, and interaction.
- **Vector DB (Pinecone / Qdrant / Azure Cognitive Search)**: For storing and querying learning content contextually.
- **Database (PostgreSQL / SQL Server)**: For storing user profiles, goals, progress, preferences.
- **Authentication (Azure AD B2C / Auth0)**: User management and security.

---

## 3. System Architecture Diagram
```
+-------------------------+
|     React Frontend      |
|  (Learning Dashboard)   |
+-----------+-------------+
            |
            v
+-----------+-------------+
|    .NET 8 Web API       |
| (User Auth, Profile,    |
|  Goal Management)       |
+-----------+-------------+
            |
    +-------+--------+
    | User Data (DB) |
    | SQL Server     |
    +----------------+
            |
            v
+------------------------------+
|   Python AI Agent (LLM)      |
| - Learning Plan Generator    |
| - Progress Evaluator         |
| - Daily Task Recommender     |
+------------------------------+
            |
            v
+------------------------------+
|   Vector Store (RAG System)  |
|  - Pinecone / Qdrant         |
|  - Stores & searches context |
|    from curated learning     |
|    content (docs/videos)     |
+------------------------------+
            |
            v
+------------------------------+
|  OpenAI / Azure OpenAI GPT   |
|  - LLM for reasoning,        |
|    task planning, and Q&A    |
+------------------------------+
```

---

## 4. Technology Stack

| Layer       | Technology                    |
|-------------|-------------------------------|
| Frontend    | React, TypeScript             |
| Backend     | ASP.NET Core 8 Web API        |
| AI Agent    | Python, LangChain / Azure OpenAI |
| Database    | SQL Server / PostgreSQL       |
| Vector DB   | Pinecone / Azure Cognitive Search |
| Auth        | Azure AD B2C / Auth0          |
| Hosting     | Azure Web Apps / Kubernetes   |

---

## 5. Key Modules

- **User Profile Service**
- **Goal & Skill Tracker**
- **Learning Plan Generator**
- **Agent Engine (AI Logic)**
- **Recommendation Engine**
- **Progress Analytics**
- **Notification & Nudging System**

🧩 Module-Level Breakdown
Each module includes:

* 🔹 Name

* 🔹 Responsibilities

* 🔹 Tech Stack

* 🔹 Input/Output

* 🔹 Delivery Goal

### 🔐 1. Authentication & User Management Module
Responsibilities:

* Register/Login users

* Manage user sessions and tokens

* Role-based access (optional)

* Tech Stack: .NET 8 Web API + Identity / Azure AD B2C

* Input: Email, password, OAuth tokens

* Output: JWT token, user context

* Delivery Goal: Auth API + frontend integration

#### 🎯 2. Goal & Skill Tracker Module
Responsibilities:

Let users define learning goals and target skills

Store timelines and preferences

Tech Stack: .NET 8 Web API + SQL Server

Input: Goal name, topic, timeframe, difficulty level

Output: Structured user goal object

Delivery Goal: API endpoints for goal CRUD + UI form

#### 🧠 3. AI Agent Module
Responsibilities:

Accept goals and user profiles

Generate personalized learning plans

Recommend daily/weekly tasks

Tech Stack: Python + LangChain + OpenAI GPT-4 / Azure OpenAI

Input: Goal, skill profile, past progress

Output: Structured learning plan (tasks, resources)

Delivery Goal: Flask/FastAPI microservice with basic planning logic

#### 📚 4. Content Retrieval (RAG) Module
Responsibilities:

Use a vector store to semantically search curated content

Power the agent’s resource suggestions

Tech Stack: Python + Pinecone / Qdrant + LangChain

Input: Goal/topic query from AI Agent

Output: Ranked resource list (title, URL, summary)

Delivery Goal: Index pre-curated docs and support semantic search

#### 📈 5. Progress Tracker & Feedback Module
Responsibilities:

Allow users to mark task progress

Adjust future plans based on feedback and history

Tech Stack: .NET 8 Web API + SQL Server + React

Input: Task status updates, feedback

Output: Updated progress profile, feedback log

Delivery Goal: API + UI for marking and viewing progress

#### 📢 6. Nudging & Notification Module
Responsibilities:

Send motivational messages or reminders

Notify users of task changes or deadlines

Tech Stack: .NET Background Jobs (Hangfire) or Azure Functions + Email/WhatsApp API

Input: User schedule, inactivity signals

Output: Message trigger (email/SMS/push)

Delivery Goal: Scheduled reminders + optional manual trigger UI

#### 📊 7. Dashboard & UI Module
Responsibilities:

Central UI for goal setup, plan view, task updates

Progress visualization and recommendations

Tech Stack: React + TypeScript + Zustand or Redux

Input: API data (goals, plans, tasks)

Output: Dynamic UI with interactive views

Delivery Goal: Functional responsive dashboard + login flow

#### 🧪 8. QA & Observability Module
Responsibilities:

Logging, error tracking, performance monitoring

Unit and integration test coverage

Tech Stack: Serilog + Application Insights + xUnit + Postman

Input: Runtime events, HTTP traffic

Output: Logs, metrics, alerts, test reports

Delivery Goal: Centralized logs + basic monitoring alerts

#### ✅ Recommended Delivery Order (MVP)
Authentication Module

Goal Tracker + UI Form

AI Agent Basic Plan Generator

Progress Tracker

Learning Plan UI Integration

Content Search (RAG)

Nudging/Notification System

Observability + Test Coverage



---

## 6. Data Flow

1. User sets a goal via UI
2. Backend stores goal and user context
3. Agent queries vector DB + LLM to generate a learning plan
4. Plan sent to frontend
5. As user completes tasks, progress is updated and next steps are suggested

---

## 7. Non-Functional Requirements

- Scalable microservices architecture
- Responsive UI/UX
- Secure authentication & authorization
- Observability (logs, metrics, alerts)
- Maintainable and modular codebase

---

## 8. Deployment Strategy

- Dockerized containers for API and agent
- Deploy on Azure using Kubernetes or App Services
- CI/CD via GitHub Actions or Azure DevOps

---

## 9. Future Enhancements

- Voice-based interaction
- Integration with third-party platforms (YouTube, Udemy)
- Multi-language support
