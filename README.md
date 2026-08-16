# AI Study Planner Agent

An AI-powered study planning and scheduling agent built with **n8n, Grok, Google Calendar, Google Sheets, and Gmail**.

The system takes a student's study requirements through a form, uses an AI agent to generate a personalized day-by-day study schedule, validates and parses the structured plan, creates individual study sessions in Google Calendar, stores the complete plan in Google Sheets, and sends a confirmation email automatically.

🔗 **Live Demo:** https://n8n-service-tm25.onrender.com/form/a09fb499-2c9f-4bac-98ed-cb6663fee616

---

## Overview

Planning a study schedule manually can be time-consuming, especially when students need to balance:

- Exam dates
- Multiple subjects
- Available study hours
- Topic coverage
- Revision
- Practice sessions
- Daily time constraints

The **AI Study Planner Agent** automates this process.

A student provides their study requirements, and the AI generates a structured study plan based on predefined planning rules. The workflow then automatically converts the generated plan into actionable calendar events and stores the schedule for tracking.

---

## Features

### AI-Powered Study Planning

Uses **Grok** to generate a personalized study schedule based on:

- Exam date
- Available study time
- Subjects
- Study preferences
- Planning constraints

### Automatic Google Calendar Scheduling

Every generated study session is converted into a Google Calendar event with:

- Subject
- Topic
- Date
- Start time
- End time
- Study session details

### Google Sheets Tracking

The generated study plan is automatically stored in Google Sheets for easy tracking and reference.

### Email Confirmation

After the plan is generated, the system automatically sends a confirmation email to the student.

### Multi-Session Processing

The workflow processes each study session individually using an n8n loop, allowing every session to be independently added to Google Calendar and recorded.

### Structured AI Output

The AI is instructed to return structured JSON containing:

- Student information
- Exam date
- Subjects
- Study sessions
- Topics
- Duration
- Session type
- Priority

This makes the AI output reliable and usable by downstream automation nodes.

### Error Handling

The Google Sheets integration includes retry handling for temporary API failures such as HTTP 503 errors.

---

# Workflow Architecture

```text
                ┌──────────────────────┐
                │     Student Form     │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │      Grok AI Agent   │
                │                      │
                │  Generate Study Plan │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │    Parse Schedule    │
                │   Structured JSON    │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │   Loop Over Items    │
                │ Process Each Session │
                └──────────┬───────────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
      ┌────────────┐ ┌────────────┐ ┌────────────┐
      │   Google   │ │   Google   │ │   Gmail    │
      │  Calendar  │ │   Sheets   │ │            │
      └────────────┘ └────────────┘ └────────────┘

```
### How It Works

1. Student submits their requirements
The student provides information such as:
Name
Exam date
Subjects
Available study hours
Preferred study time

2. AI Agent generates the plan
The information is sent to the Grok AI model.
The AI follows predefined study-planning rules such as:
Calculating available study days
Allocating new learning and revision
Keeping sessions within available study hours
Assigning specific topics
Prioritizing important subjects
Scheduling revision closer to the exam
Reserving the final days for revision and quick practice

3. Structured output is generated
The AI returns the study plan in a structured JSON format.

4. Schedule is parsed
The structured response is processed by n8n and converted into individual study-session items.

5. Sessions are processed individually
The Loop Over Items node processes each study session separately.
For every session, the workflow:

Study Session
      ↓
Google Calendar
      ↓
Google Sheets
      ↓
Confirmation

6. Google Calendar events are created
Each session becomes an actionable calendar event.

7. Study plan is stored
The sessions are logged in Google Sheets so the student has a centralized record of their plan.

8. Confirmation is sent
The student receives an email confirming that their study plan has been generated.

### Study Planning Logic

The AI agent follows a predefined set of rules to create the schedule.

Planning rules include:
Calculate the exact number of available study days
Distribute subjects fairly
Prioritize important topics
Allocate more revision closer to the exam
Use new learning during the initial phase
Use revision and practice during the later phase
Keep individual sessions between 1.5 and 3 hours
Respect the student's daily available study hours
Assign specific topics instead of generic subject names
Reserve the final two days for revision and quick practice

This combines LLM-based reasoning with deterministic workflow automation.

### Tech Stack
Technology	Purpose
n8n	Workflow automation and orchestration
Grok	AI-powered study plan generation
Google Calendar API	Creates study sessions
Google Sheets API	Stores study plans
Gmail	Sends confirmation emails
Render	Cloud deployment

### Deployment
The n8n workflow is deployed on Render.

Student
   ↓
Public n8n Form
   ↓
Render-hosted n8n
   ↓
Grok
   ↓
Google APIs
Live Demo

Try the AI Study Planner
Note: The live demo runs on a free Render instance, so the service may take some time to wake up after a period of inactivity.

Required Credentials
To run the workflow, the following credentials are required:

Grok / xAI
xAI API key
Google Cloud

OAuth credentials for:
Google Calendar
Google Sheets
Gmail

These credentials should be stored securely in n8n and must never be committed to GitHub.

### Setup
1. Clone the repository
git clone https://github.com/karinapandav/AI_Study_Planner_Agent.git
cd AI_Study_Planner_Agent

2. Set up n8n
Run n8n locally or deploy it using a supported hosting provider.

3. Import the workflow
Import the provided n8n workflow into your n8n instance.

4. Configure credentials
Connect:
Grok / xAI
Google Calendar
Google Sheets
Gmail

5. Configure the Google Sheet
Create a spreadsheet for storing generated study sessions.

Suggested columns:
Plan ID
Date
Day
Subject
Topic
Duration
Start Time
End Time
Session Type
Priority

6. Configure Google Calendar
Connect the Google Calendar account where study sessions should be created.

7. Activate the workflow
Publish/activate the workflow and use the production form URL.
    
### Why This Project?

This project demonstrates how AI models can be combined with workflow automation and real-world APIs to create useful applications.
Instead of simply generating text with an LLM, the AI output is converted into structured data and used to perform real actions:

LLM
 ↓
Structured Data
 ↓
Automation
 ↓
External APIs
 ↓
Real-world Actions

### What I Learned

Building this project helped me gain practical experience with:

AI agent workflows
Prompt engineering
Structured LLM output
JSON parsing
n8n workflow orchestration
API integrations
Google OAuth authentication
Google Calendar automation
Google Sheets automation
Error handling and retries
Cloud deployment
Connecting AI outputs to real-world actions
 
### Author

### Karina Pandav ###

B.Tech — Artificial Intelligence & Data Science

⭐ If you found this project interesting

Feel free to explore the workflow, try the live demo, or connect with me on GitHub.
