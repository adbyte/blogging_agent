🤖 AI Blog Post Automation Agent (n8n + Telegram + Airtable)
This repository contains an n8n workflow that functions as an AI-powered agent to automate the creation of structured, high-quality blog posts. The agent interacts with users via Telegram, uses an AI/LLM for content generation, and stores user preferences in an Airtable base for personalized output.

✨ Features
Conversational Interface: Interact with the agent naturally through a Telegram bot.

End-to-End Content Creation: Provide a blog title and receive a full outline, followed by a complete, well-structured blog post.

Personalized Output: Store and manage preferences like writing tone (e.g., "professional," "casual") and specific keywords to be included in the content.

Dynamic Preference Management: Use simple commands directly in Telegram (/add_preference, /add_keyword) to update your settings in real-time.

Structured Formatting: The final blog post is delivered in clean markdown with proper headings and structure, ready to be published.

Extensible: Built on n8n, making it easy to modify, add new tools, or integrate with other services.

⚙️ How It Works
![Blog Agent Workflow](blog_agent_workflow.png)
The workflow follows a logical sequence triggered by a user message in Telegram. Below is a visual representation of the agent's logic.

User Input: The user sends a blog title to the Telegram bot.

Preference Retrieval: The workflow queries an Airtable base to retrieve the user's saved preferences (tone, keywords).

Outline Generation: The blog title and retrieved preferences are sent to an AI/LLM (e.g., OpenAI's GPT-4) with a specific prompt to generate a detailed blog post outline.

Outline Delivery: The generated outline is sent back to the user via Telegram for review.

Full Content Generation: The workflow uses the original title, the generated outline, and the user preferences to prompt the AI/LLM to write the full blog post (approx. 1000 words).

Final Delivery: The complete, markdown-formatted blog post is sent to the user in Telegram.

Tool/Command Handling: The workflow includes a router that listens for specific commands (/add_preference and /add_keyword). When a command is detected, it triggers a separate path to add the specified data to the correct field in the Airtable base, confirming the update with the user.

🛠️ Components Used
n8n: The core automation platform that orchestrates the workflow.

Telegram: Serves as the user interface for interaction.

Airtable: Acts as a simple database to store and manage user preferences.

AI / LLM: Any large language model provider compatible with n8n (e.g., OpenAI, Anthropic, Google Gemini) for content generation.

🚀 Setup & Configuration
To get this workflow running, you will need to configure the following:

1. Airtable Base:
Create a new Airtable base with a table named "User Preferences". The table should have the following fields:

UserID (Single line text): To store the Telegram User ID. This will be the primary key.

Tone (Single line text): To store the desired writing tone (e.g., "Professional", "Witty", "Informative").

Keywords (Long text): To store a comma-separated list of keywords to include in the blog post.

2. n8n Credentials:
In your n8n instance, configure the credentials for the following services:

Telegram Bot: You will need the API token from Telegram's BotFather.

Airtable: You will need your Airtable API key.

AI/LLM Provider: You will need the API key for your chosen language model (e.g., OpenAI API key).

3. Workflow Configuration:

Import the workflow.json file into your n8n instance.

Telegram Trigger Node: Connect your Telegram Bot credential.

Airtable Nodes:

Connect your Airtable credential.

Select your "Blog Agent" base and the "User Preferences" table.

Ensure the UserID from the Telegram trigger is used to look up and update records.

LLM Nodes:

Connect your AI/LLM provider credential.

Review and adjust the prompts in the "Generate Outline" and "Generate Full Blog" nodes to better suit your needs.

💬 Usage
Interact with the agent through your Telegram bot.

To Generate a Blog Post:
Simply send the title of the blog post you want to create.
Example: The Future of Renewable Energy in Urban Environments

To Manage Preferences:
Use the following commands to update your settings stored in Airtable.

Add/Update Writing Tone:
/add_preference <Your-Preference>
Example: /add_preference Professional and Authoritative

Add Keywords:
/add_keyword <comma-separated, keywords>
Example: /add_keyword solar power, wind turbines, smart grids, sustainability

The agent will confirm once your preferences have been updated. The next blog post you generate will use these new settings.
