# AI-Powered Workplace Productivity Assistant
### The Back Office — an admin assistant for small business owners

## Problem statement
Small business owners spend a large share of their week on admin that isn't the business itself: writing emails to suppliers and clients, turning scattered meeting notes into things people can actually act on, and figuring out what to do first on a day that has too much in it. Done manually, this admin work eats into time that should go toward customers, product, and growth — and because it's repetitive, it's also exactly the kind of work AI is well suited to accelerate.

## Solution overview
The Back Office is a working prototype that automates three of the highest-friction admin tasks for a small business owner, through a single lightweight interface:

1. **Smart Email Generator** — turns a short description of what needs to be said into a ready-to-send email, adapted to audience (client / supplier or manager / team) and tone (formal, informal, persuasive).
2. **Meeting Notes Summarizer** — turns raw, messy meeting notes into three usable sections: Key Points, Decisions Made, and Action Items (each with an owner and deadline where one was given).
3. **AI Task Planner** — turns a flat list of tasks and errands into a prioritized, time-blocked plan for a day or a week, and flags when the list is unrealistic for the timeframe.

Each tool is its own tab; the owner fills in a short form and the AI's output appears as a printed "receipt" they can copy straight into an email, a to-do list, or a calendar.

## Tools used
- **Claude (Anthropic)** via the Messages API — generation for all three features.
- **React** — the interface (three tools, one shared shell).
- Prompt design and testing were done iteratively in-conversation before being locked into system prompts (see below).

## Sample prompts
Each feature uses a dedicated system prompt rather than one generic prompt, so the model's behaviour is scoped tightly to the task:

**Email Generator (system prompt, abridged):**
> You are a correspondence assistant for a small business owner who is short on time. Draft a ready-to-send email based on the details given. Match the requested tone exactly. Adapt vocabulary and formality to the stated audience. Do not invent facts, prices, dates, or commitments the owner did not mention — use a bracketed placeholder instead. Output ONLY the subject line and email body.

**Meeting Summarizer (system prompt, abridged):**
> You summarize raw, messy meeting notes for a small business owner who cannot attend every meeting personally. Work only from what is in the notes — never invent attendees, numbers, or commitments. Output exactly three sections: KEY POINTS, DECISIONS MADE, ACTION ITEMS (each item with owner and deadline). If the notes are too thin to summarize responsibly, say so.

**Task Planner (system prompt, abridged):**
> You are a scheduling assistant for a small business owner juggling many small tasks. Build a realistic, time-blocked plan for the stated horizon. Prioritize by urgency and importance, not list order. If the task list is clearly too much for the horizon, say so explicitly and suggest what to defer.

Each user-facing form maps directly onto the variable part of these prompts (audience, tone, raw notes, task list, horizon), so the owner never has to write a prompt themselves.

## Responsible AI considerations
- **No invented facts.** All three prompts explicitly instruct the model not to fabricate details (prices, dates, attendees, commitments) and to flag gaps instead of guessing.
- **Honesty over completeness.** The summarizer and planner are told to say when input is too thin or a plan is unrealistic, rather than forcing a polished-looking but misleading answer.
- **Human in the loop.** The interface carries a standing note that every output is a draft to review before sending, sharing, or acting on — the tool accelerates the admin work, it doesn't remove the owner's judgment from it.
- **Scope limits.** The assistant only drafts and summarizes; it never sends emails, books anything, or takes actions on the owner's behalf.

## Challenges and solutions
| Challenge | Solution |
|---|---|
| A single generic prompt produced inconsistent, sometimes rambling output across very different tasks (drafting vs. summarizing vs. scheduling). | Split into three dedicated system prompts, each with its own role, constraints, and required output format. |
| Early drafts of the summarizer occasionally smoothed over gaps in messy notes with plausible-sounding but unstated details. | Added an explicit rule to state when notes are too ambiguous, and to never invent attendees, numbers, or commitments. |
| A results-only interface felt like a generic chatbot and didn't reflect the small-business, admin-desk context of the brief. | Designed the interface around a "back office" metaphor — folder tabs per task, output rendered as a printed receipt — so the tool feels purpose-built rather than templated. |
