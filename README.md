# Threads Profile and Posts MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-threads-profile-posts/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-threads-profile-posts) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-threads-profile-posts%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-threads-profile-posts&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-threads-profile-posts)](https://www.npmjs.com/package/@mambalabsdev/mcp-threads-profile-posts) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-threads-profile-posts)](https://www.npmjs.com/package/@mambalabsdev/mcp-threads-profile-posts) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-threads-profile-posts)](https://github.com/mambalabsdev/mcp-threads-profile-posts/blob/main/LICENSE)

An MCP server for the Mamba Labs Threads Profile and Posts actor on Apify. Public Threads profiles and newest posts as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes Threads usernames or profile links and returns one row per profile with follower count, bio, bio links, and verified mark, plus one row per post the logged out profile page shows, with text, date, likes, replies, reposts, quotes, and media links.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-threads-profile-posts": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-threads-profile-posts"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_threads_profiles` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "How many Threads followers do zuck and mosseri have, and what did each post last?"
- "Get the Threads bio and bio links for these 20 creators."

## Tool

`get_threads_profiles`. One tool. Example arguments:

```json
{
  "profiles": [
    "zuck"
  ],
  "include_posts": true
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `profiles` | array | no | Threads usernames (zuck or @zuck) or profile links (https://www.threads.com/@zuck, threads.net links work too). A post link is read as its author's profile. In Clay, wrap a column in a one item list. |
| `include_posts` | boolean | no | yes (default): one row per post the profile page shows to a logged out visitor, the newest threads with the author's own continuation posts. no: profile rows only. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Free rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `profile-row`, one profile | $0.004 | $0.0038 | $0.0036 | $0.0034 |
| `post-row`, one post | $0.0035 | $0.003325 | $0.00315 | $0.002975 |
| `apify-actor-start`, per run start | $0.006 | $0.006 | $0.006 | $0.006 |

Names with no public profile, refused requests, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/threads-profile-posts](https://apify.com/mambalabs/threads-profile-posts)

## License

MIT. See [LICENSE](LICENSE).
