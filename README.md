# ai-interview-prep-automation

> No-code automation that generates interview questions and answers with Gemini, stores them in Google Sheets, and emails them daily.

<img width="989" height="957" alt="Screenshot 2026-10-22 132833" src="https://github.com/user-attachments/assets/a1399422-060b-4875-94d6-a11152bf2ae0" />

## Problem

Interview preparation is usually manual and inconsistent. Questions are collected ad hoc, practice depends on remembering to sit down and do it, and good material is rarely saved in one reusable place.

## Solution

A Make.com scenario that runs automatically **every day at 4:00 PM**. Each run generates a fresh set of interview questions with Google Gemini, saves them to a Google Sheet that grows into a reusable Interview Question Bank, and emails the results so daily practice happens without any manual effort. The scenario can also be triggered manually with **Run once** when you want an on-demand session.

## Architecture

```
Set variables  →  Google Gemini AI  →  Google Sheets  →  Gmail
   (Tools)        (Simple text        (Add a Row)       (Send an Email)
                     prompt)
```

| # | Module | Purpose |
|---|--------|---------|
| 1 | **Tools: Set variables** | Defines the practice configuration: role, topic and difficulty |
| 2 | **Google Gemini AI** | Generates questions, sample answers, workplace examples and follow-ups from a text prompt |
| 3 | **Google Sheets: Add a Row** | Saves the output to the Interview Question Bank |
| 4 | **Gmail: Send an Email** | Delivers the generated questions to your inbox |

## Inputs

Set in the **Tools: Set variables** module:

- **Role**: the job role you are preparing for
- **Topic**: the subject area to practise
- **Difficulty**: the level of the questions

## Outputs

Each run produces:

- Five interview questions
- Sample answers
- Workplace examples
- Follow-up questions

The results are appended as a new row in Google Sheets and sent by email.

## Setup

1. Create a free account at [make.com](https://www.make.com).
2. In Make, choose **Create scenario → ⋯ → Import Blueprint** and upload [`blueprint/interview-prep-generator.blueprint.json`](blueprint/interview-prep-generator.blueprint.json).
3. **Reconnect your connections**: Google Gemini AI (API key from Google AI Studio), Google Sheets, and Gmail.
4. **Update the placeholders** in the modules:
   - Google Sheets: select your own spreadsheet and sheet (replace `YOUR_SHEET_ID`)
   - Gmail: set the recipient address (replace `YOUR_EMAIL`)
5. In **Set variables**, enter your role, topic and difficulty.
6. Click **Run once** to test, then turn the scenario **Active** and set the schedule to daily at 4:00 PM.

> **Security note:** never commit API keys or credentials. Make does not export connections in blueprints, and you must create your own after importing.

## Tech Stack

- [Make.com](https://www.make.com): workflow orchestration and scheduling
- Google Gemini API: question and answer generation
- Google Sheets: Interview Question Bank storage
- Gmail: daily delivery

## Repository Structure

```
├── README.md
├── blueprint/
│   └── interview-prep-generator.blueprint.json
├── docs/
│   ├── scenario-canvas.png
│   ├── sheet-output.png
│   └── email-output.png
└── prompts/
    └── gemini-prompt.md
```

## Future Improvements

- **Workflow: Resume Tailoring**, a companion workflow that takes a job description, compares it with your existing resume, and suggests tailored bullet points without inventing experience. Its output can feed role-specific questions into this interview prep generator.

