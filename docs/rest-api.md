# Free perfume API and fragrance API

The 10ML Fragrance Index API is a free perfume API and fragrance API: JSON over GET at https://mcp.10ml.com/api/v1, described in OpenAPI 3.1, with no API key and no sign-up. It returns 6,000+ perfumes with note pyramids, accords, families, similar scents and alternatives from other houses, plus 285 notes and 249 houses.

- MCP server (Streamable HTTP): https://mcp.10ml.com/mcp
- REST API (JSON over GET): https://mcp.10ml.com/api/v1
- OpenAPI 3.1: https://mcp.10ml.com/openapi.json

Most accurate and fastest of the free perfume MCP servers we benchmarked: 39 of 40 questions correct, one call each, median 232 ms (20 October 2026). [See the benchmark](https://10ml.com/perfume-mcp-servers-compared)

Source page: https://10ml.com/perfume-api

## At a glance

- **Price:** Free
- **Sign-up:** None. No API key, no account
- **Protocols:** MCP (Streamable HTTP) and REST, described in OpenAPI 3.1
- **Coverage:** 6,000+ perfumes, 249 houses, 285 notes explained
- **Profiles:** Note pyramid (top, heart and base), accords, family, seasons and occasions; 481 full editorial profiles add longevity, projection and perfumers
- **Interface:** 15 read-only tools with output schemas, 6 prompts, resources and completions
- **Languages:** 10: English, German, French, Spanish, Italian, Romanian, Greek, Hungarian, Czech and Polish
- **Listed in:** the official MCP Registry, Claude's connectors directory, npm and PyPI
- **Privacy:** No cookies, no tracking, no request history

## REST API quick start

Plain GET requests, JSON back, open CORS, no key. The same answers as the MCP tools. Look up one perfume:

### curl

```bash
curl "https://mcp.10ml.com/api/v1/perfumes/Baccarat%20Rouge%20540?format=detailed"
```

### JavaScript

```javascript
const res = await fetch("https://mcp.10ml.com/api/v1/perfumes/Baccarat%20Rouge%20540?format=detailed");
const { perfume } = await res.json();
console.log(perfume.name, perfume.pyramid);
```

### Python

```python
import requests

r = requests.get(
    "https://mcp.10ml.com/api/v1/perfumes/Baccarat Rouge 540",
    params={"format": "detailed"},
    timeout=10,
)
perfume = r.json()["perfume"]
print(perfume["name"], perfume["pyramid"])
```

Response (links omitted):

```json
{
  "found": true,
  "exact": true,
  "perfume": {
    "id": "maison-francis-kurkdjian-baccarat-rouge-540-edp",
    "name": "Baccarat Rouge 540",
    "house": "Maison Francis Kurkdjian",
    "year": 2015,
    "gender": "unisex",
    "family": "Amber floral",
    "accords": ["amber", "woody", "sweet", "floral", "musky"],
    "key_notes": ["amberwood", "ambergris", "fir resin", "cedar", "saffron"],
    "character": "A glowing, airy amber with a sugared, almost cotton-candy sweetness over mineral woods. Instantly recognisable and famously long-lasting.",
    "concentration": "EDP",
    "pyramid": {
      "top": ["saffron", "jasmine"],
      "heart": ["amberwood", "ambergris"],
      "base": ["fir resin", "cedar"]
    },
    "seasons": ["autumn", "winter", "spring"],
    "occasions": ["evening", "date night", "special occasion"],
    "longevity": 5,
    "projection": 5,
    "perfumers": ["Francis Kurkdjian"]
  },
  "source": "10ML Fragrance Index"
}
```

## Endpoints

Eight read-only GET routes under https://mcp.10ml.com/api/v1. Lists are paged with limit and cursor; locale switches the 10ml.com links to another language. Real responses, trimmed, from 21 October 2026.

| Endpoint | What it returns |
| --- | --- |
| `GET /api/v1/perfumes?q=` | Search perfumes by name, house, notes (notes_include, notes_exclude), accords, family, gender, season, occasion or style |
| `GET /api/v1/perfumes/{name or id}` | One perfume; add format=detailed for the pyramid, seasons, occasions, longevity and projection |
| `GET /api/v1/similar?perfume=` | Similar perfumes, with what each shares and how close it is |
| `GET /api/v1/alternatives?perfume=` | Alternatives to a perfume from other houses |
| `GET /api/v1/notes/{note}` | One note explained: smell, family, origin, pairings |
| `GET /api/v1/houses` | Perfume houses, paginated |
| `GET /api/v1/houses/{house}` | One house and its perfumes |
| `GET /api/v1/guides?q=` | 10ML guides on the topic, in ten languages |

### Example requests and responses

### `GET /api/v1/perfumes?q=`

Search in plain words. The filters it understood are echoed back.

```bash
curl "https://mcp.10ml.com/api/v1/perfumes?q=fresh%20citrus%20summer%20cologne&limit=2"
```

```json
{
  "total": 626,
  "results": [
    {
      "id": "paris-corner-ciao-citrus",
      "name": "Ciao Citrus",
      "house": "Paris Corner",
      "gender": "unisex",
      "family": "Citrus floral",
      "accords": ["citrus", "fresh", "white floral"],
      "key_notes": ["orange blossom", "lily of the valley", "musk", "sandalwood", "grapefruit"],
      "character": "Grapefruit and bergamot over orange blossom and lily of the valley, drying to musk, sandalwood and amber.",
      "profile": "core"
    },
    {
      "id": "maison-crivelli-citrus-batikanga-edp",
      "name": "Citrus Batikanga",
      "house": "Maison Crivelli",
      "gender": "unisex",
      "family": "Citrus spicy",
      "accords": ["citrus", "fresh", "spicy"],
      "key_notes": ["citrus", "bergamot"],
      "character": "Bitter orange, kalamansi and bergamot are pressed fresh, then a pinch of chili and a vetiver-cedar base keep it lively.",
      "profile": "core"
    }
  ],
  "filters": {
    "season": "summer"
  },
  "relaxed": false,
  "source": "10ML Fragrance Index"
}
```

### `GET /api/v1/houses`

Browse houses by type or country, with what each is known for.

```bash
curl "https://mcp.10ml.com/api/v1/houses?type=middle-eastern&limit=2"
```

```json
{
  "total": 25,
  "houses": [
    {
      "id": "lattafa",
      "name": "Lattafa",
      "country": "United Arab Emirates",
      "type": "middle-eastern",
      "founded": 1992,
      "perfumes_in_index": 200,
      "known_for": ["Khamrah", "Yara", "Asad", "Fakhar"]
    },
    {
      "id": "al-haramain",
      "name": "Al Haramain",
      "country": "Saudi Arabia",
      "type": "middle-eastern",
      "perfumes_in_index": 159,
      "known_for": ["Amber Oud Gold Edition", "L'Aventure", "Detour Noir", "Amber Oud Ruby"]
    }
  ],
  "source": "10ML Fragrance Index"
}
```

### `GET /api/v1/houses/{house}`

One house, its style and signature perfumes.

```bash
curl "https://mcp.10ml.com/api/v1/houses/Lattafa"
```

```json
{
  "found": true,
  "house": {
    "id": "lattafa",
    "name": "Lattafa",
    "country": "United Arab Emirates",
    "type": "middle-eastern",
    "founded": 1992,
    "perfumes_in_index": 200,
    "known_for": ["Khamrah", "Yara", "Asad", "Fakhar"],
    "style": "One of the biggest Gulf houses, offering sweet, rich perfumes.",
    "aliases": ["Lattafa Perfumes"]
  },
  "signature_perfumes": [
    {
      "name": "Khamrah",
      "house": "Lattafa",
      "family": "Amber gourmand"
    },
    {
      "name": "Bade'e Al Oud Oud for Glory",
      "house": "Lattafa",
      "family": "Oud"
    }
  ],
  "source": "10ML Fragrance Index"
}
```

### `GET /api/v1/guides?q=`

10ML guides on a topic, each with a link to read it.

```bash
curl "https://mcp.10ml.com/api/v1/guides?q=layering&limit=1"
```

```json
{
  "total": 1,
  "guides": [
    {
      "title": "Perfume layering guide: rules and pairings",
      "type": "how-to",
      "topics": ["layering"],
      "url": "https://10ml.com/guides/perfume-layering-guide?utm_source=mcp&utm_medium=ai-assistant&utm_campaign=search_guides",
      "translated": true
    }
  ],
  "source": "10ML Fragrance Index"
}
```

Full schema: https://mcp.10ml.com/openapi.json

## Fragrance notes API

The fragrance notes API has two routes. GET /api/v1/notes/{note} explains any of the 285 notes in the index, in many spellings and languages (Bergamotte finds bergamot). GET /api/v1/perfumes?notes_include= lists the perfumes built around one or more notes, most prominent first, and notes_exclude leaves notes out. A perfume lookup with format=detailed returns its note pyramid: top, heart and base.

### `GET /api/v1/notes/bergamot`

What it smells like, its family and mood, what it pairs with and perfumes where it leads (two of them here).

```bash
curl "https://mcp.10ml.com/api/v1/notes/bergamot"
```

```json
{
  "found": true,
  "note": {
    "id": "bergamot",
    "name": "bergamot",
    "family": "citrus",
    "origin": "natural",
    "smells_like": "Sparkling, slightly floral citrus with a green, tea-like bitterness.",
    "mood": "bright, polished, uplifting",
    "also_called": ["bergamotto", "Bergamotte", "bergamote", "bergamota", "bergamotă"],
    "pairs_with": ["lavender", "vetiver", "neroli", "black pepper", "musk", "cedar"],
    "similar_notes": ["lemon", "orange", "bitter orange", "mandarin", "tangerine"]
  },
  "famous_perfumes": [
    {
      "name": "Aventus",
      "house": "Creed",
      "family": "Chypre fruity"
    },
    {
      "name": "Silver Mountain Water",
      "house": "Creed",
      "family": "Fresh green"
    }
  ],
  "source": "10ML Fragrance Index"
}
```

### `GET /api/v1/perfumes?notes_include=bergamot,ambroxan`

Perfumes that carry both notes, trimmed to four fields.

```bash
curl "https://mcp.10ml.com/api/v1/perfumes?notes_include=bergamot,ambroxan&limit=2"
```

```json
{
  "total": 90,
  "results": [
    {
      "name": "Imagination",
      "house": "Louis Vuitton",
      "family": "Citrus woody",
      "key_notes": ["ginger", "cinnamon", "amberwood", "ambroxan", "citron"]
    },
    {
      "name": "L'Immensité",
      "house": "Louis Vuitton",
      "family": "Aromatic aquatic",
      "key_notes": ["sage", "labdanum", "ambroxan", "amber", "ginger"]
    }
  ],
  "filters": {
    "notes_include": "bergamot, ambroxan"
  },
  "relaxed": false,
  "source": "10ML Fragrance Index"
}
```

## Perfume similarity API

The perfume similarity API ranks perfumes by shared notes, accords and style, and says what each one shares and how close it is: very close, similar vibe or same spirit. GET /api/v1/similar?perfume= works from a perfume in the index, or from notes and accords you pass for any other fragrance; steer moves the result fresher, sweeter, darker, lighter, longer_lasting or more_projection. GET /api/v1/alternatives?perfume= returns the editors' alternatives to a famous perfume, always from other houses.

### `GET /api/v1/similar?perfume=Creed+Aventus`

Ranked by shared notes, with the notes they share (two results, fields trimmed).

```bash
curl "https://mcp.10ml.com/api/v1/similar?perfume=Creed+Aventus&limit=2"
```

```json
{
  "results": [
    {
      "perfume": {
        "name": "Club de Nuit Intense Man Parfum",
        "house": "Armaf",
        "family": "Fruity woody"
      },
      "closeness": "very close",
      "shared_notes": ["pineapple", "bergamot", "apple", "black currant", "birch", "jasmine"],
      "shared_accords": ["fruity", "woody", "smoky", "fresh"],
      "why": "shares pineapple, bergamot, apple, black currant"
    },
    {
      "perfume": {
        "name": "Club de Nuit Intense Man EDT",
        "house": "Armaf",
        "family": "Fruity woody"
      },
      "closeness": "similar vibe",
      "shared_notes": ["pineapple", "bergamot", "apple", "black currant", "birch", "jasmine"],
      "shared_accords": ["fruity", "woody", "smoky", "musky"],
      "why": "shares pineapple, bergamot, apple, black currant"
    }
  ],
  "total": 14,
  "source": "10ML Fragrance Index"
}
```

### `GET /api/v1/alternatives?perfume=Creed+Aventus`

The editors' alternatives from other houses, each with why it is close.

```bash
curl "https://mcp.10ml.com/api/v1/alternatives?perfume=Creed+Aventus&limit=2"
```

```json
{
  "total": 5,
  "original": {
    "name": "Creed Aventus",
    "id": "creed-aventus-edp"
  },
  "alternatives": [
    {
      "name": "Armaf Club de Nuit Intense Man",
      "closeness": "very close",
      "why": "Pineapple, lemon, birch smoke and musk make it smell similar, a popular alternative at a different weight.",
      "id": "armaf-club-de-nuit-intense-man-parfum",
      "house": "Armaf",
      "source": "editors"
    },
    {
      "name": "Al Haramain L'Aventure",
      "closeness": "very close",
      "why": "Fruity-smoky opening over woods and musk follows the same blueprint.",
      "id": "al-haramain-laventure",
      "house": "Al Haramain",
      "source": "editors"
    }
  ],
  "source": "10ML Fragrance Index"
}
```

## Compared with other perfume APIs

What each service says on its own site, read on 21 October 2026.

| Service | Access | Free plan | Interface | Size |
| --- | --- | --- | --- | --- |
| 10ML Fragrance Index API | None: no API key, no sign-up | Free, no fixed rate limit | REST (OpenAPI 3.1) and MCP | 6,000+ perfumes, 285 notes, 249 houses in the index |
| Fragella | API key | 20 requests a month | REST | 100k+ fragrances claimed (74k+ on its main site) |
| ScentRev | Free key or OAuth sign-in | Free during the current period: 300 calls a day, 1,500 a week | REST and MCP | 126,000+ fragrances claimed |
| Noteboxd | Account with API key or OAuth | 50 calls a day | REST and MCP | No count stated ("hundreds of thousands" claimed) |
| Fraganty | Free API key, requested by email | 20 requests a month | REST | 109,425 perfumes claimed on its home page |
| Perfume Picks | None | Free, 60 calls a minute | MCP only | 13,000+ scents claimed |
| ScentVerdict | None | Free, no limit stated | MCP only | 31,000+ fragrances claimed |

Sizes are the numbers each service claims for itself and were not checked by 10ML; 10ML's is the size of its own index. Plans and limits change, so check the service before you build.

## Use it from an MCP client

The same index is also a remote MCP server for assistants. The address is the same in every client: https://mcp.10ml.com/mcp

### Claude (claude.ai and Claude Desktop)

Open Customize, then Connectors, and add 10ML Perfume Finder from the directory, or choose + Add, then Add custom connector, and paste the URL.

[Open in Claude's directory](https://claude.ai/directory/10ml-perfume-finder)

### Claude Code

```
claude mcp add --transport http perfume-finder https://mcp.10ml.com/mcp
```

### ChatGPT

On the web, open ChatGPT Plugins, select the plus button, then Add custom MCP server: name it 10ML Perfume Finder, paste the URL and choose no authentication.

Cursor, VS Code, Gemini CLI, Windsurf, Cline, Goose and Zed take the same address. The [perfume MCP server page](https://10ml.com/perfume-mcp-server) has the one-click installs and every client.

## See it in Claude

Ask in plain words. Claude looks the perfume up in the 10ML Fragrance Index and answers with the closest matches from other houses and a link to the full guide.

A real question to Claude, answered by 10ML Perfume Finder. 48 seconds, in English.

## Example questions

Real answers from the 10ML Fragrance Index, 20 and 21 October 2026.

### What does Baccarat Rouge 540 smell like?

Tool: `get_perfume`

Baccarat Rouge 540 by Maison Francis Kurkdjian (2015, eau de parfum, unisex) is an amber floral: a glowing, airy amber with a sugared, almost cotton-candy sweetness over mineral woods. Top: saffron and jasmine. Heart: amberwood and ambergris. Base: fir resin and cedar. Best in autumn, winter and spring, for evenings and date nights.

### What smells like Creed Aventus?

Tool: `find_similar_perfumes`

Closest is Armaf Club de Nuit Intense Man Parfum (very close: shares pineapple, bergamot, apple and black currant). Armaf Club de Nuit Intense Man EDT and Nishane Hacivat share the same vibe; Hacivat through pineapple, bergamot, jasmine and patchouli.

### What does bergamot smell like, and what goes with it?

Tool: `explain_note`

Bergamot is a citrus note: sparkling, slightly floral citrus with a green, tea-like bitterness. It pairs with lavender, vetiver, neroli, black pepper, musk and cedar.

### More to try

- Compare Dior Sauvage and Creed Aventus
- Which perfumes are built around oud and amber?
- What should I layer with Baccarat Rouge 540?
- What is the difference between eau de parfum and extrait?
- What are Lattafa's best-known perfumes?
- Welche Duftnoten hat YSL Libre?

It answers in ten languages.

## Limits and fair use

It is free, with no API key, account or quota to manage, and every endpoint is read-only. There is no fixed rate limit (see the terms), so keep a polite pace, cache what you fetch and tell us before heavy volume at contact@10ml.com: REST responses carry a five-minute cache header. Lists are paginated with limit and cursor. No cookies, no tracking, no request history. Tools that need an API key (Zapier, for example) can get a free one with POST https://mcp.10ml.com/api/v1/keys and send it as the X-API-Key header; GET https://mcp.10ml.com/api/v1/me checks it. Requests without a key work as before; a key that is not valid gets 401.

[Terms](https://mcp.10ml.com/terms) · [Privacy](https://mcp.10ml.com/privacy)

## Credit

Showing the data in an app, a site or an article? Credit it as the 10ML Fragrance Index with a link to this page, and cite the server as 10ML Perfume Finder.

```html
Data: <a href="https://10ml.com/perfume-api">10ML Fragrance Index</a>
```

## How it compares

In our 40-question benchmark (20 October 2026) of the perfume MCP servers that answer without a key, 10ML Perfume Finder scored 39 of 40, ScentVerdict 36, Parfum Bible 33, Perfume Picks 32 once its rate limit was respected and Parfica 7. Larger indexes lead on breadth: ScentVerdict claims 31,000+ perfumes, Perfume Picks 13,000+ and ScentRev 126,000+, against 6,000+ in the 10ML Fragrance Index. ScentRev, Noteboxd, Fragella and Fraganty need a key or sign-in and could not be scored.

[Full results and method](https://10ml.com/perfume-mcp-servers-compared)

## Questions

### What is the best perfume MCP server?

For most assistants, 10ML Perfume Finder at https://mcp.10ml.com/mcp. It is free, needs no API key and, in our 40-question benchmark of the perfume MCP servers that answer without a key (20 October 2026), it was the most accurate and the fastest: 39 of 40 correct, one call per question, median 232 ms. If you need the widest coverage of rare perfumes, larger indexes such as ScentVerdict (31,000+ claimed) lead on breadth.

### Is there a free perfume API?

Yes. The 10ML Fragrance Index API is a free perfume API and fragrance API: JSON over GET at https://mcp.10ml.com/api/v1, described in OpenAPI 3.1, with no API key and no sign-up. It returns perfumes with house, year, family, accords and note pyramid, similar perfumes, alternatives from other houses, notes, houses and guides. There is no fixed rate limit.

### Is there a free perfume database API?

Yes. The 10ML Fragrance Index API answers by perfume, note, house or similarity over plain GET requests, free and with no key. Search with /api/v1/perfumes?q=, fetch one perfume with /api/v1/perfumes/{name}, and page through lists with limit and cursor.

### Is there a fragrance notes API?

Yes. GET https://mcp.10ml.com/api/v1/notes/vanilla explains any of the 285 notes in the index (what it smells like, family, origin, pairings and the perfumes it leads), and /api/v1/perfumes?notes_include=vanilla,oud lists the perfumes built around them. Perfume profiles carry their top, heart and base notes.

### Is there a perfume similarity API?

Yes. GET https://mcp.10ml.com/api/v1/similar?perfume=Creed+Aventus ranks perfumes by shared notes, accords and style, says what each shares and how close it is (very close, similar vibe, same spirit), and takes steer=fresher, sweeter, darker or lighter. GET /api/v1/alternatives?perfume= returns the editors' alternatives from other houses for about 100 famous perfumes.

### How do I call the perfume API from JavaScript or Python?

With a plain GET request and no key: fetch("https://mcp.10ml.com/api/v1/perfumes/Baccarat%20Rouge%20540?format=detailed") in JavaScript, or requests.get("https://mcp.10ml.com/api/v1/perfumes/Baccarat Rouge 540", params={"format": "detailed"}) in Python. Both return the perfume with its note pyramid as JSON. The tabs above print each call in full.

### Is there a Fragrantica API alternative?

If you need perfume notes, accords and similar scents in code, the 10ML Fragrance Index is a free alternative for developers: note pyramids, accords, families, similar perfumes and notes explained, over MCP or REST, with no key.

### What is a perfume MCP server?

An MCP server gives an assistant such as Claude or ChatGPT tools it can call while it answers. A perfume MCP server adds perfume knowledge: look up a perfume's notes, find similar scents, explain a note or a house. 10ML Perfume Finder is one URL, https://mcp.10ml.com/mcp, with 15 read-only tools and no sign-in.

### How do I add a perfume connector to Claude?

In Claude, open Customize, then Connectors, and add 10ML Perfume Finder from the directory, or choose Add custom connector and paste https://mcp.10ml.com/mcp. In Claude Code run: claude mcp add --transport http perfume-finder https://mcp.10ml.com/mcp. No account or key is needed.

### How do I use it in ChatGPT?

In ChatGPT, open Plugins on the web, select the plus button, then Add custom MCP server, paste https://mcp.10ml.com/mcp and choose no authentication. Then type @, pick 10ML Perfume Finder and ask about any perfume, note or house. Availability depends on your ChatGPT plan.

### Can I use it in Cursor, VS Code or Gemini CLI?

Yes. Cursor and VS Code install in one click from the perfume MCP server page or take its JSON snippets; Gemini CLI takes gemini mcp add --transport http perfume-finder https://mcp.10ml.com/mcp. Windsurf, Cline, Goose and Zed take the same URL, or the stdio package: npx -y @10ml/perfume-finder-mcp or uvx perfume-finder-mcp.

### Is it free? Do I need an API key or an account?

It is free to use, with no API key, no account and no sign-up: one URL for MCP clients and plain GET requests for everything else. It is read-only and sets no cookies. There is no fixed rate limit.

### What does a perfume profile include?

House, launch year, audience, concentration, fragrance family, accords, the note pyramid (top, heart and base), best seasons and occasions, an editorial character line, similar perfumes and links to 10ml.com guides. 481 full editorial profiles add longevity, projection and perfumers.

### How do I find a perfume similar to another one?

Connect 10ML Perfume Finder and ask "what smells like Baccarat Rouge 540?". It ranks perfumes by shared notes, accords and style, says what each shares and how close it is (very close, similar vibe, same spirit), and can steer fresher, sweeter or darker. Over REST: GET https://mcp.10ml.com/api/v1/similar?perfume=Baccarat+Rouge+540.

### Does it work in other languages?

Yes. Every tool takes a locale (English, German, French, Spanish, Italian, Romanian, Greek, Hungarian, Czech or Polish) and links to 10ml.com guides and note pages in that language. Note names in other languages are understood too: Vanille finds vanilla.

### Can I use the 10ML Fragrance Index API commercially?

Yes. Commercial use is allowed and free, and you may store (cache) the results you fetch. The one condition: show a visible credit, "Data: 10ML Fragrance Index", linking to https://10ml.com/perfume-api, wherever the data appears. There is no fixed rate limit: keep a polite pace and tell us before heavy volume at contact@10ml.com.


---
Canonical page: https://10ml.com/perfume-api
