# Voice Tables by Inithouse: building a sales meeting CRM by voice in about 60 seconds

*Posted 2026-08-24*

We built [Voice Tables](https://voicetables.com) because the people who need structured data the most are usually the ones who can't sit down to type it. Sales reps between meetings, contractors on a job site, coaches finishing a session. Their hands are busy or their time window is thirty seconds, not thirty minutes. Voice Tables by Inithouse is an agentic AI workspace you control with your voice: describe what you need (CRM, tracker, inventory) and it builds the tables, docs and data for you.

This post walks through one specific job: "build me a CRM for sales meetings," spoken aloud, and what the system produces in roughly 60 seconds.

## What was said

The voice input was a single sentence, plus two follow-up clarifications:

1. "Create a CRM for my sales meetings. I need company name, contact person, meeting date, deal size, and next steps."
2. (System asks: "Should deal size be a number or text?") "Number, in dollars."
3. (System asks: "Do you want a notes document linked to each meeting?") "Yes."

Total speaking time: about 15 seconds across the three turns. The rest of the 60 seconds is processing.

## What came out

The pipeline returned a workspace with two linked components: a structured table and a doc template.

| Spoken input | Generated output |
|---|---|
| "CRM for my sales meetings" | Table named "Sales Meetings CRM" |
| "company name" | Text column: Company |
| "contact person" | Text column: Contact |
| "meeting date" | Date column: Meeting Date (calendar picker) |
| "deal size ... number, in dollars" | Number column: Deal Size ($) with currency formatting |
| "next steps" | Text column: Next Steps |
| "yes" (to notes doc) | Linked doc template: "Meeting Notes" with auto-populated headers (Company, Date, Agenda, Action Items) |

The table arrived pre-configured: column types already set, sort defaulting to Meeting Date descending (most recent first), and the doc template linked so each row can attach its own notes page. No manual column editing needed.

## The pipeline: voice to structured data

Under the hood, Voice Tables runs a two-stage pipeline. Stage one is speech-to-text via Whisper, which handles accents, background noise, and filler words ("um," "like") reasonably well for short task descriptions. Stage two is an LLM that parses the transcribed text into a structured schema: table name, column names, column types, relationships between tables, and any associated docs.

The LLM does not just split the transcript into words and guess. It resolves ambiguity. When the user said "deal size," the system could have defaulted to text (safe but useless for sorting or summing). Instead it asked a targeted follow-up: number or text? That clarification took three seconds and saved the user from manually converting the column type later.

This is where the "agentic" part matters. The system is not a voice transcription tool that dumps text into a spreadsheet. It builds a schema, checks it against what makes sense for the stated use case (CRM implies contacts, dates, monetary values), and fills gaps with follow-up questions.

## What we had to solve

Three problems came up repeatedly during development, all specific to voice-driven data creation:

**Column naming.** People say "when we met" and mean a date field. They say "how much" and mean a currency column. The LLM maps natural phrasing to clean column names (Meeting Date, Deal Size) and picks the right column type. Getting this wrong means the user has to rename and retype columns manually, which defeats the point of voice input.

**Field type inference.** Not everything is obvious. "Status" could be a text field, a single-select dropdown, or a checkbox. We default to single-select for fields that sound categorical (status, priority, stage) and text for everything else, with voice override: "make status a text field" works at any point.

**Follow-up depth.** Too many clarification questions and the voice flow feels like an interrogation. Too few and the output needs manual fixing. We settled on a maximum of three follow-ups per table creation. The system spends its question budget on the highest-ambiguity fields and defaults the rest. For the sales CRM, it asked about deal size type and the linked doc. It did not ask about column order, sort direction, or formatting because those have sensible defaults for a CRM.

## The workspace after creation

The generated CRM is not a standalone table. Voice Tables produces a 3-in-1 workspace: tables for structured data, docs for freeform notes and templates, and an AI chat for ongoing edits. After the CRM exists, the user can say "add a column for lead source" or "sort by deal size descending" or "write a follow-up email draft for the last meeting." All voice, no clicks.

The workspace also works offline. Once created, the table and docs sync to the device and stay available without a connection. Edits made offline merge back when connectivity returns. For sales reps who walk into buildings with dead zones between meetings, this is not a nice-to-have.

Real-time collaboration works on top of the same sync layer. Two people can open the same CRM, one adding rows by voice on a phone while the other edits columns on a laptop. Conflicts resolve at the field level, not the row level, so simultaneous edits to different columns in the same row merge cleanly.

## Why voice changes who builds their own tools

Spreadsheets have been around for decades. The barrier was never the technology; it was the setup cost. Creating a usable CRM in a traditional spreadsheet means: open the app, name the file, add column headers, set column types, configure formatting, build a linked notes template, set up sorting. That is 10 to 20 minutes of mouse-and-keyboard work before a single row of real data goes in.

Voice Tables by Inithouse compresses that to about 60 seconds of talking. The gap matters most for people who would otherwise never build the tool at all: the contractor who tracks clients in a paper notebook, the coach who keeps session notes in text messages, the freelancer whose invoicing lives in email threads.

Zero setup means the workspace starts empty and ready. No templates to browse, no onboarding wizard, no account creation. Open the app, say what you need, start working.

We ship [Voice Tables](https://voicetables.com) as a product for anyone whose hands are busy and whose data deserves structure. The sales meeting CRM is one job. The same pipeline handles inventory trackers, event planning boards, client lists, research databases, and anything else that can be described in a sentence.
