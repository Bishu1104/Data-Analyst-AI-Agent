# 🤖 Data Analyst AI Agent

> **An AI-powered data analyst agent built with n8n, Anthropic Claude, Google Sheets, and Gmail — ask questions in natural language, get data-backed insights, and email professional reports on demand.**

[![n8n](https://img.shields.io/badge/Workflow-n8n-orange?style=for-the-badge)](https://n8n.io/)
[![Anthropic](https://img.shields.io/badge/LLM-Claude%20Haiku-blueviolet?style=for-the-badge)](https://www.anthropic.com/)
[![Google Sheets](https://img.shields.io/badge/Data-Google%20Sheets-green?style=for-the-badge)](https://www.google.com/sheets/about/)
[![Gmail](https://img.shields.io/badge/Reports-Gmail-red?style=for-the-badge)](https://www.gmail.com/)

## 📌 Overview

**Data Analyst AI Agent** is an agentic analytics workflow that lets users interact with spreadsheet data through a conversational interface instead of manually writing formulas or repeatedly building reports.

The agent receives a natural-language question, retrieves the latest rows from a connected Google Sheet, analyzes the available data using an LLM, and returns a concise business-oriented response. When requested, it can also convert the analysis into a structured HTML email and send the report through Gmail.

The workflow is designed around a simple principle:

**Ask → Retrieve → Analyze → Explain → Report**

## ✨ Key Features

- 💬 **Natural-language analytics** — ask questions such as *“Which industry has the highest average valuation?”* or *“Summarize the major trends in the dataset.”*
- 📊 **Live Google Sheets access** — the agent retrieves the latest spreadsheet data before answering data-related questions.
- 🧠 **LLM-powered reasoning** — uses an Anthropic chat model to interpret questions and turn raw rows into useful insights.
- 🧩 **Tool-using AI agent** — the model can decide when to use connected tools rather than relying only on its conversational context.
- 📝 **Conversational memory** — maintains a short context window so follow-up questions can build on the previous interaction.
- 📧 **Automated email reporting** — users can request an analysis/report to be formatted as HTML and delivered through Gmail.
- ✅ **Data-grounded responses** — the workflow instructs the agent to fetch spreadsheet data instead of guessing or hallucinating values.
- ⚡ **Low-code / no-code architecture** — the complete workflow is orchestrated in n8n and can be imported as a JSON workflow.

## 🏗️ Architecture

![Data Analyst AI Agent Workflow](./Analysis%20AI%20Agent%20Workflow.png)

### Workflow Components

```text
┌──────────────────────────┐
│   User sends a message   │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│   n8n Chat Trigger       │
└────────────┬─────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│            AI Agent                 │
│                                     │
│  Anthropic Claude + Short Memory    │
│                                     │
│  ┌────────────────┐  ┌───────────┐ │
│  │ Google Sheets  │  │   Gmail   │ │
│  │  Read Data     │  │ Send Report│ │
│  └────────────────┘  └───────────┘ │
└─────────────────────────────────────┘
             │
             ▼
┌──────────────────────────┐
│   Insight / Report       │
└──────────────────────────┘
```

## 🔄 How It Works

### 1. Receive the question

The n8n chat trigger starts the workflow whenever a user sends a message.

### 2. Understand the request

The AI Agent interprets the user's intent and determines whether spreadsheet data is required.

### 3. Retrieve the latest data

For data-related questions, the agent invokes the **Google Sheets tool** to read the current rows from the configured spreadsheet.

### 4. Analyze the data

Claude processes the retrieved information and produces an explanation focused on the user's question. The system prompt explicitly instructs the agent not to invent values when data is required.

### 5. Respond conversationally

The user receives a concise answer in the chat interface, with the agent briefly explaining what it analyzed.

### 6. Generate an email report when requested

When the user asks for an email/report, the agent prepares an HTML-formatted message with headings, bullet points, and highlighted figures, then passes it to the Gmail tool.

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| **n8n** | Workflow orchestration and agent tooling |
| **Anthropic Claude Haiku 4.5** | Natural-language understanding and reasoning |
| **Google Sheets** | Source for structured analytical data |
| **Gmail** | Delivery of generated reports |
| **n8n Simple Memory** | Short conversational context |
| **JSON** | Portable n8n workflow definition |
| **CSV** | Sample dataset and data dictionary |

## 📂 Repository Structure

```text
Data-Analyst-AI-Agent/
│
├── AI Agent n8n.json
│   └── Complete n8n workflow export
│
├── Analysis AI Agent Workflow.png
│   └── Workflow architecture screenshot
│
├── Data_Dictionary.csv
│   └── Definitions of the dataset fields
│
├── Unicorn_Companies.csv
│   └── Sample unicorn-company dataset
│
└── README.md
    └── Project documentation
```

The sample dataset contains fields including **Company, Valuation, Date Joined, Industry, City, Country, Continent, Year Founded, Funding, and Select Investors**.

## 🚀 Getting Started

### Prerequisites

Before importing the workflow, make sure you have:

- An **n8n** instance (cloud or self-hosted)
- An **Anthropic API / model connection** available in n8n
- A **Google account** with access to Google Sheets
- A **Gmail account** connected to n8n
- A spreadsheet containing the data you want the agent to analyze

### 1. Clone the repository

```bash
git clone https://github.com/Bishu1104/Data-Analyst-AI-Agent.git
cd Data-Analyst-AI-Agent
```

### 2. Import the n8n workflow

1. Open your n8n workspace.
2. Create a new workflow.
3. Choose **Import from File**.
4. Select `AI Agent n8n.json`.
5. Reconnect your own Google Sheets, Gmail, and Anthropic credentials.

> **Important:** The exported workflow is tied to the original node configuration. Replace the connected resources and credentials with your own before activating it.

### 3. Connect your Google Sheet

Configure the Google Sheets tool to point to your own workbook and the sheet containing your analytical data.

For the included sample project, the sheet is based on the **Unicorn Companies** dataset.

### 4. Connect Gmail

Authorize the Gmail node with your own Google account. The workflow can then generate and send formatted analysis reports when requested.

### 5. Configure the AI model

The included workflow uses **Anthropic Claude Haiku 4.5** as its chat model. You can adapt the model node in n8n if you want to use another compatible LLM.

### 6. Activate and test

Once credentials and data sources are connected, activate the workflow and send questions through the n8n chat interface.

## 💡 Example Queries

Try questions like:

```text
Which industry has the highest number of unicorn companies?
```

```text
Which countries have the most unicorn companies?
```

```text
Summarize the key patterns in the dataset.
```

```text
Which companies have the highest valuations?
```

```text
Prepare a concise analysis of the dataset and email me the report.
```

For follow-up analysis, you can also ask conversational questions such as:

```text
What about the top 5 industries?
```

## 📧 Email Reporting

One of the core features of the agent is turning analysis into a business-ready email.

When an email is requested, the workflow is designed to:

1. Fetch the relevant data.
2. Analyze the requested metric or question.
3. Generate a structured HTML report.
4. Send the report through Gmail.
5. Confirm the action in the chat interface.

The email format uses simple HTML elements such as headings, paragraphs, lists, and highlighted numbers so the final report is easy to scan.

## 🧠 Agent Design Principles

### Data first, answer second

The system prompt instructs the agent to retrieve spreadsheet data whenever the user's question depends on the dataset. This reduces the risk of responding from assumptions rather than current data.

### Tool-aware reasoning

The AI Agent is connected to external tools for **data retrieval** and **report delivery**, allowing the LLM to choose actions based on the user's request.

### Human-readable outputs

The workflow is optimized for business users: users can ask questions in plain English and receive explanations without needing to write SQL, Python, or spreadsheet formulas.

### Reusable workflow

Although the repository includes a unicorn-company dataset, the underlying workflow can be adapted to many spreadsheet-based analytics use cases such as sales, finance, operations, marketing, HR, customer analytics, and reporting.

## 🔐 Security Notes

- **Do not commit API keys, OAuth secrets, access tokens, or private credentials to GitHub.**
- Use your own n8n credential connections when importing this workflow.
- Review the Google Sheet and Gmail destination before activating the workflow.
- The sample workflow contains configuration metadata from the exported n8n workflow; treat exported workflow files as configuration artifacts and review them before sharing in production environments.
- For real business datasets, follow your organization's privacy, access-control, and data-retention policies.

## 📈 Possible Improvements

Future iterations could extend the agent with:

- Automatic chart generation and visualization
- SQL/database connectors such as PostgreSQL or MySQL
- CSV/Excel upload support
- Automated KPI dashboards
- Scheduled daily or weekly analytics reports
- Multi-agent workflows for validation, analysis, and report writing
- Data-quality checks for missing values, duplicates, and inconsistent types
- Approval steps before external emails are sent
- Better observability, logging, and evaluation of agent responses

## 🎯 Why This Project Matters

Traditional reporting often requires an analyst to repeatedly extract data, perform calculations, interpret the results, and manually prepare an email or presentation.

This project demonstrates how **agentic AI + workflow automation + business data** can compress that process into a conversational interface while still grounding the analysis in an external data source.

It is a practical example of combining:

**LLMs + Tool Calling + Data Analytics + Workflow Automation + Business Reporting**

## 👨‍💻 Author

**Bishwjit Kumar**

- GitHub: [@Bishu1104](https://github.com/Bishu1104)
- Project: [Data-Analyst-AI-Agent](https://github.com/Bishu1104/Data-Analyst-AI-Agent)

## ⭐ Show Your Support

If you find this project useful or interesting, consider giving the repository a ⭐ and sharing feedback or improvements through GitHub Issues or pull requests.

---

**Built with n8n + Claude + Google Sheets + Gmail**
