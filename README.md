# Task Master Sample App

This repository serves as a sample configuration for the [`claude-task-master`](https://github.com/eyaltoledano/claude-task-master) AI-powered task management system. It's designed to provide a ready-to-use example of how to structure your project to integrate with Task Master, especially within an environment like Cursor.

## About Task Master

Task Master is an AI-powered task-management system you can drop into Cursor, Lovable, Windsurf, Roo, and others. It helps you manage your development workflow, from parsing product requirement documents to generating, assigning, and tracking tasks.

For full documentation and more details, please visit the official [claude-task-master repository](https://github.com/eyaltoledano/claude-task-master).

## How to Use This Sample

This repository is pre-configured to work with Task Master. Here's how to get started:

### 1. Clone the Repository & Install Dependencies

Clone this repository to your local machine and install dependencies:

```bash
git clone <repository-url>
cd taskmaster-sample-app
npm i
```

### 2. Configure API Keys

Task Master uses AI models from various providers, which require API keys. You need to provide your keys to use its AI-powered features.

#### For CLI Usage

If you plan to use the `task-master` CLI directly, you'll need a `.env` file in the project root.

1.  Copy the example file:
    ```bash
    cp .env.example .env
    ```
2.  Edit the `.env` file and add your API keys.

#### For Cursor (MCP Server) Usage

For the best experience inside Cursor, you should configure the MCP (Model Control Protocol) server. This allows you to interact with Task Master through Cursor's chat and tools.

1.  Create or open your project-specific MCP configuration file at `.cursor/mcp.json`.
2.  Add the following configuration, filling in your API keys. You only need to add keys for the services you intend to use.

    ```json
    {
      "mcpServers": {
        "taskmaster-ai": {
          "command": "npx",
          "args": ["-y", "--package=task-master-ai", "task-master-ai"],
          "env": {
            "ANTHROPIC_API_KEY": "YOUR_ANTHROPIC_API_KEY_HERE",
            "PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
            "OPENAI_API_KEY": "YOUR_OPENAI_KEY_HERE",
            "GOOGLE_API_KEY": "YOUR_GOOGLE_KEY_HERE",
            "MISTRAL_API_KEY": "YOUR_MISTRAL_KEY_HERE",
            "OPENROUTER_API_KEY": "YOUR_OPENROUTER_KEY_HERE",
            "XAI_API_KEY": "YOUR_XAI_KEY_HERE",
            "AZURE_OPENAI_API_KEY": "YOUR_AZURE_KEY_HERE",
            "OLLAMA_API_KEY": "YOUR_OLLAMA_API_KEY_HERE"
          }
        }
      }
    }
    ```

3.  Enable the `taskmaster-ai` MCP server in Cursor's settings.

### 3. Start Using Task Master

Once configured, you can start interacting with Task Master.

**In Cursor:**

- "Initialize taskmaster-ai in my project"
- "What's the next task I should work on?"
- "Parse my PRD at .taskmaster/docs/prd.txt"

**Via CLI:**

You can use `npx` to run Task Master commands without installing it globally. Here are a few examples:

- `npx task-master list` - to show tasks to perform
- `npx task-master models` - to show configured models
- `npx task-master next` - to see the next suggested task
- `npx task-master init` - to initialize task master in a new project

## Project Structure

- `.taskmaster/`: Contains Task Master specific files, such as tasks, reports, and documentation.
  - `docs/`: Place your Product Requirement Documents (PRDs) here.
  - `tasks/`: Where generated `tasks.json` and individual markdown task files are stored.
- `.cursor/`: Configuration for the Cursor editor.
  - `mcp.json`: (You may need to create this) MCP server configuration.
  - `rules/`: Contains rules for the AI to follow during development. This repo includes the standard Task Master rules.
- `.env.example`: Template for API keys for CLI usage.
- `package.json`: Project dependencies. This sample is a Next.js app.
