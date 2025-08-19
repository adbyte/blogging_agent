# 🤖 AI Blog Post Automation Agent (n8n + Telegram + Airtable)

This repository contains an **n8n workflow** that functions as an AI-powered agent to automate the creation of structured, high-quality blog posts.  

The agent interacts with users via **Telegram**, uses an **AI/LLM** for content generation, and stores user preferences in **Airtable** for personalized output.

---

## ✨ Features

- **Conversational Interface** – Interact with the agent naturally through a Telegram bot.  
- **End-to-End Content Creation** – Provide a blog title and receive a full outline, followed by a complete, well-structured blog post.  
- **Personalized Output** – Store and manage preferences like writing tone (e.g., "professional," "casual") and specific keywords to be included in the content.  
- **Dynamic Preference Management** – Use simple commands directly in Telegram (`/add_preference`, `/add_keyword`) to update your settings in real-time.  
- **Structured Formatting** – The final blog post is delivered in clean markdown with proper headings and structure, ready to be published.  
- **Extensible** – Built on **n8n**, making it easy to modify, add new tools, or integrate with other services.  

---

## ⚙️ How It Works

![Blog Agent Workflow](blog%20agent%20workflow.png)

The workflow follows a logical sequence triggered by a user message in Telegram:

1. **User Input** – The user sends a blog title to the Telegram bot.  
2. **Preference Retrieval** – The workflow queries an Airtable base to retrieve the user's saved preferences (tone, keywords).  
3. **Outline Generation** – The blog title and retrieved preferences are sent to an AI/LLM (e.g., OpenAI's GPT-4) with a structured prompt to generate a detailed blog post outline.  
4. **Outline Delivery** – The generated outline is sent back to the user via Telegram for review.  
5. **Full Content Generation** – The workflow uses the title, outline, and preferences to generate a ~1000-word blog post.  
6. **Final Delivery** – The completed markdown blog post is delivered in Telegram.  
7. **Command Handling** – `/add_preference` and `/add_keyword` commands update preferences in Airtable and confirm with the user.  

---

## 🛠️ Components Used

- **[n8n](https://n8n.io/)** – Core automation platform orchestrating the workflow  
- **[Telegram](https://core.telegram.org/bots/api)** – Conversational interface with the user  
- **[Airtable](https://airtable.com/)** – Database for storing and managing preferences  
- **AI/LLM (e.g., OpenAI, Anthropic, Gemini)** – Content generation engine  

---

## 🚀 Setup & Configuration

### 1. Airtable Base
Create a new Airtable base with a table named **`User Preferences`**. The table should have these fields:  

- `UserID` *(Single line text)* – stores the Telegram User ID (primary key).  
- `Tone` *(Single line text)* – desired writing tone (e.g., Professional, Casual, Witty).  
- `Keywords` *(Long text)* – comma-separated list of keywords.  

---

### 2. n8n Credentials
Configure the following in your n8n instance:  

- **Telegram Bot** – Get API token from [BotFather](https://core.telegram.org/bots#botfather).  
- **Airtable** – Use your Airtable API key.  
- **AI/LLM Provider** – API key for your model (e.g., OpenAI).  

---

### 3. Workflow Configuration
1. Import the `workflow.json` into n8n.  
2. Connect your credentials in the respective nodes:  
   - **Telegram Trigger Node** → Telegram Bot  
   - **Airtable Nodes** → Airtable Base + Table `User Preferences`  
   - **LLM Nodes** → AI/LLM provider  
3. Review & adjust prompts in the **Generate Outline** and **Generate Full Blog** nodes.  

---

## 💬 Usage

### Generate a Blog Post
Simply send the blog title to your Telegram bot.  
```text
The Future of Renewable Energy in Urban Environments
