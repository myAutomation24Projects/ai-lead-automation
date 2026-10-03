AI Lead Automation with n8n

An AI-powered lead qualification and routing workflow built with n8n, Google Sheets, Google Gemini, and Gmail.

The workflow automatically analyzes new leads, classifies them as HOT, WARM, or COLD, updates the lead record, and sends an appropriate follow-up email based on the lead's intent and priority.

## Workflow Overview

```text
Google Sheets Trigger
        ↓
     AI Agent
        ↓
Update Row in Google Sheets
        ↓
      Switch
    ↙    ↓    ↘
  HOT   WARM   COLD
   ↓      ↓      ↓
AI Agent AI Agent Update Sheet
   ↓      ↓
 Gmail   Gmail

What This Project Does

Detects a new lead added to Google Sheets.

Sends the lead information to an AI Agent.

Uses Google Gemini to analyze the lead.

Produces structured lead information.

Updates the original Google Sheets row.

Routes the lead using a Switch node:

HOT → high-priority follow-up

WARM → normal follow-up

COLD → records the classification without sending the same high-priority message

Generates an appropriate email for HOT and WARM leads.

Sends the email through Gmail.

Key Features

AI-based lead qualification

HOT / WARM / COLD lead routing

Structured AI output

Automatic Google Sheets updates

Automated email generation

Gmail integration

Conditional workflow routing

n8n AI Agent workflow

Google Gemini integration

Tech Stack

Technology

Purpose

n8n

Workflow automation

Google Sheets

Lead database and trigger

Google Gemini

AI analysis and message generation

Gmail

Automated lead follow-up

JavaScript / Expressions

Data mapping inside n8n

Workflow Nodes

1. Google Sheets Trigger

Triggers the workflow when a new lead is added to the Google Sheet.

Example lead data:

Name
Email
Company
Requirement
Budget
Timeline
Message

The exact columns can be changed depending on the business use case.

2. AI Agent

The first AI Agent analyzes the incoming lead.

Typical responsibilities:

Understand the lead's requirement

Identify buying intent

Consider budget and timeline

Determine lead priority

Return structured information for the next nodes

The AI Agent is connected to a Google Gemini Chat Model and a Structured Output Parser.

3. Structured Output Parser

The parser makes the AI response predictable so that n8n can use the result in later nodes.

A possible output structure is:

{
  "lead_status": "HOT",
  "reason": "Strong buying intent and short timeline",
  "priority": "HIGH"
}

4. Update Row in Google Sheets

The workflow writes the AI analysis back into the same lead record.

This allows the business to see the lead status directly in the spreadsheet.

5. Switch Node

The Switch node routes the lead based on the AI classification.

HOT  → High-priority follow-up
WARM → Normal follow-up
COLD → Update/record classification

6. HOT Lead AI Agent

The HOT lead branch uses another AI Agent to generate a personalized follow-up message.

The message can be based on:

Lead name

Requirement

Company

Budget

Timeline

Original enquiry

The generated message is then passed to Gmail.

7. WARM Lead AI Agent

The WARM branch follows a similar process but generates a less urgent follow-up.

8. Gmail

The Gmail nodes send the generated messages to the lead.

This removes the need for a salesperson to manually write the initial follow-up for every qualified lead.

Example Use Case

Imagine a software company receives enquiries from its website.

A new lead enters Google Sheets:

Name: Rahul
Company: ABC Technologies
Requirement: AI chatbot for customer support
Budget: ₹1,50,000
Timeline: 2 weeks
Message: We want to start quickly and need a demo.

The AI Agent may classify the lead as:

Status: HOT
Priority: HIGH
Reason: Clear requirement, defined budget and short implementation timeline

The workflow then routes the lead to the HOT branch and generates a personalized follow-up email.

Why This Automation Is Useful

Without automation:

New lead
   ↓
Salesperson checks spreadsheet
   ↓
Reads the enquiry
   ↓
Decides lead priority
   ↓
Writes an email
   ↓
Sends email

With this workflow:

New lead
   ↓
AI analyzes lead
   ↓
Lead is classified
   ↓
Spreadsheet is updated
   ↓
Appropriate follow-up is generated
   ↓
Email is sent

This can reduce repetitive manual lead qualification and follow-up work.

Setup

Requirements

n8n (self-hosted or cloud)

Google account

Google Sheets

Gmail

Google Gemini API / supported Gemini credential

A Google Sheet containing your lead data

Basic Setup Steps

Create a Google Sheet for your leads.

Add the required lead columns.

Connect Google Sheets to n8n.

Configure the Google Sheets Trigger.

Add the AI Agent.

Connect the Google Gemini Chat Model.

Add a Structured Output Parser.

Configure the AI output fields.

Add the Google Sheets Update Row node.

Add a Switch node.

Create HOT, WARM, and COLD rules.

Add AI Agents to the HOT and WARM branches.

Connect Gmail to the follow-up branches.

Test the workflow with sample leads.

Verify that the spreadsheet is updated and the correct email branch is executed.

Testing

Use sample leads representing different levels of intent.

HOT Lead

Strong requirement
Clear budget
Short timeline
Wants to start soon

Expected result:

HOT → Personalized high-priority email

WARM Lead

Interested
Requirement is reasonably clear
No immediate deadline

Expected result:

WARM → Personalized follow-up email

COLD Lead

General enquiry
Low buying intent
No clear timeline

Expected result:

COLD → Classification/update without the HOT follow-up

Important Security Note

Never upload API keys, passwords, OAuth secrets, or exported n8n credentials to a public GitHub repository.

If you export an n8n workflow JSON, inspect it before uploading it and remove any sensitive credential information.

GitHub specifically recommends not committing sensitive information such as passwords or API keys.

Suggested Repository Structure

ai-lead-automation/
│
├── README.md
├── workflow/
│   └── ai-lead-automation.json
│
├── screenshots/
│   └── workflow.png
│
└── sample-data/
    └── leads.csv

Future Improvements

Possible next versions of this project could include:

Lead scoring based on multiple signals

Duplicate lead detection

CRM integration

Slack/WhatsApp notifications

Follow-up scheduling

Lead response tracking

Sales dashboard

Error handling and retry workflow

Human approval before sending emails

Lead analytics and conversion tracking

Project Goal

This project demonstrates how AI agents and workflow automation can be combined to automate a practical sales process, from lead intake and qualification to personalized follow-up.

Built With

n8n · Google Sheets · Google Gemini · Gmail · AI Agents
