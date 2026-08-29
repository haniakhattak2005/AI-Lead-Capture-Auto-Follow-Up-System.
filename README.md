# AI Lead Capture & Auto Follow-Up System

An automation that captures a new lead the moment they submit a form, saves them to a CRM, and sends a personalized AI-generated follow-up email — all within seconds, with zero manual work.

Built with **n8n**, **Airtable**, **Gemini AI**, and **Gmail**.

---

## The Problem

When a business gets a new lead, there's usually a delay before anyone replies — the sales rep is busy, checks email once a day, or the lead gets buried in an inbox. Leads go cold fast, and slow follow-up directly costs businesses potential customers.

This system removes that delay. The moment someone submits interest, they receive a personalized reply — not a generic template, but a message written around exactly what they said they need.

---

## How It Works

```
Lead fills out form (Google Forms)
        │
        ▼
Response logged (Google Sheets)
        │
        ▼
n8n detects new row (Google Sheets Trigger)
        │
        ▼
Contact saved to CRM (Airtable)
        │
        ▼
AI writes personalized email (Gemini API)
        │
        ▼
Email sent automatically (Gmail) ──► Sales rep notified (Gmail)
```

1. **Lead intake** — A lead fills out a simple form with their name, email, company, and what they're interested in.
2. **Trigger** — n8n watches the connected Google Sheet and fires the moment a new response appears.
3. **CRM sync** — The lead is automatically saved (or updated, if they already exist) as a contact in Airtable, with a status of "New."
4. **AI personalization** — Gemini reads what the lead said they're interested in and drafts a short, natural-sounding follow-up email tailored to their specific situation — not a mail-merge template.
5. **Auto-send** — The email is sent immediately via Gmail, without anyone reviewing it first.
6. **Internal notification** — The sales rep receives an email with the lead's full details and a copy of what was sent, so they have complete context for any personal follow-up.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| [Google Forms](https://forms.google.com) | Lead intake form |
| [Google Sheets](https://sheets.google.com) | Stores raw form responses; acts as the trigger source |
| [n8n](https://n8n.io) | Automation engine connecting every step |
| [Airtable](https://airtable.com) | Lightweight CRM for storing and tracking leads |
| [Gemini API](https://ai.google.dev) | Generates the personalized follow-up email |
| [Gmail](https://gmail.com) | Sends the follow-up email and internal notification |

All tools used are free-tier, making this system easy to replicate or adapt without upfront cost.

---

## Setup

### 1. Google Form
Create a form with these fields: Name, Email, Company, and "What are you interested in?" Link it to a Google Sheet under the Responses tab.

### 2. Airtable
Create a base with a `Contacts` table containing these fields: `Name`, `Email`, `Company`, `Interest`, `Status` (single select: New / Contacted).

### 3. n8n Workflow
Import [`lead-capture-auto-followup.json`](./lead-capture-auto-followup.json) into n8n and configure:
- **Google Sheets Trigger** → connect your Google account, select the form's response sheet
- **Airtable - Add Contact** → connect your Airtable personal access token, select your base/table
- **Gemini - Generate Email** → add your Gemini API key
- **Gmail nodes** → connect your Gmail account, set your notification email address

### 4. Activate
Toggle the workflow to **Active** in n8n so it runs automatically in the background rather than requiring manual execution.

---

## Example Output

**Lead submits:**
> Interested in: "We run a Shopify store and want to automate our customer support with AI"

**AI-generated follow-up email:**
> A short, personalized email referencing their Shopify store and support automation needs — signed off warmly, ready to send.

---

## Limitations

This system is built for demonstration and small-scale use. Some things worth knowing before scaling it up:

- Airtable's free tier has record limits — a paid plan or a different CRM would be needed for larger lead volumes.
- Gemini's free tier has rate limits, which can cause delays under high-volume traffic.
- The AI-generated email is sent without human review — for higher-stakes outreach, adding an approval step before sending is recommended.

---

## Possible Improvements

- Add a Slack notification option alongside/instead of email
- Add lead scoring based on the "interest" text before deciding follow-up priority
- Swap Google Sheets/Forms for a dedicated landing page + webhook for a more polished intake experience
- Add a human-in-the-loop approval step before the AI email is sent

---

## About

Built by Hania Khattak as part of a portfolio of AI automation projects. Feel free to fork, adapt, or reach out with questions.

**Connect:** www.linkedin.com/in/haniakhattak · (https://haniakhattak2005.github.io/Portfolio/) · info.haniakhattak@gmail.com
