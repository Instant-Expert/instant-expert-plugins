# Instant Expert

Find specific executives, operators and experts from a conversation with Claude, or bring a lead list you already have, and invite them to a paid 15 to 60 minute call or a written or voice answer to one question. You pay only when someone books the call or completes the answer.

This plugin bundles two things: the Instant Expert connector (a remote MCP server at `https://instant.expert/mcp`) and a skill that teaches Claude the workflow, from "who should I talk to?" through search, drafting, order review and checking replies.

## Use it

1. Install the plugin, then connect the **Instant Expert** connector from the plugin's **Connectors** tab (claude.ai and Cowork) or run `/mcp` and choose **Authenticate** (Claude Code). You sign in to your Instant Expert account and approve the connection.
2. Ask in plain language, for example:
   - "We're building claims-triage software for mid-size insurers. Who should I talk to for discovery?"
   - "Find 30 heads of RevOps at Series B fintech companies in the US and draft a 15-minute call invite."
   - "Here are 40 LinkedIn URLs from our lead list. Draft an invite asking about their outbound tooling, $75 per call, $1,500 cap."
   - "Did anyone reply to last week's requests?"
3. Claude shows you the people, the draft and an order preview (recipients, message, prices, total cap, card and terms). Nothing is sent or charged until you explicitly approve that preview. Paid sending is off for a new connection until you allow it, and card details are only ever entered on instant.expert, never in chat.

## Pricing

Searching, importing contacts and preparing drafts cost nothing (they count toward your account's limits). You set the price per person, $5 minimum, including Instant Expert's fee. A call is charged when the person books it, a written or voice answer when the reply is completed, and nothing is charged if nobody accepts. Details: https://instant.expert/docs/limits

## Data

The plugin contains only Markdown and JSON; it runs no code on your machine. Through the connector, Claude sends Instant Expert what you ask it to work with: search requests, contacts you provide (LinkedIn URLs, emails, names), your messages, budgets and order confirmations. Instant Expert stores these in your account to run searches, find work emails at delivery time and deliver your invitations. Email addresses are never returned to Claude. Replies from the people you invite come back through the connector when you ask for them.

- Docs: https://instant.expert/docs/mcp
- Privacy policy: https://instant.expert/privacy
- Terms: https://instant.expert/terms
- Support: https://instant.expert/support (team@instant.expert)

## License

MIT for the files in this plugin. The Instant Expert service is governed by its own terms.
