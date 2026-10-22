# Melo connector for Claude

Save words from a language-learning conversation, then review them as flashcards
in Melo on iPhone. Search your saved vocabulary or remove words you no longer need.

## Before connecting

Install [Melo for iOS](https://apps.apple.com/us/app/melo-words-from-ai-chats/id6760539346) and sign in with
Apple. Demo mode has no personal vocabulary connection. In Melo settings, copy
your personal MCP URL. Keep it private: it grants access to your vocabulary.

## Connect to Claude

1. Open Claude's Customize → Connectors and add a custom web connector.
2. Name it Melo and enter the shared server URL:
   `https://melo-mcp.azuic.workers.dev/mcp`.
3. Continue with OAuth. On Melo's connection page, paste the personal MCP URL
   copied from the iOS app. Check the callback hostname and select Connect to Claude.
4. Return to Claude and ask it to save or search vocabulary.

The public connector uses OAuth 2.0 with Dynamic Client Registration and S256
PKCE. No manually configured OAuth client ID or secret is needed. Your personal
URL is entered on Melo's authorization page, not used as the directory listing URL.
The current access token lasts one year. Melo does not issue refresh tokens;
reconnect when an expired connection requires sign-in.

## Try it

- "Save flâner to Melo in French, with its meaning, pronunciation, and two examples."
- "Find my saved Japanese adjectives. Browse the next page if there are more."
- "Remove bonjour from my Melo vocabulary."

Words save on request. For auto-save, explicitly ask "Save the new vocabulary
we discuss to Melo in this conversation." You can use the optional instructions
in [SYSTEM_PROMPT.md](AUTO_SAVE.md). Say "Stop saving words to Melo" to stop.
Claude still applies its permission and confirmation controls.

Saving the same exact word replaces its entry, including previously saved fields.
Melo matches saved word identifiers exactly for writes and deletions. Search is
case-insensitive and normalizes Unicode composition while preserving accents.

## Tools and data access

| Tool | What it does |
| --- | --- |
| `save_word` | Create or replace one exact vocabulary entry. |
| `search_vocab` | Search words and meanings; browse compact pages with an optional language filter. |
| `get_vocab` | Export the complete vocabulary for app sync or an explicit export. |
| `delete_word` | Remove one exact word. |
| `delete_account` | Permanently delete all vocabulary stored for the account. |

This connector reads and writes your vocabulary. It does not access Claude's
memory or history, and it receives only the tool arguments the client sends.
Only include information needed for the vocabulary entry.

## Troubleshooting

- **Nothing appears in Melo:** verify that the authorization page used the URL
  from the same Apple account you use in the app, then refresh Melo. Cloudflare
  KV changes can take time to become visible across locations.
- **No words save automatically:** saving requires your request or an explicit
  auto-save preference. Check Claude's connector permissions too.
- **A search misses a word:** try `mode: contains`; accents are significant.
  Follow `nextOffset` until it is `null` to finish browsing.
- **A connection is unauthorized or expired:** reconnect through OAuth. Never
  post a personal MCP URL, code, or bearer token in a support issue.
- **An entry lost details after saving again:** saving replaces the complete
  entry. Include the fields you want to retain when updating it.
- **Deleting vocabulary:** Delete Account removes saved words. It does not
  revoke the Apple-provided account token or OAuth connections. See the policy
  for credential retention and deletion assistance.

## Privacy and support

Read [Melo's privacy policy](https://azuic.github.io/melo-privacy/). Vocabulary and OAuth records
are processed by Cloudflare, and your connected AI service receives tool results.

Support and privacy: **hi@zui.ooo**. [Melo on the App Store](https://apps.apple.com/us/app/melo-words-from-ai-chats/id6760539346).

