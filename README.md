# Meridian Firm Intelligence — Demo Starter Kit

A starter repo for **vibe-coding an agentic prototype** against the Meridian Advisory Group case study, using **GitHub Copilot**.

The goal is to get *something working*, such as an agent that does something useful based on the case-study information, quickly enough that you can show it, learn from it, and iterate. This repo gives you the raw materials and a working Foundry agent example. What you build on top is wide open.

---

## The scenario summary

Meridian Advisory Group is a 400-person consulting firm losing deals to faster, AI-native competitors. Their institutional knowledge lives in people's heads, engagement health is invisible until it's a write-down, and proposals take 3–4 weeks to produce. The full case study is in:

📄 **[`PROSERVE_Meridian_FirmIntelligence_UseCase.docx`](PROSERVE_Meridian_FirmIntelligence_UseCase.docx)**

Your job is to design and stand up an **agentic** solution that helps. Demos may use **Microsoft Foundry** or **Copilot Studio** for the agent, grounded in one or more of the three **Microsoft IQs**. Sample synthetic data is included, but you may choose to generate your own.

---

## What's in the box

```
.
├── PROSERVE_Meridian_FirmIntelligence_UseCase.docx   # the case study
├── example/
│   └── sample-basic-agent.py                         # a working Foundry prompt-agent
└── sample-data/
    ├── work-iq/      # M365 work context
    ├── foundry-iq/   # the firm's institutional knowledge  
    └── fabric-iq/    # structured business data 
```

### Microsoft IQ: Pick one or more

| Source | What's in it | How to use it |
|---|---|---|
| **`work-iq/`** | An inbound RFP email + a calendar invite | Copy and paste the email body and send to yourself. Use the calendar invite body text in a mock meeting invite. |
| **`foundry-iq/`** | Firm knowledge as documents: methodology, case studies, past proposals, team bios, style guide, pricing, industry briefs, client references | Index the documents in Azure AI Search, and create a Foundry IQ Knowledge Base over your index(es). GitHub Copilot can help! |
| **`fabric-iq/`** | Structured tables (CSV): clients, consultants, engagements, assignments, utilization, opportunities, proposals | Import the data into Fabric using Data Factory, or ask GitHub Copilot to help you. |

You don't need all three. A sharp demo that does *one* thing well beats a sprawling one that half-works. 

---

## Quick start

You'll build with **GitHub Copilot inside VS Code**, so once it's set up you can paste the *"Prefer to let Copilot handle it?"* prompts into GitHub Copilot Chat, and let it do the heavy lifting. Commands are shown for **Windows**; macOS is in the drop-downs.

<details>
<summary><b>Already a developer?</b> Here's the whole Quick start in one block.</summary>

Assumes VS Code + the **GitHub Copilot** extension, **Python 3.11+**, and the **Azure CLI** are already installed.

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1          # macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
az login
```

Copy `sample.env` to `.env`, fill in the two values, then jump to [Building with GitHub Copilot](#building-with-github-copilot):

```powershell
copy sample.env .env          # macOS/Linux: cp sample.env .env
```
</details>


### 1. Install VS Code and GitHub Copilot


1. Download and install **[VS Code](https://code.visualstudio.com/)**.
2. Open it, click the **Extensions** icon on the left (or press `Ctrl+Shift+X`).
3. Search for **GitHub Copilot**, click **Install**, and **Sign in** with your GitHub account.
4. Open this folder: **File → Open Folder**, and pick where you saved this repo.
5. Open the Copilot Chat panel (speech-bubble icon). At the top is a mode selector — **Ask / Plan / Agent** — referenced throughout this README.

### 2. Install Python and the Azure CLI

These are the tools the demo agent needs to run. On **Windows**, open PowerShell and run:

```powershell
winget install Python.Python.3.12
winget install Microsoft.AzureCLI
```

<details>
<summary>macOS (using <a href="https://brew.sh">Homebrew</a>)</summary>

```bash
brew install python azure-cli
```
</details>

Close and reopen your terminal afterward so the new tools are picked up.

> Prefer to let Copilot handle it? Paste this into Copilot Chat:
>
> ```
> Check whether Python 3.11+ and the Azure CLI are installed. If either is missing, install it for my operating system and confirm the versions.
> ```

### 3. Set up the project

This makes an isolated space for the demo's dependencies and installs them. On **Windows**:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

<details>
<summary>macOS</summary>

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```
</details>

