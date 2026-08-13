# AI Study Planner Agent

An AI-powered study planning and scheduling agent built with n8n, Google Gemini/Groq, Google Sheets, and Google Calendar.

The agent allows students to create personalized study plans using natural language, automatically stores study sessions, creates calendar events, and supports rescheduling existing sessions through conversational commands.

The project demonstrates how AI agents and workflow automation can be combined to build practical productivity tools without requiring a separate frontend application.
---

# Features
**AI Study Plan Generation**
Generate personalized study schedules based on:
Exam details
Subjects/topics
Available study time
Study priorities
Exam date

The AI breaks the syllabus into manageable study sessions and produces structured outputs for downstream automation.

**Conversational AI Agent**
Users can interact with the study planner using natural language.
Example:
Create a study plan for my DBMS exam.
Generate a study schedule for my Machine Learning exam.
I have 3 hours every day and my exam is in two weeks. Create a plan.

**AI Intent Classification**
The workflow identifies the user's intent and routes the request to the appropriate process.
Currently supported intents:
Create Study Plan
Reschedule Study Session

This allows multiple study-management operations to be handled through a single conversational workflow.

**Intelligent Study Session Rescheduling**
Users can modify existing sessions using natural language.
Examples:
Move my Calculus session to tomorrow.
Shift my DBMS session to Friday at 2 PM.
Reschedule my Mathematics revision.

The workflow:
Reads existing study sessions.
Identifies the relevant session.
Generates the updated schedule.
Updates Google Sheets.
Synchronizes the change with Google Calendar.

**Google Sheets Integration**
Google Sheets acts as the lightweight data layer for storing study plans and sessions.
Plans
Stores information such as:
Plan ID
Exam Name
Start Date
Exam Date
Created Timestamp
Sessions

Stores:
Plan ID
Date
Start Time
End Time
Subject
Topic
Priority
Status
Calendar Event ID

**Google Calendar Integration**
Study sessions are automatically synchronized with Google Calendar.
The workflow can:
Create study events
Store Calendar Event IDs
Update events when sessions are rescheduled
 
**Structured AI Outputs**
AI responses are converted into structured JSON using n8n's Structured Output Parser.
This makes the AI output reliable enough to pass between different workflow stages.

# 🛠 Tech Stack

### Workflow Automation

- n8n

### AI

- Google Gemini *(or Groq GPT-OSS Models)*

### Google Services

- Google Sheets API
- Google Calendar API
- Google OAuth2

### AI Components

- AI Agent
- Intent Classifier
- Structured Output Parser
- Simple Memory

---

# 🏗 Workflow Architecture

## Create Study Plan

```text
                    User
                      │
                      ▼
                Chat Trigger
                      │
                      ▼
             Intent Classifier
                      │
                      ▼
             AI Study Planner
                      │
                      ▼
         Structured Output Parser
                      │
            ┌─────────┴─────────┐
            ▼                   ▼
      Google Sheets      Google Calendar
                      │
                      ▼
              Respond to User
```

---

## Reschedule Study Plan

```text
                    User
                      │
                      ▼
                Chat Trigger
                      │
                      ▼
             Intent Classifier
                      │
                      ▼
             Read Google Sheets
                      │
                      ▼
             Aggregate Sessions
                      │
                      ▼
       Merge Chat + Session Data
                      │
                      ▼
             AI Rescheduler
                      │
                      ▼
         Structured Output Parser
                      │
              Update Google Sheets
                      │
                      ▼
            Update Google Calendar
                      │
                      ▼
               Respond to User
```

---

# 💬 Example Commands

## Create a Study Plan

```
Create a study plan for my Data Structures exam.
```

```
Generate a weekly timetable for Machine Learning.
```

---

## Reschedule a Session

```
Move my Calculus study session to tomorrow at 2 PM.
```

```
Shift my DBMS revision to Friday evening.
```

```
Reschedule my Mathematics session.
```

---

# 🚀 Current Status

## ✅ Completed

- AI-powered Study Plan Generation
- Conversational AI Agent
- Intent Classification
- Google Sheets Integration
- Google Calendar Integration
- Structured Output Parsing
- AI-powered Study Session Rescheduling
- Google Sheets Synchronization
- Google Calendar Synchronization
- End-to-End Workflow Automation

---

## 🚧 Planned Enhancements

- Unique Session IDs
- Study Conflict Detection
- Automatic Workload Balancing
- Daily Study Reminders
- Email Notifications
- WhatsApp / Telegram Integration
- Weekly Progress Reports
- Study Analytics Dashboard
- PDF Study Plan Export
- Voice-enabled Study Planner
- Deployment

---

# 📚 Learning Outcomes

This project demonstrates practical experience with:

- AI Workflow Automation
- Prompt Engineering
- AI Agents
- Intent Classification
- Structured AI Outputs
- Workflow Orchestration using n8n
- Google Sheets API
- Google Calendar API
- Data Aggregation
- Data Merging
- JSON Processing
- Event Synchronization
- Conversational AI
- Low-Code AI Development

---

# 🚀 Future Roadmap

- Multi-user authentication
- User-specific study plans
- Adaptive scheduling using AI
- Exam progress tracking
- Revision optimization
- Mobile app integration
- Dashboard with analytics
- RAG-powered syllabus understanding
- Voice assistant support

---

# 🤝 Contributing

Contributions, suggestions, and feature requests are welcome.

Feel free to fork this repository and submit a pull request.

---

# 📄 License

This project is licensed under the MIT License.

---

# 👨‍💻 Author

**Karina Pandav**

If you found this project helpful, consider giving it a ⭐ on GitHub.
