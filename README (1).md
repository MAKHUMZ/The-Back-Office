# The Back Office — AI-Powered Workplace Productivity Assistant

A CAPACITI AI Skill Accelerator project: an AI assistant that automates three of the most time-consuming admin tasks for a small business owner.

## What it does
- **Smart Email Generator** — draft a ready-to-send email by describing what it needs to say, choosing an audience (client / supplier / team) and a tone (formal, informal, persuasive).
- **Meeting Notes Summarizer** — paste in raw meeting notes, get back Key Points, Decisions Made, and Action Items (owner + deadline).
- **AI Task Planner** — list your tasks and errands, get back a prioritized, time-blocked plan for the day or week.

## Tools used
- Claude (Anthropic) — Messages API, for all generation
- React — interface

## Project structure
```
BackOfficeAssistant.html  # the working prototype (open directly in a browser)
documentation.md          # problem statement, solution overview, prompts, challenges
README.md                 # this file
```

## Running it
Open `BackOfficeAssistant.html` directly in a browser — no build step required. It calls the Anthropic Messages API from the client. To run it outside of the Claude environment it was built in, wire it up to your own backend/API key rather than calling the API directly from the browser (never expose an API key in client-side code in production).

## Responsible AI
Every output is a draft. The prompts are instructed not to invent facts, prices, dates, or commitments, and to flag when input is too thin to summarize or a task list is unrealistic for the time available — see `documentation.md` for details.

## Author
CAPACITI AI Skill Accelerator Programme — AI-Powered Workplace Productivity Assistant project.
