# Tebar for Hermes Agent

Publish and schedule social media posts from [Hermes Agent](https://hermes-agent.nousresearch.com) with [Tebar](https://tebar.app), an Indonesian social media scheduler.

This is a portable Agent Plugins v1 package (`plugin.json` + `mcp.json` + `skills/`), configuration only. It connects Hermes to Tebar's official hosted MCP server and bundles one skill that tells the agent how to use it safely.

## What it does

- Publish now or schedule posts with images or videos to Instagram (Business or Creator), Threads, Facebook Pages, TikTok, YouTube, LinkedIn, X, Pinterest, Telegram and Discord
- List, edit, reschedule or cancel scheduled posts, and retry failed ones
- Read account and post statistics, and find your best posts
- Read and reply to comments, answer Instagram DMs, and run comment-to-DM automations
- Keep content ideas on an ideas board
- Upload files Hermes received in Telegram or WhatsApp (the agent runs a `curl` upload command)

## Setup

1. Create a Tebar account at https://publish.tebar.app and connect your social accounts on the **Akun** (Accounts) page.
2. Create an API key in the Tebar dashboard (user menu → **API key**). API access needs a paid Tebar plan or the free trial; on the Free plan every tool call returns `plan_required`.
3. Set it for Hermes, for example in your profile `.env`:

   ```
   TEBAR_API_KEY=tb_live_...
   ```

4. Install and enable the plugin:

   ```
   hermes plugins install tebar
   hermes plugins enable tebar
   ```

The agent works in one Tebar workspace: the key's workspace if you created the key for a workspace, otherwise your main workspace. It only sees the accounts, posts and comments in that workspace.

## Disclosure

- **Network calls.** Every tool call goes to `https://api.tebar.app/mcp`, which calls the social platforms' APIs (Meta, TikTok, Google, LinkedIn, X, Pinterest, Telegram, Discord) for the user's connected accounts. The API key from `TEBAR_API_KEY` is sent as a Bearer header.
- **Public, irreversible actions.** Write tools publish posts, reply to comments, send DMs and turn on automations that reply to people on their own. Published posts, replies and DMs cannot be deleted or unsent through Tebar. Posting to X is paid from the user's Tebar balance.
- **Approval.** The package marks the server `untrusted`, so Hermes asks before every tool that is not annotated read-only.
- **Data sent to the model provider.** Tool results (posts, statistics, comments, DMs, commenter and customer names) reach the model provider Hermes is configured with. Comments and DMs are written by strangers; Tebar marks them as untrusted data.
- **Server-defined tools.** The tool list comes from the server at run time and is not covered by the pinned commit. Tebar's tool annotations (`readOnlyHint`, `destructiveHint`, `openWorldHint`) describe each tool's effect.
- No local commands, background processes, stored credentials or telemetry: the package contains only configuration and one skill.

## Support

halo@tebar.app · Docs: https://docs.tebar.app · Privacy: https://tebar.app/privacy · Terms: https://tebar.app/terms

## License

MIT
