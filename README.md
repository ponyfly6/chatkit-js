# ChatKit JS

ChatKit is a batteries-included framework for building high-quality, AI-powered chat experiences. Designed for developers who want to add advanced conversational intelligence to their apps fast—with minimal setup and no reinventing the wheel.

## Features

- 🎨 **Deep UI customization** — Make ChatKit feel like a native part of your app
- 💬 **Built-in response streaming** — Interactive, natural conversations in real-time
- 🛠️ **Tool and workflow integration** — Visualize agentic actions and chain-of-thought reasoning
- 🧩 **Rich interactive widgets** — Embed custom components directly inside chat bubbles
- 📎 **Attachment handling** — Support for file and image uploads out of the box
- 🧵 **Thread and message management** — Organize complex conversations effortlessly
- 🏷️ **Source annotations and entity tagging** — Provide transparency and references
- 🌐 **Framework-agnostic** — Works with React, Vue, Svelte, or vanilla JavaScript

## What makes ChatKit different?

ChatKit is a drop-in chat solution that delivers a complete, production-ready interface out of the box. You don't need to:

- Build custom chat UIs from scratch
- Manage low-level chat state and event handling
- Patch together multiple libraries for streaming, attachments, and widgets

Simply add the ChatKit component, configure your API, and customize the experience to match your brand.

## Quickstart

### 1. Install the package

```bash
npm install @openai/chatkit-react
```

### 2. Generate a client token on your server

```python
from fastapi import FastAPI
from openai import OpenAI
import os

app = FastAPI()
openai = OpenAI(api_key=os.environ["OPENAI_API_KEY"])

@app.post("/api/chatkit/session")
def create_chatkit_session():
    session = openai.chatkit.sessions.create()
    return {"client_secret": session.client_secret}
```

### 3. Add the ChatKit script to your page

```html
<script
  src="https://cdn.platform.openai.com/deployments/chatkit/chatkit.js"
  async
></script>
```

### 4. Render ChatKit in your React app

```tsx
import { ChatKit, useChatKit } from '@openai/chatkit-react';

export function MyChat() {
  const { control } = useChatKit({
    api: {
      async getClientSecret(existing) {
        // Refresh session if expired
        if (existing) {
          const res = await fetch('/api/chatkit/session', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
          });
          const { client_secret } = await res.json();
          return client_secret;
        }

        // Get new session
        const res = await fetch('/api/chatkit/session', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
        });
        const { client_secret } = await res.json();
        return client_secret;
      },
    },
  });

  return <ChatKit control={control} className="h-[600px] w-[320px]" />;
}
```

## Examples

| Example | Description |
|---------|-------------|
| [Starter App](https://github.com/openai/openai-chatkit-starter-app) | Fully working template to get started quickly |
| [Advanced Samples](https://github.com/openai/openai-chatkit-advanced-samples) | Explore various integrations and customizations |

## Documentation

Visit [chatkit.studio](https://chatkit.studio) for:

- 📘 Complete API reference
- 🎨 Live playground to customize your chat UI
- 📚 Guides on advanced features like widgets and entity tagging

## Monorepo Structure

This repository is a pnpm workspace containing:

| Package | Description |
|---------|-------------|
| [`@openai/chatkit`](packages/chatkit/) | TypeScript type definitions for the ChatKit Web Component |
| [`@openai/chatkit-react`](packages/chatkit-react/) | React bindings and hooks for ChatKit |
| [`docs`](packages/docs/) | Documentation site (Astro + Starlight) |

## Development

```bash
# Install dependencies
pnpm install

# Build all packages
pnpm build

# Run the documentation site
pnpm dev:docs

# Run tests
pnpm test

# Run linting
pnpm lint

# Format code
pnpm format
```

## License

This project is licensed under the [Apache License 2.0](LICENSE).
