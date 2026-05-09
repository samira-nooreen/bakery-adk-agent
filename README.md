# 🥐 Location Intelligence ADK Agent
### *Build an AI-powered bakery intelligence agent using Google ADK, BigQuery, Google Maps, MCP & Gemini 3.1 Pro*

---

> **What if an AI could tell you exactly where to open your bakery, how much to charge for sourdough, and where the nearest supplier is — all in one conversation?**
> That's what this project builds.

---

## 🎯 About This Project

Built as part of the **Google Build with AI LIVE Workshop** by GeeksforGeeks (9th May 2025, 12 PM IST).

This hands-on 2-hour workshop covered how to create a **Location Intelligence Agent** that combines real-world mapping data with enterprise analytics to make smart business decisions — powered entirely on Google Cloud.

---

## 🧠 What This Agent Does

| Capability | Example Query |
|---|---|
| 📍 Foot Traffic Analysis | *"Find the zip code with the highest morning foot traffic in LA"* |
| 🏪 Competition Research | *"Search for bakeries in that zip code — is the market saturated?"* |
| 💰 Pricing Intelligence | *"Find the max price for a Sourdough Loaf in the LA Metro area"* |
| 📈 Revenue Forecasting | *"Forecast December 2025 revenue using historical sales data"* |
| 🚚 Logistics Validation | *"Find the nearest Restaurant Depot — drive time under 30 minutes?"* |

**Powered by:**
- 🤖 **Gemini 3.1 Pro** — reasoning engine
- 🗺️ **Google Maps MCP** — location intelligence
- 📊 **BigQuery MCP** — data analytics
- ⚙️ **Google ADK** — agent orchestration

---

## ✅ Prerequisites

- Google Cloud Project with billing enabled
- Web browser
- Basic terminal knowledge

---

## 🚀 Setup Guide

### 1. Set Up Google Cloud

1. Open [Google Cloud Console](https://console.cloud.google.com)
2. Create or select a project
3. Enable billing

### 2. Start Cloud Shell

Activate Cloud Shell from the top-right corner of the console, then verify your setup:

```bash
# Verify authentication
gcloud auth list

# Verify active project
gcloud config get project

# Export project ID
export PROJECT_ID=$(gcloud config get project)
```

### 3. Clone the Repository

```bash
git clone https://github.com/google/mcp.git
cd mcp/examples/launchmybakery
```

### 4. Authenticate

```bash
gcloud auth application-default login
```

> ⚠️ Re-authenticate if your session exceeds 60 minutes.

### 5. Configure Environment & BigQuery

```bash
# Run environment setup (enables APIs, creates .env, configures Maps API Key)
chmod +x setup/setup_env.sh
./setup/setup_env.sh

# Set up BigQuery (creates bucket, dataset, and tables)
chmod +x ./setup/setup_bigquery.sh
./setup/setup_bigquery.sh
```

### 6. Verify BigQuery Dataset

Open [BigQuery Console](https://console.cloud.google.com/bigquery) and confirm dataset `mcp_bakery` exists with these tables:

| Table | Description |
|---|---|
| `demographics` | Population data by zip code |
| `bakery_prices` | Pricing data across LA Metro |
| `sales_history_weekly` | Weekly sales history |
| `foot_traffic` | Morning/evening foot traffic scores |

### 7. Install ADK

```bash
# Create and activate virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install ADK
pip install google-adk==1.28.0

# Navigate to agent directory
cd adk_agent/
```

### 8. Run the Agent

```bash
adk web --allow_origins 'regex:https://.*\.cloudshell\.dev'
```

Expected output:
```
+------------------------------------------+
| ADK Web Server started                   |
| http://127.0.0.1:8000                    |
+------------------------------------------+
```

### 9. Open the ADK UI

**Option A:** Navigate to `http://127.0.0.1:8000`

**Option B:** Use Cloud Shell Web Preview → Change Port → Enter `8000`

---

## 📁 Project Structure

```
launchmybakery/
├── data/                          # CSV datasets
├── adk_agent/
│   └── mcp_bakery_app/
│       ├── agent.py               # Root agent definition (Gemini 3.1 Pro)
│       ├── tools.py               # MCP toolset configuration
│       └── .env                   # API keys & environment config
├── setup/
│   ├── setup_env.sh               # Environment setup script
│   └── setup_bigquery.sh          # BigQuery setup script
└── cleanup/
    └── cleanup_env.sh             # Cleanup script
```

---

## 🔧 How It Works

### Google Maps MCP Toolset
Used for place search, competition analysis, route calculations, and location intelligence.

```python
def get_maps_mcp_toolset():
    # Uses Maps API Key + Streamable HTTP MCP connection
    # Tools: search_places, compute_routes, lookup_weather
```

### BigQuery MCP Toolset
Used for SQL execution, sales analytics, demographic analysis, and forecasting.

```python
def get_bigquery_mcp_toolset():
    # Uses OAuth authentication + BigQuery MCP server
    # Tools: execute_sql_readonly, get_table_info, list_dataset_ids
```

### Agent Definition

```python
root_agent = LlmAgent(
    model='gemini-3.1-pro-preview'
    # Combines BigQuery + Maps reasoning
    # Unified business intelligence
)
```

---

## 💬 Example Prompts to Try

```
Find the zip code with the highest morning foot traffic score in Los Angeles.
```
```
Search for bakeries in that zip code to see if the market is saturated.
```
```
Find the maximum price for a Sourdough Loaf in the LA Metro area.
```
```
Forecast December 2025 revenue using historical sales data.
```
```
Find the nearest Restaurant Depot and ensure drive time is under 30 minutes.
```

---

## 🧹 Cleanup

Remove all cloud resources after the session:

```bash
chmod +x ../cleanup/cleanup_env.sh
./../cleanup/cleanup_env.sh
```

This removes:
- ✅ BigQuery datasets
- ✅ Cloud Storage buckets
- ✅ API keys
- ✅ Local `.env` configuration

---

## 💡 Key Learnings

- **Agentic AI vs Traditional LLMs** — LLMs are a brain; agentic AI gives them hands, eyes, and internet access
- **MCP Servers** — middleware connecting LLMs to external data sources and APIs
- **Trade-off: Accuracy vs Latency** — tool-augmented agents take ~30s for complex queries but deliver precise, real-world answers
- **Infrastructure automation** — setup scripts handle API enabling, key creation, and dataset provisioning end-to-end
- **Multi-tool orchestration** — a single query can trigger Google Maps + BigQuery calls in sequence

---

## 🛠️ Technologies Used

`Google ADK` · `Gemini 3.1 Pro` · `MCP` · `BigQuery` · `Google Maps` · `Python` · `Cloud Shell` · `Vertex AI`

---

## 📸 Submission Requirements

For the **Google Build with AI Workshop** certificate, submit screenshots of:

1. **Relevant question** — Ask a bakery/business intelligence question and capture the prompt + agent response + tool execution
2. **Irrelevant question** — Ask an unrelated question (e.g. *"Who won the football match yesterday?"*) and capture how the agent handles it
3. **GCP Credits screenshot** — Billing → Credits page showing your redeemed credits

---

## 🏆 Workshop Details

| Detail | Info |
|---|---|
| 🗓️ Date | 9th May 2025 |
| ⏰ Time | 12 PM IST |
| ⏱️ Duration | 2 Hours |
| 🎓 Organizer | GeeksforGeeks x Google |
| ☁️ Platform | Google Cloud Shell |

---

*Built with ❤️ as part of the Google Build with AI LIVE Workshop by GeeksforGeeks · #GoogleWithGFG #AntiGravity*
