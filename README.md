<div align="center">

# ParentConnect AI

### A friendly Dialogflow ES foundation for parent-school support

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
