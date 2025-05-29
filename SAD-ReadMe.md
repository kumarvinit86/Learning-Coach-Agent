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
[React UI] ⇄ [.NET 8 Web API] ⇄ [SQL DB]
⇡
[Python Agent / Azure Function]
⇅
[Vector DB + LLM (OpenAI/GPT-4)]


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
