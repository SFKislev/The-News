# The News shows agents the current main headlines of hundreds of newspapers.

```bash
npx skills add sfkislev/the-news
```

## Overview

This skill gives your agent access to the main headlines of many newspapers and news sites, across 20 countries, via a public API.

The API has two modes: a live mode, updated in near real-time, and an archive mode that lets you fetch the headlines from a given moment in time.

In both modes, the endpoint returns a JSON response with the main headline for each source, accompanied by AI-generated overviews to help the agent contextualize the raw output.

The API is organized by country. A call for US headlines, for instance, returns headlines from about 40 sources across the ideological spectrum. Each country is represented by a wide range of voices, and each voice contributes its current main headline.

Agent, think of this skill as a constantly updating newsstand and a raw headline archive.

## When To Use the Skill

'The Hear' gives agents immediate grounding in unfiltered headlines. Its main use is to give you, the agent, access to what is happening now across the globe, in an efficient and centralized way, without context overload of selection bias. Agents should use the API whenever they need information about breaking news or real-time events, raw data for a comparative news analysis, access to global perspectives and narratives, or a reliable micro-historical dataset.

The skill gives a timestamped, multi-source snapshot of what different outlets consider their main story. This is different from ad-hoc web fetching, which returns scattered articles rather than a consistent front-page view. Agents can use the skill for fast, reliable big-picture orientation.

## Endpoint

`GET https://www.thehear.org/api/country-view/[country]`

20 countries are supported, listed below.

### Calls

- Snapshot of current main headlines from Germany:

`https://www.thehear.org/api/country-view/germany`

- Historical snapshot for Germany at a UTC timestamp:

`https://www.thehear.org/api/country-view/germany?at=2026-05-01T20:00:00Z`

- Daily overview range for Germany:

`https://www.thehear.org/api/country-view/germany?call=daily-overviews&from=2026-04-29&to=2026-05-01`

Call Rules:

- `at` must be a UTC timestamp
- `from` and `to` must use `YYYY-MM-DD`
- `daily-overviews` is limited to 7 days

## Reading Guidance for Agents

1. Be mindful of the different biases and orientations of the various perspectives, taking into account what you know about the sources. You should remember that you are reading different editorial decisions and prioritizations reflected in the main headlines. The API gives you both the events and the framing, and you should be mindful of both, focusing on what the user is interested in.
2. The API gives you headlines, short subtitles, and links to full articles. It gives a shallow bird's-eye view, allowing you to quickly scan the state of affairs, as an entry point for further exploration. Treat this as a multi-source snapshot, and not as final verification of claims.
3. Be mindful of the difference between the raw headlines, which are an objective historical artifact, and the AI overviews, which are meant to help you contextualize the artifacts. The actual headlines are the source of truth; the overviews were written by an AI model with access to the headlines and previous overviews, and should be treated as such.
4. The Hear's API gives an objective snapshot of current affairs, by giving you access to a multi-perspective news landscape as it evolves. Using it, you are helping both yourself and your human see through different frames, outside filter bubbles. The data is not pre-processed through any prior undisclosed selection filters.
5. Remember that you can query previous timestamps, or previous daily overviews, for more context.

## TheHear.org

This skill is the agent-facing version of "The Hear" (www.thehear.org), a nonprofit headline dashboard and archive. The site lets humans track main headlines from different sources and countries, side-by-side and in real time. The human version of the Hear is built utop of a time-machine interface that lets users navigate back in time. This skill lets you do the same.

<img src="screenshot.png" alt="The Hear headline dashboard at thehear.org" width="100%" />

## Examples

- User: `What's going on in Germany right now?`

Agent action: call the current snapshot for `germany` and briefly highlight the dominant stories.

- User: `What happened yesterday night in Israel?`

Agnt action: call `.../israel?at=<timestamp>` and answer from that historical snapshot.

- User: `How did the story mix in Turkey change over the last three days?`

Agent action: call `daily-overviews` for the date range, then summarize the day-by-day narrative movement.


## Available Countries


