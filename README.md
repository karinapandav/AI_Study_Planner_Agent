# AI Study Planner Agent

An AI-powered study planning and scheduling workflow built with **n8n, Groq, Google Sheets, Google Calendar, and Gmail**.

The AI Study Planner Agent takes a student's study requirements through a form, generates a personalized study schedule using an AI agent, converts the generated plan into structured study sessions, creates Google Calendar events, stores the sessions in Google Sheets, and sends the completed study plan through email.

The project demonstrates how **AI agents, workflow automation, APIs, and cloud productivity tools** can be combined to build a practical productivity application without developing a separate frontend.

---

# Features

## AI Study Plan Generation

The workflow generates personalized study schedules based on:

* Student name
* Subject/topic
* Exam date
* Available study hours per day
* Current knowledge level
* Weak topics
* Completed topics
* Study preference

The AI analyzes the provided information and breaks the required syllabus into manageable study sessions.

Each generated session contains information such as:

* Date
* Subject
* Topic
* Start time
* End time
* Session type
* Priority

---

## AI-Powered Planning

The project uses an AI Agent powered by **Groq** to generate the study schedule.

The AI is instructed to:

* Understand the student's requirements
* Prioritize weak topics
* Break large topics into smaller sessions
* Allocate available study time
* Include learning, revision, practice, and mock-test sessions
* Respect the student's exam date and daily study limit
* Produce structured data for downstream automation

---

## Automatic Google Calendar Scheduling

Generated study sessions are automatically converted into Google Calendar events.

The workflow:

1. Generates a study session.
2. Creates a corresponding Calendar event.
3. Retrieves the Calendar Event ID.
4. Stores the event information with the study session.

This allows the generated timetable to become an actionable calendar schedule instead of remaining only as text.

---

## Google Sheets Study Plan Storage

Google Sheets acts as the lightweight database for storing generated study sessions.

Each study session can contain:

| Field             | Description                          |
| ----------------- | ------------------------------------ |
| Plan ID           | Unique identifier for the study plan |
| Date              | Study session date                   |
| Start Time        | Session start time                   |
| End Time          | Session end time                     |
| Subject           | Subject being studied                |
| Topic             | Specific topic                       |
| Priority          | Session priority                     |
| Status            | Current session status               |
| Calendar Event ID | Associated Google Calendar event     |

Google Sheets provides a simple and accessible way to view and manage the generated study schedule.

---

## Email Delivery

After the study plan is generated and processed, the workflow uses Gmail to send the study-plan information to the user.

This creates an end-to-end automation flow from:

**Student Input → AI Plan → Calendar → Google Sheets → Email**

---

# Workflow Architecture

## Create Study Plan

```text
                         User
                           │
                           ▼
                ┌────────────────────┐
                │ Form — Study       │
                │ Planner Input      │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │      AI Agent       │
                │      (Groq)         │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Code — Parse        │
                │ Schedule            │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Split in Batches    │
                │ One Session at Time │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Google Calendar     │
                │ Create Event        │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Code — Build Sheet  │
                │ Rows + Email        │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Google Sheets       │
                │ Log Study Plan      │
                └──────────┬─────────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Gmail               │
                │ Send Confirmation   │
                └────────────────────┘
```

---

# Workflow Breakdown

### 1. Form — Study Planner Input

The student submits their study requirements through an n8n form.

Example inputs:

```text
Name: Karina
Subject: Machine Learning
Exam Date: 2026-08-30
Study Hours/Day: 3
Current Level: Beginner
Weak Topics: Supervised Learning
Study Preference: Theory + Practice
```

---

### 2. AI Agent

The submitted information is passed to the AI Agent.

The agent generates a personalized schedule based on:

* Available preparation time
* Exam deadline
* Current level
* Weak areas
* Study preference
* Required subject coverage

The AI produces structured schedule information that can be processed by the next workflow stage.

---

### 3. Parse Schedule

The generated AI response is processed by a Code node.

The parser:

* Extracts the generated schedule
* Converts the AI response into usable JSON
* Validates the schedule structure
* Prepares individual sessions for downstream processing

---

### 4. Split in Batches

The generated study plan contains multiple sessions.

The workflow processes them **one session at a time**.

This allows each session to be independently:

* Scheduled in Google Calendar
* Stored in Google Sheets
* Associated with a Calendar Event ID

---

### 5. Google Calendar

Each study session is converted into a Google Calendar event.

Example:

```text
Machine Learning — Supervised Learning
16:30 – 19:00
August 16, 2026
```

The resulting Calendar Event ID is captured for tracking.

---

### 6. Build Sheet Rows + Email

A Code node transforms the processed session and Calendar information into the format required by the downstream Google Sheets and Gmail nodes.

This acts as a data transformation layer between the workflow components.

---

### 7. Google Sheets

The final study sessions are stored in Google Sheets.

This provides persistent storage for the generated timetable and allows the user to easily view their schedule.

---

### 8. Gmail

The workflow sends the resulting study-plan information through Gmail, providing the student with an additional copy of their generated schedule.

---

# Tech Stack

### Workflow Automation

* **n8n**

### AI

* **Groq**
* Groq Chat Model
* AI Agent
* Prompt Engineering

### Google Services

* Google Sheets API
* Google Calendar API
* Gmail API
* Google OAuth2

### Data Processing

* JavaScript
* JSON
* n8n Code Nodes
* Data transformation
* Batch processing

---

# Authentication

The workflow uses **Google OAuth2** to securely connect n8n with:

* Google Sheets
* Google Calendar
* Gmail

No separate frontend application or custom authentication system is required for the current workflow.

---

# Current Workflow Capabilities

## Implemented

* AI-powered study-plan generation
* n8n form-based user input
* Groq-powered AI Agent
* Personalized scheduling
* Weak-topic prioritization
* Structured schedule generation
* JSON parsing
* Session-by-session processing
* Google Calendar event creation
* Calendar Event ID tracking
* Google Sheets study-session storage
* Gmail integration
* End-to-end workflow automation

---

# Learning Outcomes

This project demonstrates practical experience with:

* AI Agents
* Generative AI
* Prompt Engineering
* Workflow Automation
* n8n
* Groq API
* Google APIs
* OAuth2 Authentication
* Google Sheets integration
* Google Calendar integration
* Gmail integration
* JSON processing
* Data transformation
* Batch processing
* API-based automation
* AI-powered scheduling
* Event creation and synchronization
* Low-code AI application development

---

# Contributing

Contributions, suggestions, and feature requests are welcome.

Feel free to fork this repository and submit a pull request.

---

# License

This project is licensed under the **MIT License**.

---

# Author

**Karina Pandav**

Built as a practical project exploring **AI Agents, workflow automation, and intelligent productivity systems**.

If you found this project useful, consider giving it a ⭐ on GitHub.