> Prefer to let Copilot handle it? Paste this into Copilot Chat:
>
> ```
> Create a Python virtual environment in .venv, activate it, and install the dependencies from requirements.txt. 
> ```

### 4. Connect to Azure and Foundry

Sign in to Azure (a browser window will open):

```powershell
az login
```

Then you need a Foundry project with a deployed model. Save the provided **`sample.env`** to a new file named **`.env`**:

```powershell
copy sample.env .env
```

<details>
<summary>macOS</summary>

```bash
cp sample.env .env
```
</details>

Open `.env` and fill in the two values:

```
FOUNDRY_PROJECT_ENDPOINT=<from the Overview page of your Foundry project>
FOUNDRY_MODEL_NAME=<your deployed model name, e.g. gpt-5.1>
```

> Prefer to let Copilot handle it? Paste this into Copilot Chat:
>
> ```
> Sign me in to Azure, then provision a Microsoft Foundry resource and project, with a deployed chat model, on my current subscription. Then create a .env file in the repo root with FOUNDRY_PROJECT_ENDPOINT set to the project endpoint and FOUNDRY_MODEL_NAME set to the deployment name. 
> ```

You're set up. Head to [Building with GitHub Copilot](#building-with-github-copilot) to start.

**Note:** You don't need to run [`example/sample-basic-agent.py`](example/sample-basic-agent.py). It's a reference implementation of a Foundry agent as reference for GitHub Copilot.

---

## Building with GitHub Copilot

Below are **starter prompts** to get moving. Edit them freely or use your own.

### Get oriented

> Ask mode:
> ```
> Read PROSERVE_Meridian_FirmIntelligence_UseCase.docx and the files under sample-data/. Summarize the business problem, then suggest 3 small agentic demos I could build in an hour, each using a different mix of the work-iq / foundry-iq / fabric-iq data. For each, say what the agent does,which data it touches, and the single "wow" moment.
> ```

> Ask mode:
> ```
> Read PROSERVE_Meridian_FirmIntelligence_UseCase.docx and the files under sample-data/. Provide me a prompt I can use to build an end-to-end working demo of a Foundry agent with a web front end in Azure.
> ```

### Build something

These prompts are not designed to be used in order. They are examples for exploration and experimentation.

#### Prompt to build a Foundry agent with Work IQ and Foundry IQ
> Plan mode:
> ```
> I am building a demo for Meridian Advisory Group that implements a Foundry agent that generates proposals. The Foundry agent should be grounded in the provided data in sample-data/, using Work IQ and Foundry IQ. Refer to example/sample-basic-agent.py as the pattern for a Foundry agent. The Work IQ context contains emails and a calendar invite. The Foundry IQ knowledge base contains previous proposals, firm methodology, SME bios, case studies, pricing information, and other firm institutional knowledge. The agent should be able to generate very effective proposals for a client. Create a web app for this agent as well that enables the user to request a proposal for a specific client.
> ```

#### Prompt to index data and create a Foundry IQ knowledge base
> Agent mode:
> ```
> Index the documents in sample-data/foundry-iq/ into Azure AI Search to feed a Foundry IQ knowledge base.
> ```

#### Prompt to generate sample data for the agent
> Agent mode:
> ```
> Generate sample data based on your [2nd agentic idea] to help me feed the agent's knowledge sources.
> ```

#### Prompt to create a web app front end for the agent
> Agent mode:
> ```
> Now create a web app front end for the agent, and deploy it to an Azure web app.
> ```

### Rehearse the demo

> Ask mode:
> ```
> Write a 2-minute demo script for this agent aimed at Dr. Marsh and COO Whitfield — the exact prompts I type live, what comes back, and the single "wow" moment to land.
> ```

---

## A few things worth keeping in mind

- **Sample data is fictional** but designed to be internally consistent (the same clients, people, and engagements recur across all three IQs). Lean on that for cross-source demos.
- **Honor the constraints in the demo**. Client confidentiality, "no reusing a client's pricing," and zero-friction adoption are part of what makes the story credible. Bake them into your agent's behavior.
- **Smaller is better.** A two-minute demo that clearly does one valuable thing will teach you (and your audience) more than a half-built platform.


Have fun. Build something, run it, then make it better.
