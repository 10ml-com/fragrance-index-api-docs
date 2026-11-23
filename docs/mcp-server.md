# Perfume MCP server: free, one URL, no API key

10ML Perfume Finder is a free perfume MCP server. Add https://mcp.10ml.com/mcp to Claude, ChatGPT, Cursor or VS Code and your assistant can look up 6,000+ perfumes from the 10ML Fragrance Index, with note pyramids, accords, similar scents and alternatives from other houses. No API key, no sign-up. It answered 39 of 40 questions in our October 2026 benchmark.

Add this URL to your MCP client: https://mcp.10ml.com/mcp

Works with Claude, ChatGPT, Cursor, VS Code, Gemini CLI, Windsurf, Cline, Goose and Zed. Most accurate and fastest of the free perfume MCP servers we benchmarked (20 October 2026). [See the benchmark](https://10ml.com/perfume-mcp-servers-compared)

Source page: https://10ml.com/perfume-mcp-server

## Connect it

The address is the same in every client: https://mcp.10ml.com/mcp

### Claude (claude.ai and Claude Desktop)

Open Customize, then Connectors, and add 10ML Perfume Finder from the directory, or choose + Add, then Add custom connector, and paste the URL.

[Open in Claude's directory](https://claude.ai/directory/10ml-perfume-finder)

### Claude Code

```
claude mcp add --transport http perfume-finder https://mcp.10ml.com/mcp
```

### ChatGPT

On the web, open ChatGPT Plugins, select the plus button, then Add custom MCP server: name it 10ML Perfume Finder, paste the URL and choose no authentication.

### Cursor

[Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=perfume-finder&config=eyJ1cmwiOiJodHRwczovL21jcC4xMG1sLmNvbS9tY3AifQ==)

Or add to ~/.cursor/mcp.json:

```
{ "mcpServers": { "perfume-finder": { "url": "https://mcp.10ml.com/mcp" } } }
```

### VS Code

[Install in VS Code](vscode:mcp/install?%7B%22name%22%3A%22perfume-finder%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.10ml.com%2Fmcp%22%7D)

Or add to .vscode/mcp.json:

```
{ "servers": { "perfume-finder": { "type": "http", "url": "https://mcp.10ml.com/mcp" } } }
```

### Gemini CLI

```
gemini mcp add --transport http perfume-finder https://mcp.10ml.com/mcp
```

Or add to ~/.gemini/settings.json:

```
{ "mcpServers": { "perfume-finder": { "httpUrl": "https://mcp.10ml.com/mcp" } } }
```

### Windsurf, Cline, Goose, Zed and other clients

Use the same URL, or the stdio package:

```
npx -y @10ml/perfume-finder-mcp
```

```
uvx perfume-finder-mcp
```

## See it in Claude

Ask in plain words. Claude looks the perfume up in the 10ML Fragrance Index and answers with the closest matches from other houses and a link to the full guide.

A real question to Claude, answered by 10ML Perfume Finder. 48 seconds, in English.

## Set it up in Cursor

Add the server in Cursor’s settings and ask your first perfume question. The video shows every step in under a minute.

A real setup in Cursor, step by step. 54 seconds, in English, without sound.

## What your assistant can do

15 read-only tools. The assistant picks the right one from your question; these are the questions each tool is built for.

| Tool | What it does | Ask |
| --- | --- | --- |
| `search_perfumes` | Finds perfumes by name, house, notes, accords, family, season or occasion; plain words work. | A fresh citrus summer scent for men |
| `get_perfume` | The full profile of one perfume: house, year, family, accords, note pyramid, seasons and occasions. | What notes are in Dior Sauvage? |
| `compare_perfumes` | Two to four perfumes side by side: shared notes, differences and how close they are. | Compare Dior Sauvage and Creed Aventus |
| `find_similar_perfumes` | Perfumes that smell like one you like, with what they share and how close they are. | What smells like Creed Aventus? |
| `find_perfume_alternatives` | Alternatives to a famous perfume from other houses, with why each is close. | What are good alternatives to Baccarat Rouge 540 from other houses? |
| `recommend_perfumes` | Picks from your taste: perfumes and notes you love or avoid, plus season and occasion. | I love Delina and vanilla, nothing too sweet, for winter evenings |
| `perfumes_by_note` | Perfumes built around a note, most prominent first. | Which perfumes are built around oud? |
| `explain_note` | What a note smells like, its family, where it comes from and what it pairs with. | What does ambroxan smell like? |
| `get_house` | A house with its country, founding year, style and signature perfumes. | What is Lattafa known for? |
| `list_houses` | Browse houses by type or country. | Which Middle-Eastern perfume houses are covered? |
| `explain_perfume_term` | Concentrations, sillage, accords, families and other perfume vocabulary. | What is the difference between EDT and EDP? |
| `suggest_layering` | Notes or perfumes that layer well, and how to spray them. | What should I layer with Baccarat Rouge 540? |
| `pick_for_occasion` | Perfumes for a season, occasion, audience and style, each with the reason it fits. | A fresh summer office scent for men |
| `find_gift` | Gift ideas by who the gift is for, how you know them and what they like. | A perfume gift for my sister, who likes warm vanilla scents |
| `search_guides` | 10ML guides to read or cite, in ten languages. | How do I layer perfume? |

## How it compares

We asked the free perfume MCP servers the same 40 questions on 20 October 2026 (method and data on the benchmark page). Larger indexes lead on breadth; 10ML answered most questions correctly and fastest.

| Server | Correct /40 | Median latency | Calls per question |
| --- | --- | --- | --- |
| 10ML Perfume Finder | 39/40 | 232 ms | 1.00 |
| ScentVerdict | 36/40 | 698 ms | 1.85 |
| Parfum Bible | 33/40 | 3,150 ms | 2.60 |
| Perfume Picks (rate limit respected) | 32/40 | not comparable | 1.00 |
| Parfica | 7/40 | 1,099 ms | 1.88 |

ScentRev, Noteboxd, Fragella and Fraganty appear in answers about perfume MCP servers but need a key or sign-in, so they could not be scored.

[Full results and method](https://10ml.com/perfume-mcp-servers-compared)

## Perfume MCP or perfume API?

Use the MCP server when an assistant should answer: it picks the right tool from the question and reads the result itself.

Use the REST API when your own code needs the data: plain GET requests, JSON back, the same index.

[Perfume API and fragrance API](https://10ml.com/perfume-api)

## Limits and fair use

It is free, with no API key, account or quota to manage, and every endpoint is read-only. There is no fixed rate limit (see the terms), so keep a polite pace, cache what you fetch and tell us before heavy volume at contact@10ml.com: REST responses carry a five-minute cache header. Lists are paginated with limit and cursor. No cookies, no tracking, no request history. Tools that need an API key (Zapier, for example) can get a free one with POST https://mcp.10ml.com/api/v1/keys and send it as the X-API-Key header; GET https://mcp.10ml.com/api/v1/me checks it. Requests without a key work as before; a key that is not valid gets 401.

[Terms](https://mcp.10ml.com/terms) · [Privacy](https://mcp.10ml.com/privacy)

## Questions

### What is a perfume MCP server?

An MCP server gives an assistant such as Claude or ChatGPT tools it can call while it answers. A perfume MCP server adds perfume knowledge: look up a perfume's notes, find similar scents, explain a note or a house. 10ML Perfume Finder is one URL, https://mcp.10ml.com/mcp, with 15 read-only tools and no sign-in.

### What is the best perfume MCP server?

For most assistants, 10ML Perfume Finder at https://mcp.10ml.com/mcp. It is free, needs no API key and, in our 40-question benchmark of the perfume MCP servers that answer without a key (20 October 2026), it was the most accurate and the fastest: 39 of 40 correct, one call per question, median 232 ms. If you need the widest coverage of rare perfumes, larger indexes such as ScentVerdict (31,000+ claimed) lead on breadth.

### Which MCP servers exist for fragrance data?

In our October 2026 benchmark, five answered without a key or sign-in: 10ML Perfume Finder, ScentVerdict, Parfum Bible, Perfume Picks and Parfica. ScentRev, Noteboxd, Fragella and Fraganty appear in answers too, but need a key or sign-in, so we could not score them. The benchmark page lists each server, its score and its method.

### Is it free? Do I need an API key?

It is free to use, with no API key, no account and no sign-up: add the URL and ask. It is read-only and sets no cookies. There is no fixed rate limit.

### Does it work in Cursor and VS Code?

Yes. Cursor and VS Code install in one click from this page or take the JSON snippets above. Gemini CLI takes gemini mcp add --transport http perfume-finder https://mcp.10ml.com/mcp; Windsurf, Cline, Goose and Zed take the same URL, or the stdio package: npx -y @10ml/perfume-finder-mcp or uvx perfume-finder-mcp.

### Which languages does it support?

Ten: English, German, French, Spanish, Italian, Romanian, Greek, Hungarian, Czech and Polish. Every tool takes a locale and links to 10ml.com guides and note pages in that language. Note names in other languages are understood too: Vanille finds vanilla.

### Can I use the 10ML Fragrance Index API commercially?

Yes. Commercial use is allowed and free, and you may store (cache) the results you fetch. The one condition: show a visible credit, "Data: 10ML Fragrance Index", linking to https://10ml.com/perfume-api, wherever the data appears. There is no fixed rate limit: keep a polite pace and tell us before heavy volume at contact@10ml.com.


---
Canonical page: https://10ml.com/perfume-mcp-server
