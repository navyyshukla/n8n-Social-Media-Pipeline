# 🚀 n8n-Social-Media-Pipeline

An automated, end-to-end AI content generation pipeline built with **n8n**. This workflow takes a simple topic idea, generates a viral-ready Twitter/X thread using Groq's Llama 3.1, logs the data securely in Supabase, and utilizes a dual-channel Discord architecture for team alerts and content delivery.

## 🛠️ Tech Stack & Integrations
* **n8n:** Visual node-based workflow automation.
* **Groq (Llama 3.1 8B):** Ultra-fast Large Language Model for content generation.
* **Supabase:** Open-source PostgreSQL database for secure content logging.
* **Discord Webhooks:** Parallel notification and delivery system.

## 🏗️ System Architecture

This pipeline follows a strict **Intake $\rightarrow$ Process $\rightarrow$ Log $\rightarrow$ Deliver** architecture:

1. **Content Intake Form (Frontend):** A clean, user-friendly n8n web form that allows team members to submit topic ideas without needing access to the backend.
2. **Groq AI Engine (Processing):** The submitted topic is passed to Groq via an API request. A strict system prompt ensures the generated Twitter thread is formatted beautifully and remains under Discord's 2,000-character limit.
3. **Supabase Database Log (Storage):** Before delivery, the `raw_idea` and the `generated_content` are safely logged as a new row in a Supabase database. This creates a permanent archive of all team content.
4. **Dual-Channel Discord Delivery (Output):**
   The workflow branches into two simultaneous webhook executions:
   * **`#thread-alerts`:** A high-level status ping notifying the team that a new topic has been processed and saved.
   * **`#full-drafts`:** The actual content delivery channel containing the fully formatted AI thread, ready for review and publishing.

## ⚙️ How to Import and Run

If you want to run this pipeline on your own n8n instance:

1. Clone or download this repository.
2. Open your n8n workspace.
3. Go to **Workflows** $\rightarrow$ **Import from File** and select `CreatorJoy-AI-Pipeline.json`.
4. **Configure Credentials:**
   * Add your Groq API Key to the HTTP Request node.
   * Add your Supabase URL and Service Role Key to the Supabase node.
   * Replace the Discord Webhook URLs with your own server's webhooks.
5. Click **Publish** and open the Production URL of the trigger node to test!

## 🔮 Future Expansions
* **Multi-Platform Support:** Branching the AI prompt to generate LinkedIn posts alongside Twitter threads.
* **Approval Queue:** Integrating a Slack/Discord interactive button to approve the draft before automatically posting to the social platform via API.

---
*Designed and built for automated content scaling.*