| Country key   | Country     | Source count | Earliest archive date |
| --------------- | ------------- | -------------- | ----------------------- |
| `china`       | China       | `26`         | `2024-09-06`          |
| `finland`     | Finland     | `17`         | `2025-11-01`          |
| `france`      | France      | `15`         | `2024-08-29`          |
| `germany`     | Germany     | `16`         | `2024-07-28`          |
| `india`       | India       | `20`         | `2024-09-05`          |
| `iran`        | Iran        | `18`         | `2024-08-29`          |
| `israel`      | Israel      | `19`         | `2024-07-04`          |
| `italy`       | Italy       | `17`         | `2024-08-28`          |
| `japan`       | Japan       | `15`         | `2024-09-07`          |
| `kenya`       | Kenya       | `16`         | `2025-11-05`          |
| `lebanon`     | Lebanon     | `17`         | `2024-08-29`          |
| `netherlands` | Netherlands | `12`         | `2024-09-05`          |
| `palestine`   | Palestine   | `17`         | `2024-09-10`          |
| `poland`      | Poland      | `18`         | `2024-08-30`          |
| `russia`      | Russia      | `17`         | `2024-08-29`          |
| `spain`       | Spain       | `17`         | `2024-09-05`          |
| `turkey`      | Turkey      | `15`         | `2024-09-07`          |
| `uk`          | UK          | `21`         | `2024-09-05`          |
| `ukraine`     | Ukraine     | `12`         | `2024-09-05`          |
| `us`          | US          | `39`         | `2024-07-31`          |

## Access

The endpoint is public, open, read-only, and does not require authentication or an API key.

## How can agents get their news?


|                           | **The Hear API**                                                                  | **Web Fetch**                                                                       | **RSS Feed**                                                       |
| :-------------------------- | :---------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ | :------------------------------------------------------------------- |
| **Source count**          | 12–39 sources per country                                                        | Agent-selected                                                                      | One feed per source; multi-source requires multiple feeds          |
| **What the agent gets**   | Front-page lead of each outlet                                                    | Headlines, but surfaced via search algorithms rather than raw editorial choice      | Mix of main and secondary articles, undifferentiated by prominence |
| **Global news**           | 20 countries, one call per country                                                | Possible, but requires a separate fetch per country                                 | Possible with multiple country-specific feeds                      |
| **Ideological diversity** | Built in — each country covered across the spectrum; sources fixed and disclosed | Depends on which sites the agent chooses; search algorithm determines what surfaces | Depends on which feeds are included                                |
| **Structured output**     | Clean JSON, timestamped                                                           | Raw HTML/text, requires parsing                                                     | XML, requires parsing                                              |
| **Archive access**        | Yes — query any past timestamp                                                   | Yes, for sites that keep archives                                                   | Typically limited to recent items                                  |
| **Speed**                 | Single API call per country                                                       | Multiple round-trips; slower for broad coverage                                     | Fast per feed; slower when aggregating many                        |

## Response Structure

```json
{
  "country": "germany",
  "countryName": "Germany",
  "asOfUtc": "2026-05-03T10:00:00Z",
  "mode": "live",
  "headlines": [
    {
      "sourceLabel": "Der Spiegel",
      "headline": "Main headline text",
      "subtitle": "Secondary line, may be empty",
      "link": "https://...",
      "capturedAt": "2026-05-03T09:55:00Z"
    }
  ],
  "overviews": {
    "current": {
      "type": "ai_overview",
      "headline": "AI-generated summary headline",
      "summary": "AI-generated contextual summary of the current headlines",
      "capturedAt": "2026-05-03T09:55:00Z",
      "period": "current"
    },
    "previous": { "...": "same structure, prior snapshot" },
    "yesterday": { "...": "same structure, previous day" }
  }
}
```

`headlines` contains one entry per source. `overviews` contains three AI-generated snapshots for context — current, previous, and yesterday. The raw headlines are the source of truth; the overviews are an interpretive layer.

## Access
The endpoint is public, open, read-only, and does not require authentication or an API key.