# TARS-Bot (v0.5.1)

TARS-Bot is a high-performance, modular Discord chatbot built with Node.js and powered by the OpenAI API. It is engineered for scalability and efficiency, utilizing advanced data structures to maintain low-latency responses ($O(1)$ complexity) even with a high volume of concurrent users. 

Since its inception 8 months ago, the project has scaled to support over 25,000 users across more than 50 servers.

## Core Architecture

The system is built on a modular framework of over 32 independent modules, separating command logic from the core processing engine.

### Hierarchical Memory System
TARS-Bot implements a dynamic tri-level memory architecture (Short, Medium, and Long-term):
* **O(1) Data Access:** User profiles and session states are cached in Maps to ensure constant-time retrieval.
* **Heap-Based History Management:** Message histories are managed using Heaps to prevent memory leaks and optimize the pruning of massive chat logs.
* **Summarization Engine:** A specialized module distills short-term memory into persistent keywords and concise summaries (maximum 2 paragraphs), preserving context for long-term storage without exceeding token limits.

### System Resilience and Integrity
* **History Integrity Checker (HIC):** A self-healing module that scans and repairs conversation inconsistencies, preventing runtime crashes caused by malformed API payloads or token overflows.
* **Global Context Persistence:** Unlike standard bots, TARS tracks user interactions across different servers based on their unique ID, maintaining a unified conversational thread.
* **Proactive Moderation:** An integrated layer that evaluates user intent and denies interaction if offensive content is detected.

## Features

* **Multimodal Interaction:** Full support for Text (GPT models), Vision (image analysis), and DALL-E (image generation).
* **Text-to-Speech (TTS):** High-fidelity audio generation featuring 6 distinct vocal profiles.
* **Thread Management:** Native support for Discord threads to handle complex multi-user discussions.
* **Customizable Schemas:** Flexible MongoDB integration for per-user and per-server configuration.

## Project Structure

```text
.
├── comandos/            # Command definitions (OpenAI, Config, Utility)
├── events/              # Discord gateway event handlers
├── modules/
│   ├── conversations/   # Thread and history logic
│   ├── hic/             # History Integrity Checker (Self-healing)
│   ├── moderation/      # Security and safety layers
│   ├── mongo/           # Database schemas and connection logic
│   ├── openai/          # Specialized wrappers for Text, Image, and Audio
│   └── summarizer/      # Context compression algorithms
├── main.js              # Entry point
└── deploy-commands.js   # Slash command registration script
```

## Technical Stack

* **Runtime:** Node.js (ES Modules)
* **Database:** MongoDB via Mongoose
* **AI Integration:** OpenAI API (v4.52.5)
* **Communication:** Discord.js (v13.17.1)
* **Logging:** Winston
* **Testing:** Jest

## Setup and Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/tars-bot.git
    cd tars-bot
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Environment Configuration:**
    Create a `.env` file in the root directory:
    ```env
    DISCORD_TOKEN=your_discord_bot_token
    OPENAI_API_KEY=your_openai_api_key
    MONGO_URI=your_mongodb_connection_string
    ```

4.  **Deployment:**
    Register the slash commands and start the bot:
    ```bash
    node deploy-commands.js
    npm start
    ```

## Development and Testing

The project uses Jest for unit testing. To run the test suite:
```bash
npm test
```

## License

This project is licensed under the ISC License. Developed by msh.
