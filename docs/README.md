# Eliza - Multi-agent simulation framework

<img src="static/img/eliza_banner.jpg" alt="Eliza Banner" width="100%" />

_As seen powering [@DegenSpartanAI](https://x.com/degenspartanai) and [@MarcAIndreessen](https://x.com/pmairca)_

## 🌍 README Translations

[中文说明](./README_CN.md) | [Deutsch](./README_DE.md) | [Français](./README_FR.md) | [ไทย](./README_TH.md) | [Español](README_ES.md)

---

## Features

- Multi-agent simulation framework
- Add unlimited unique characters with [characterfile](https://github.com/lalalune/characterfile/)
- Full-featured Discord and Twitter connectors, with Discord voice channel support
- Robust conversational and document RAG memory
- Reads links, PDFs, transcribes audio/videos, and summarizes conversations
- Highly extensible - create your own actions and clients to extend Eliza's capabilities
- Supports open-source and local models (default: Nous Hermes Llama 3.1B)
- Supports OpenAI for cloud inference on lightweight devices
- "Ask Claude" mode for complex queries
- Fully written in TypeScript

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Customising Eliza](#customising-eliza)
3. [Running with Different Models](#running-with-different-models)
4. [Environment Setup](#environment-setup)
5. [Local Inference Setup](#local-inference-setup)
6. [Clients](#clients)
7. [Development](#development)

---

## Getting Started

### Prerequisites

- [Node.js 23+](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- [pnpm](https://pnpm.io/installation)

### Configuration

1. Clone the repository:
   ```bash
   git clone https://github.com/elizaOS/eliza.git
   cd eliza
   ```

2. Install dependencies:
   ```bash
   pnpm install
   ```

3. Set up environment variables:
   - Copy `.env.example` to `.env`:
     ```bash
     cp .env.example .env
     ```
   - Edit `.env` and add your API keys.

4. Configure characters:
   - Modify the default character file `src/core/defaultCharacter.ts`.
   - Alternatively, load a JSON character file with:
     ```bash
     pnpm start --characters="path/to/your/character.json"
     ```

5. Start the bot:
   ```bash
   pnpm start
   ```

---

## Customising Eliza

### Adding Custom Actions

To prevent merge conflicts, add custom actions to a `custom_actions` directory and include them in the `elizaConfig.yaml` file. Refer to `elizaConfig.example.yaml` for guidance.

---

## Running with Different Models

### Run with Llama

Set the environment variable for a provider supporting Llama models (70B or 405B). Llama can also run locally without additional configuration.

### Run with Grok

Set the `GROK_API_KEY` environment variable and specify "grok" as the model provider in your character file.

### Run with OpenAI

Set the `OPENAI_API_KEY` environment variable and specify "openai" as the model provider in your character file.

---

## Environment Setup

Define the following variables in your `.env` file:

```
# Required variables
DISCORD_APPLICATION_ID=
DISCORD_API_TOKEN= # Bot token
OPENAI_API_KEY=sk-* # OpenAI API key
ELEVENLABS_XI_API_KEY= # ElevenLabs API key

# ElevenLabs settings
ELEVENLABS_MODEL_ID=eleven_multilingual_v2
ELEVENLABS_VOICE_ID=21m00Tcm4TlvDq8ikWAM
ELEVENLABS_VOICE_STABILITY=0.5
ELEVENLABS_VOICE_SIMILARITY_BOOST=0.9
ELEVENLABS_VOICE_STYLE=0.66
ELEVENLABS_VOICE_USE_SPEAKER_BOOST=false
ELEVENLABS_OPTIMIZE_STREAMING_LATENCY=4
ELEVENLABS_OUTPUT_FORMAT=pcm_16000

TWITTER_DRY_RUN=false
TWITTER_USERNAME= # Twitter username
TWITTER_PASSWORD= # Twitter password
TWITTER_EMAIL= # Twitter email

ANTHROPIC_API_KEY=

# Wallet configuration
WALLET_SECRET_KEY=EXAMPLE_WALLET_SECRET_KEY
WALLET_PUBLIC_KEY=EXAMPLE_WALLET_PUBLIC_KEY

# Solana configuration
SOLANA_RPC_URL=https://api.mainnet-beta.solana.com
HELIUS_API_KEY=

# Telegram
TELEGRAM_BOT_TOKEN=

TOGETHER_API_KEY=
```

---

## Local Inference Setup

### CUDA Setup

Install CUDA for accelerated local inference:

```bash
pnpm install
npx --no node-llama-cpp source download --gpu cuda
```

Ensure that the CUDA Toolkit, cuDNN, and cuBLAS are installed.

### Running Locally

Set the `XAI_MODEL` environment variable to specify the model. If no API key is provided, the model will be downloaded and run locally.

---

## Clients

### Discord Bot

For guidance on setting up your Discord Bot, see: [Discord.js Guide](https://discordjs.guide/preparations/setting-up-a-bot-application.html).

---

## Development

### Testing

Run the test suite:

```bash
pnpm test           # Run tests once
pnpm test:watch    # Watch mode
```

Database-specific tests:

```bash
pnpm test:sqlite   # SQLite
pnpm test:sqljs    # SQL.js
```

Tests are written with Jest and located in `src/**/*.test.ts`. Configuration includes:

- Loading `.env.test` variables
- 2-minute timeout for long-running tests
- ESM module support
- Sequential execution (`--runInBand`)

### Updating Documentation

To verify documentation locally:

```bash
docker compose -f docker-compose-docs.yaml up --build
```

Access the Docusaurus server at: https://localhost:3000/eliza.
