<div align="center">

# ParentConnect AI

### A friendly Dialogflow ES foundation for parent-school support
## chatbot link:## https://kavin-beep.github.io/SA-chatbot/

<a href="https://github.com/kavin-beep/SA-chatbot">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=2563EB&center=true&vCenter=true&width=720&lines=ParentConnect+AI;Dialogflow+ES+Chatbot+Prototype;Connecting+Parents+and+Schools;Ready+to+Import+and+Build+Upon" alt="Animated ParentConnect AI project information" />
</a>

[![Dialogflow ES](https://img.shields.io/badge/Dialogflow-ES-FF9800?logo=dialogflow&logoColor=white)](https://cloud.google.com/dialogflow/es/docs)
[![Language](https://img.shields.io/badge/language-English-2563EB)](#current-capabilities)
[![Status](https://img.shields.io/badge/status-starter_agent-22C55E)](#project-status)

**Clear questions. Helpful guidance. Stronger school connections.**

</div>

---

## Overview

ParentConnect AI is a starter chatbot built with **Google Dialogflow ES**. This repository preserves the original chatbot export and provides a clean base for a parent-support assistant that can later answer school questions, guide families to resources, and improve communication between parents and the school.

The repository contains a Dialogflow ES agent export. It is not a Node.js application, and `package.json` is included only because it is part of the Dialogflow export format.

## Current capabilities

- Uses the original Dialogflow welcome responses.
- Recognizes common English greetings.
- Uses the original Dialogflow fallback responses for unmatched questions.
- Preserves the original exported agent configuration.
- Contains no API keys, service-account files, or project credentials.

> [!IMPORTANT]
> This is an early-stage agent. It currently contains only the welcome and fallback intents; school-specific answers still need to be added.

## Project structure

```text
SA-chatbot/
├── agent.json
├── package.json
├── intents/
│   ├── Default Fallback Intent.json
│   ├── Default Welcome Intent.json
│   └── Default Welcome Intent_usersays_en.json
├── .gitignore
└── README.md
```

## Download and Import

You can download the Dialogflow zip file containing all intents and entities from this repository and import them directly into your Dialogflow ES agent:

1. **Download the ZIP file** from this repository containing `agent.json`, `package.json`, and the `intents/` directory.
2. Navigate to the [Dialogflow ES console](https://dialogflow.cloud.google.com/).
3. Go to **Settings → Export and Import**.
4. Use **Import from ZIP** to merge the intents and entities into your existing agent, or **Restore from ZIP** to replace the current draft with this agent.

This approach allows you to quickly import all pre-configured intents and entities without manual setup.

## Import into Dialogflow ES

1. Download or clone this repository.
2. Create a ZIP containing `agent.json`, `package.json`, and the `intents` directory at the ZIP root.
3. Open the [Dialogflow ES console](https://dialogflow.cloud.google.com/).
4. Select or create an agent.
5. Open **Settings → Export and Import**.
6. Choose **Import from ZIP** to merge the files, or **Restore from ZIP** to replace the current draft.
7. Train the agent, then test greetings and unknown questions in the simulator.

> [!CAUTION]
> **Restore from ZIP** overwrites the current agent draft. Export a backup first if the target agent already contains work.

## Test checklist

After importing, verify the following:

- `hello` triggers **Default Welcome Intent**.
- An unrelated phrase triggers **Default Fallback Intent**.
- All responses are shown in English.
- The imported settings match the original agent export.
- Dialogflow reports no validation or training errors.

## Suggested next intents

| Intent | Example questions |
| --- | --- |
| School timings | "What time does school start?" |
| Attendance | "How do I report an absence?" |
| Events | "What events are coming up?" |
| Fees | "Where can I find fee information?" |
| Transport | "Who do I contact about the school bus?" |
| Human support | "I need to speak with the school office." |

## Try it / Add a test link

If you'd like visitors to test the chatbot from a web page (rather than opening the Dialogflow console), you have two common options:

1) Use Dialogflow's built-in web integrations (recommended)

- In the Dialogflow ES console, open **Integrations** for your agent.
- Enable **Dialogflow Messenger** or **Web Demo** (the console provides both an embed snippet and, in some cases, a sharable demo URL).
- Copy the provided HTML snippet and paste it into a simple static page (for example, a GitHub Pages site). GitHub Pages can host your demo for free.

Example Dialogflow Messenger snippet (paste into an HTML page and replace PROJECT_ID with your Google Cloud project id):

```html
<!-- Dialogflow Messenger embed (Dialogflow ES) -->
<script src="https://www.gstatic.com/dialogflow-console/fast/messenger/bootstrap.js?v=1"></script>
<df-messenger
  intent="WELCOME"
  chat-title="ParentConnect"
  agent-id="PROJECT_ID"
  language-code="en"
></df-messenger>
```

2) Link to the Dialogflow console simulator (developer-only)

- The Dialogflow console simulator is convenient for testing but requires users to have access to the Google Cloud project or to be added as collaborators. If you only want internal testers (school staff or developers), you can link them to the Dialogflow console and ask them to open the simulator for your agent.

Notes and privacy

- If you host a public demo, be cautious about collecting or logging sensitive student information. Review your Dialogflow interaction log settings and GDPR/FERPA requirements before making the agent publicly accessible.
- Do not publish service account keys or private credentials in the demo site.

# ParentConnect AI — Dialogflow ES Agent

A Dialogflow ES agent that acts as a demo parent–school communication assistant. Parents can check a (fictional) student's attendance and exam results, look up exam schedules, announcements, fees, transport, and school contact info — all through natural language or by tapping quick-reply chips.

> ⚠️ **Demo data notice:** All student names, IDs, grades, and records (Student A/B/C, `PC1001`–`PC1003`, `DEMO-6001` etc.) are fictional placeholders for prototyping. Replace with a real backend/webhook before production use.

---

## Table of Contents

- [Agent Configuration](#agent-configuration)
- [Entities](#entities)
- [Intents](#intents)
  - [Core Navigation](#core-navigation)
  - [Student Profile Flow](#student-profile-flow)
  - [Attendance Flow](#attendance-flow)
  - [Exam Results Flow](#exam-results-flow)
  - [Exam Schedule Flow](#exam-schedule-flow)
  - [Announcements Flow](#announcements-flow)
  - [School Info](#school-info)
  - [Admin / Contact](#admin--contact)
- [Sub-Intents (Follow-up Intents)](#sub-intents-follow-up-intents)
- [Contexts (Conversation State)](#contexts-conversation-state)
- [Option Replies (Quick Replies)](#option-replies-quick-replies)
- [Custom Payloads (Rich Content)](#custom-payloads-rich-content)
- [Importing This Agent](#importing-this-agent)
- [Known Issues / Notes](#known-issues--notes)

---

## Agent Configuration

Defined in `agent.json`:

| Setting | Value |
|---|---|
| Display name | `ParentConnect_AI` |
| Default timezone | `Asia/Kolkata` |
| ML min confidence | `0.3` |
| Webhook | **Enabled** → `https://parentconnect-scope-guard.ak67123.chatgpt.site/api/webhook` |
| Spell correction | Disabled |
| Knowledge base | Not used |

Only `Default Fallback Intent` has `webhookUsed: true` in this export — every other intent responds with static Dialogflow messages (no live backend calls yet). Wire up the other intents' `webhookUsed` flag once your fulfillment logic covers them.

---

## Entities

14 custom entities live in `entities/`. Each is a plain **enum-style** entity (`isEnum: false` synonym list, not regex, no automated expansion).

| Entity | Values |
|---|---|
| `@student-profile` | Student A, Student B, Student C *(+ synonyms: profile a/b/c, DEMO-6001/8002/1103, 6001/8002/1103)* |
| `@student-name` | Aarav Sharma, Maya Patel, Rohan Das |
| `@student-id` | PC1001, PC1002, PC1003 |
| `@grade` | Grade 6 – Grade 12 *(synonyms: class N, year N, standard N)* |
| `@section` | A, B, C |
| `@subject` | Mathematics, English, Science, Social Studies, Computer Science, Physics, Chemistry, Biology |
| `@term` | Term 1, Term 2, Term 3 |
| `@exam-type` | Unit Test, Midterm, Final |
| `@fee-type` | Tuition, Transport, Activities, Examination |
| `@announcement-category` | Academic, General, Event, Urgent |
| `@event-type` | Sports Day, Parent-Teacher Meeting, Cultural Day, Science Fair |
| `@transport-route` | Route A, Route B, Route C |
| `@school-department` | Administration, Accounts, Admissions, Transport, Student Support |
| `@contact-method` | Phone, Email, Callback, Appointment |

Each entity's synonym list also holds casual phrasing users might type — e.g. `@grade` matches "grade 10", "class 10", "year 10", and "standard 10" all to the canonical value `Grade 10`; `@fee-type`'s `Tuition` also matches "school fees" and "term fees".

Entities are referenced inside intent parameters as `@entity-name`, and inside training phrases / responses as `$parameter_name` (see examples below).

---

## Intents

47 intents total (2 are Dialogflow defaults). Grouped by feature area:

### Core Navigation
| Intent | Purpose |
|---|---|
| `Default Welcome Intent` | Fires on `WELCOME` event. Greets the parent and shows the main menu chips. |
| `Main Menu Intent` | Resets context and returns to the home menu from anywhere. |
| `Help Intent` | Lists what the bot can do. |
| `Default Fallback Intent` | Catches unrecognized input (only intent with webhook enabled). |
| `Feedback Intent` | Collects a quick thumbs-up/down style reaction. |
| `Goodbye Intent` | Ends the conversation. |

### Student Profile Flow
| Intent | Purpose |
|---|---|
| `Choose Student Profile` | Asks which demo profile (A/B/C) to load. |
| `Choose Student Profile - Student A/B/C` | Follow-ups — loads the chosen profile and opens `student-{a,b,c}-active` context. |
| `Student Verification Intent` | Alternate entry point — verify by `@student-name` + `@student-id` instead of picking a profile letter. |

### Attendance Flow
| Intent | Purpose |
|---|---|
| `Attendance Intent` | Asks which student to check attendance for. |
| `Attendance Intent - Student A/B/C` | Follow-ups — returns attendance for the named student. |
| `Selected Student A/B/C - Attendance` | Fires when a student profile is *already active* (context) and the parent just says "attendance" — skips the re-selection step. |

### Exam Results Flow
| Intent | Purpose |
|---|---|
| `Exam Results Intent` | Asks which student to check results for. |
| `Exam Results Intent - Student A/B/C` | Follow-ups — returns exam results for the named student. |
| `Selected Student A/B/C - Exam Results` | Context-shortcut version, same idea as attendance above. |

### Exam Schedule Flow
| Intent | Purpose |
|---|---|
| `Exam Schedule Intent` | Asks which grade's exam schedule to show. |
| `Exam Schedule Intent - Grade 6` … `Grade 12` | 7 follow-ups, one per grade, each returning that grade's schedule. |

### Announcements Flow
| Intent | Purpose |
|---|---|
| `Announcements Intent` | Asks which announcement category (Academic / General / Event / Urgent). |
| `Announcements Intent - Academic / General / Event / Urgent` | Follow-ups — returns the announcement text + a "card" message for that category. |

### School Info
| Intent | Purpose |
|---|---|
| `School Timings Intent` | School open/close hours. |
| `Holiday List Intent` | Upcoming holidays. |
| `School Events Intent` | Details for a chosen `@event-type` (date/time/venue). |
| `School Event Intent` | ⚠️ Near-duplicate of the above — see [Known Issues](#known-issues--notes). |
| `Transport Intent` | Bus route info for a chosen `@transport-route`. |

### Admin / Contact
| Intent | Purpose |
|---|---|
| `Admission Enquiry Intent` | New-admission info for a given `@grade`. |
| `School Contact Intent` | Routes to the right `@school-department`. |
| `Teacher Contact Intent` | Requests a teacher contact by `@grade` + `@section` + `@subject` + `@contact-method`. |
| `Fee Details Intent` | Fee summary for `@grade` + `@term`. |
| `Fee Deadline Intent` | Due date for a `@fee-type` + `@term`. |

---

## Sub-Intents (Follow-up Intents)

This agent makes heavy use of Dialogflow's **follow-up intent** pattern: a parent intent asks a question, and its children only trigger while that parent's output context is still active. In the raw JSON this shows up as `parentId` / `rootParentId` fields on the child, plus a matching input context.

Example — `Choose Student Profile` → `Choose Student Profile - Student A`:

```jsonc
// Choose Student Profile.json (parent)
{
  "name": "Choose Student Profile",
  "responses": [{
    "affectedContexts": [
      { "name": "choose-student-followup", "lifespan": 2 }
    ]
  }]
}

// Choose Student Profile - Student A.json (child)
{
  "name": "Choose Student Profile - Student A",
  "parentId": "505d1976-c9ee-4f09-860a-0866d4f6eb95",
  "rootParentId": "505d1976-c9ee-4f09-860a-0866d4f6eb95",
  "contexts": ["choose-student-followup"],   // ← only listens while this context is live
  "responses": [{
    "affectedContexts": [
      { "name": "student-a-active", "lifespan": 8 }  // ← opens the NEXT stage's context
    ],
    "parameters": [
      { "name": "student_profile", "dataType": "@student-profile" }
    ]
  }]
}
```

All follow-up families in this agent, and the context each parent opens for its children:

| Parent Intent | Opens Context | Children |
|---|---|---|
| `Choose Student Profile` | `choose-student-followup` (2) | Student A / B / C |
| `Attendance Intent` | `attendance-followup` (2) | Student A / B / C |
| `Exam Results Intent` | `results-followup` (2) | Student A / B / C |
| `Exam Schedule Intent` | `exam-schedule-followup` (2) | Grade 6 … Grade 12 (×7) |
| `Announcements Intent` | `announcements-followup` (2) | Academic / General / Event / Urgent |

A second, independent chain then keeps the conversation "in character" for whichever student was picked — see below.

---

## Contexts (Conversation State)

Contexts are how the agent remembers *what stage* the conversation is in and *which student* is active, without a database. The important long-lived one is `student-{a,b,c}-active` (lifespan **8** turns), which is opened by profile selection and re-opened by every subsequent attendance/results answer for that student — this is what lets the parent just say "attendance" a few turns later and get routed straight to `Selected Student A - Attendance` instead of being asked to pick a profile again.

| Context | Lifespan | Set by | Read by |
|---|---|---|---|
| `welcome-followup` | 5 | Default Welcome Intent | — |
| `choose-student-followup` | 2 | Choose Student Profile | Choose Student Profile - Student A/B/C |
| `attendance-followup` | 2 | Attendance Intent | Attendance Intent - Student A/B/C |
| `results-followup` | 2 | Exam Results Intent | Exam Results Intent - Student A/B/C |
| `exam-schedule-followup` | 2 | Exam Schedule Intent | Exam Schedule Intent - Grade 6…12 |
| `announcements-followup` | 2 | Announcements Intent | Announcements Intent - Academic/General/Event/Urgent |
| `student-a-active` / `-b-` / `-c-` | 8 | Choose/Attendance/Results intents for that student | Selected Student A/B/C - Attendance & - Exam Results |
| `grade-6-active` … `grade-12-active` | 6 | Exam Schedule Intent - Grade N | — (reserved for future use) |
| `admissions-active`, `fees-active`, `event-active`/`event-followup`, `transport-active`, `school-contact-active`, `teacher-contact-active`, `student-verified` | 5–6 | their respective top-level intent | — (reserved for future multi-turn use) |

---

## Option Replies (Quick Replies)

Every non-fallback response includes a **type `"2"`** message — Dialogflow's native "Quick Replies" — a row of tappable buttons rendered on supported channels (Dialogflow Messenger, Google Assistant chips, etc.).

```jsonc
{
  "type": "2",
  "title": "Choose an option",
  "replies": ["Choose student", "Attendance", "Exam schedule", "Announcements"]
}
```

- Each string in `replies` is literally what gets sent back to the agent as user input when tapped — so they should also exist as (or closely match) training phrases somewhere.
- Almost every intent ends its options with a way back out — usually `"Main menu"` or `"Choose another"` — so parents are never stuck in a dead-end branch.

---

## Custom Payloads (Rich Content)

Alongside the quick replies, nearly every response also includes a **type `"4"`** custom payload using Dialogflow's `richContent` "chips" format. This is what actually renders as clickable pill-shaped buttons in the **Dialogflow Messenger** web widget (the type `"2"` quick replies above are the fallback for platforms that don't support `richContent`):

```jsonc
{
  "type": "4",
  "payload": {
    "richContent": [
      [
        {
          "type": "chips",
          "options": [
            { "text": "Choose student" },
            { "text": "Attendance" },
            { "text": "Exam schedule" },
            { "text": "Announcements" }
          ]
        }
      ]
    ]
  }
}
```

`richContent` is an array of **rows**, each row an array of **elements** — so you can stack multiple content types (text, image, chips, cards) in one bubble by adding more rows/elements. This agent only uses a single `chips` row per response, mirroring the type `2` options exactly.

**One additional payload type shows up only in the Announcements sub-intents** — a type `"1"` **Card** message, giving those responses a title + subtitle in addition to the plain text bubble:

```jsonc
{
  "type": "1",
  "title": "📢 Academic notice",
  "subtitle": "ParentConnect demo bulletin"
}
```

### Message type reference
| Type | Meaning | Used in |
|---|---|---|
| `0` | Plain text (supports multiple variants, chosen at random) | Every intent |
| `1` | Card (title + subtitle) | 4 Announcements sub-intents only |
| `2` | Quick Replies | Every non-fallback intent |
| `4` | Custom Payload → `richContent` chips | Every non-fallback intent except `School Event Intent` and `Student Verification Intent` |

---

## Importing This Agent

1. Zip the contents of this repo (`agent.json`, `package.json`, `intents/`, `entities/` at the top level — not nested in a subfolder).
2. Dialogflow ES Console → **⚙️ Agent Settings** → **Export and Import** → **Restore from ZIP**.
3. Re-connect the webhook URL under **Fulfillment** if you want `Default Fallback Intent` (or any intent you flip `webhookUsed` on) to hit your backend instead of static responses.

---

## Known Issues / Notes

- **`School Event Intent` vs `School Events Intent`** — these two intents overlap almost completely (both key off `@event-type`, both open an event-related context, both have similar training phrases). This looks like a leftover draft; recommend merging into `School Events Intent` and deleting the singular one to avoid intent-matching ambiguity.
- **`School Event Intent` and `Student Verification Intent`** are the only two non-fallback intents missing the type `4` rich-content chips — they only send type `2` quick replies. Add a matching `richContent` block if you want consistent button rendering in the Dialogflow Messenger widget.
- **Reserved-but-unused contexts** — `grade-N-active`, `admissions-active`, `fees-active`, `event-active`, `transport-active`, `school-contact-active`, `teacher-contact-active`, and `student-verified` are all set but currently have no follow-up intents reading them. They're presumably scaffolding for a future turn (e.g. "remind me before the deadline") — safe to leave, but worth knowing they're inert today.
- **Webhook fulfillment** is configured at the agent level but only toggled on for `Default Fallback Intent`. All the "real" data (attendance %, results, fee amounts, etc.) is currently hard-coded demo text inside each intent's response — swap these for webhook calls once a real student-records backend exists.

## Project status

The original chatbot files are preserved and ready for import. The next milestone is to add verified school content, training phrases, and a safe handoff path to a staff member.

## Privacy and safety

- Do not commit service-account JSON files, API keys, access tokens, or student records.
- Avoid collecting sensitive student information through free-text messages.
- Use verified school sources for answers and provide a human contact for high-impact questions.
- Review Dialogflow interaction-log settings against the school's privacy requirements before deployment.

## Contributing

When adding an intent, include varied training phrases, concise responses, and a fallback or human-support path where appropriate. Test the agent in Dialogflow ES before exporting an updated version.

---

<div align="center">

Built to make parent-school communication simpler and more accessible.

</div>
