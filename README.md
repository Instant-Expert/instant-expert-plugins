<p align="center">
  <img src="assets/logo.png" alt="Instant Expert" width="96" height="96">
</p>

# Instant Expert for AI assistants

[Instant Expert](https://instant.expert) gets you on the phone with specific people: the VP of Sales at a Series A startup, a head of procurement at a hospital system, a claims manager at a regional insurer. You describe who you want (or paste a lead list), it finds them and their work email, and it sends each one a paid invitation to a 15 to 60 minute call or a written or voice answer to one question. You pay only when someone books or replies.

This repo has the install files for using Instant Expert from Claude, Cowork, Claude Code, Cursor, VS Code, Codex, Gemini CLI and other MCP clients. The server itself is hosted at `https://instant.expert/mcp`, so there's nothing to run locally and no API key to manage; you sign in with your Instant Expert account the first time a tool runs.

**[MCP docs](https://instant.expert/docs/mcp)** · **[Limits and costs](https://instant.expert/docs/limits)** · **[Support](https://instant.expert/support)**

## What people use it for

- **Early customer discovery.** "We're building expense software for construction firms. Who should we talk to?" The assistant turns that into a few concrete audiences (say, controllers at US general contractors with 50 to 500 employees), finds them and drafts the ask.
- **Outreach to a persona.** "Find 30 heads of RevOps at Series B fintechs and invite them to a 15-minute call about pipeline tooling."
- **A lead list you already have.** Paste LinkedIn URLs or emails (up to 100 per batch). Instant Expert finds work emails where needed and drafts the invitations.
- **User testing and interviews.** Short paid calls or written answers from a specific kind of professional, for example "five security leads at companies that use Okta".
- **Following up.** "Did anyone book yet? What did the people who replied say?"

## How it works

1. You describe the people (or the problem you're trying to learn about) in plain language.
2. Instant Expert researches and saves a list. A research search often takes a few minutes, and the assistant tells you how many people it found against how many you asked for.
3. The assistant drafts the invitation: your message, call or written answer, price per person and a total cap.
4. You review an order preview (recipients, message, prices, cap, card and terms) and approve it. Nothing is sent or charged before that.
5. Invitations go out by email from Instant Expert. Replies, booked times and transcripts come back to the assistant when you ask.

## Pricing

- Searching, importing contacts and preparing drafts are free. They count toward your account's [limits](https://instant.expert/docs/limits).
- You set the price per person ($5 minimum, Instant Expert's fee included), or use each person's suggested price. Typical offers are probably in the $25 to $300 range, depending on seniority and whether it's a call or a written answer.
- A call is charged when the person books it. A written or voice answer is charged when the reply is completed. If nobody accepts, you pay nothing.
- A total cap (`max_spend_cents`) limits spend, so you can invite more people than the cap would cover if everyone said yes.

## Install

The MCP endpoint for every client is:

```text
https://instant.expert/mcp
```

It uses Streamable HTTP with OAuth sign-in. Paid sending is off for a new connection until you allow it (see [Permissions](#permissions)).

### Claude (claude.ai, desktop and mobile)

**Plugin (connector plus the workflow skill), recommended:**

1. Open **Customize → Plugins → Add → Add marketplace** and enter `Instant-Expert/instant-expert-plugins`.
2. Install **Instant Expert**.
3. Open the plugin's **Connectors** tab and connect **Instant Expert**. Sign in and approve.

**Connector only:** [add Instant Expert as a custom connector](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Instant%20Expert&connectorUrl=https%3A%2F%2Finstant.expert%2Fmcp), or go to **Customize → Connectors → Add custom connector** and paste the URL above. On Team and Enterprise plans an Owner adds connectors for the organization first.

### Cowork

Same steps as Claude above: **Customize → Plugins → Add → Add marketplace**, enter `Instant-Expert/instant-expert-plugins`, install, then connect from the plugin's **Connectors** tab. A plugin you install is saved to your account, so it also shows up in claude.ai chat and in Claude Code.

### Claude Code

```text
/plugin marketplace add Instant-Expert/instant-expert-plugins
/plugin install instant-expert@instant-expert
```

Then run `/mcp`, pick `instant-expert` and choose **Authenticate**. Connector only, without the skill:

```bash
claude mcp add --transport http --scope user instant-expert https://instant.expert/mcp
```

### Cursor

[Add to Cursor](https://cursor.com/en/install-mcp?name=instant-expert&config=eyJ1cmwiOiJodHRwczovL2luc3RhbnQuZXhwZXJ0L21jcCJ9) (or open `cursor://anysphere.cursor-deeplink/mcp/install?name=instant-expert&config=eyJ1cmwiOiJodHRwczovL2luc3RhbnQuZXhwZXJ0L21jcCJ9`), or add this to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "instant-expert": {
      "url": "https://instant.expert/mcp"
    }
  }
}
```

Cursor shows the server as needing login; select it to sign in.

### VS Code (GitHub Copilot agent mode)

[Install in VS Code](https://insiders.vscode.dev/redirect/mcp/install?name=instant-expert&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Finstant.expert%2Fmcp%22%7D) (or open `vscode:mcp/install?%7B%22name%22%3A%22instant-expert%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Finstant.expert%2Fmcp%22%7D`), or add this to `.vscode/mcp.json`:

```json
{
  "servers": {
    "instant-expert": {
      "type": "http",
      "url": "https://instant.expert/mcp"
    }
  }
}
```

From a terminal:

```bash
code --add-mcp '{"name":"instant-expert","type":"http","url":"https://instant.expert/mcp"}'
```

VS Code asks you to sign in the first time it starts the server.

### Codex CLI

Add this to `~/.codex/config.toml`. The scopes line matters: Instant Expert refuses the `openid` scope, which Codex otherwise requests.

```toml
[mcp_servers.instant-expert]
url = "https://instant.expert/mcp"
scopes = ["email", "profile"]
```

Then sign in:

```bash
codex mcp login instant-expert --scopes email,profile
```

### Gemini CLI

```bash
gemini extensions install https://github.com/Instant-Expert/instant-expert-plugins
```

The extension adds the server and a `GEMINI.md` context file with the workflow. Restart Gemini CLI, then run `/mcp auth instant-expert` to sign in. (Since June 18, 2026, Gemini CLI serves Gemini Code Assist Standard and Enterprise and paid API keys; other users moved to Antigravity CLI.)

### Grok

Go to [grok.com/connectors](https://grok.com/connectors), click **New Connector**, choose **Custom**, paste the URL above and sign in. On Grok Business and Enterprise, an admin provisions the connector first.

### Perplexity

Open **Account settings → [Connectors](https://www.perplexity.ai/account/connectors)**, click **+ Custom connector**, choose **Remote**, name it `Instant Expert`, paste the URL, pick **OAuth** and **Streamable HTTP**, then click the connector card to sign in. Enterprise admins can share it with the whole organization.

### Le Chat (Mistral)

Open the side panel, expand **Intelligence → Connectors**, click **+ Add Connector**, switch to the **Custom MCP Connector** tab, name it `instant-expert`, paste the URL and click **Connect**. Le Chat detects the OAuth sign-in. On Free, Pro and Student plans the account owner is the admin who can add connectors.

### ChatGPT

ChatGPT uses a separate Instant Expert plugin from its own directory. It finds people and prepares drafts; you review and send them on instant.expert. See [the ChatGPT docs](https://instant.expert/docs/chatgpt).

### Any other MCP client

- **Transport:** Streamable HTTP at `https://instant.expert/mcp`.
- **Auth:** OAuth 2.1 authorization code flow with PKCE and dynamic client registration. An unauthenticated request gets a `401` pointing to `https://instant.expert/.well-known/oauth-protected-resource/mcp`.
- **Scopes:** `email` and `profile`, plus `offline_access` for refresh tokens. Requests for `openid` or `phone` are refused at consent.

If sign-in fails in a client we haven't listed, email team@instant.expert with the client name and the error.

## Permissions

- Every connection can search, import contacts, prepare drafts and read your searches, drafts, sent requests and replies.
- **Paid sending is off by default.** You allow it per assistant on the consent screen or later in [Connected assistants](https://instant.expert/settings/connections). Without it, the assistant prepares drafts and you send them from [Requests](https://instant.expert/requests).
- Even with sending allowed, the assistant has to show you each order and get your explicit approval first. It can only use a card you've already saved on instant.expert; if you don't have one, it gives you a link to add one there. Card details never pass through chat.
- You can disconnect an assistant at any time in Connected assistants. Each connection is its own OAuth grant.

## Data and privacy

The files in this repo are Markdown and JSON; nothing here runs on your machine. When you use the tools, your assistant sends Instant Expert what you ask it to work with: search requests, contacts you provide, messages, budgets and order confirmations. Instant Expert uses them to run searches, find work emails at delivery time and deliver your invitations. Email addresses aren't returned to the assistant. See the [privacy policy](https://instant.expert/privacy) and [terms](https://instant.expert/terms).

## What's in this repo

```text
.claude-plugin/marketplace.json       Claude marketplace (claude.ai, Cowork, Claude Code)
.cursor-plugin/marketplace.json       Cursor multi-plugin manifest
plugins/instant-expert/
  .claude-plugin/plugin.json          Claude plugin manifest
  .cursor-plugin/plugin.json          Cursor plugin manifest
  .mcp.json                           Claude: remote MCP server
  mcp.json                            Cursor: remote MCP server
  skills/instant-expert/SKILL.md      Workflow skill (Claude, Cursor)
gemini-extension.json, GEMINI.md      Gemini CLI extension
server.json                           Official MCP Registry entry
.github/workflows/                    Registry publishing (GitHub OIDC)
```

## Support

Email team@instant.expert or see [instant.expert/support](https://instant.expert/support).

## License

[MIT](LICENSE) for the files in this repository. The Instant Expert service is governed by its [terms](https://instant.expert/terms).
