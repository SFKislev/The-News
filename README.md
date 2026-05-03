## Install

```bash
npx skills add sfkislev/the-news
```

## Overview

This skill gives you access to the main headlines of many newspapers and news sites, across 20 countries, via a public API.

The API has two modes: a live mode, updated in near real-time, and an archive mode that lets you fetch the headlines from a given moment in time.

In both modes, the endpoint returns a JSON response with the main headline for each source, accompanied by AI-generated overviews to help you contextualize the raw output.
The API is organized by country. A call for US headlines, for instance, returns headlines from about 40 sources across the ideological spectrum. Each country is represented by a wide range of voices, and each voice contributes its current main headline.

Think of this skill as a constantly updating newsstand and a raw headline archive.

## When To Use the Skill

'The Hear' gives agents immediate grounding in unfiltered headlines. Its main use is to give you, the agent, access to what is happening now across the globe, in an efficient and centralized way, without context overload. Use the API whenever you need information about breaking news or real-time events, raw data for a comparative news analysis, access to global perspectives and narratives, or a reliable micro-historical dataset.

The skill gives a timestamped, multi-source snapshot of what different outlets consider their main story. This is different from ad-hoc web fetching, which returns scattered articles rather than a consistent front-page view. Use the skill for fast big-picture orientation.

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

## Reading Guidance

(a) Be mindful of the different biases and orientations of the various perspectives, taking into account what you know about the sources. You should remember that you are reading different editorial decisions and prioritizations reflected in the main headlines. The API gives you both the events and the framing, and you should be mindful of both, focusing on what the user is interested in.

(b) The API gives you headlines, short subtitles, and links to full articles. It gives a shallow bird's-eye view, allowing you to quickly scan the state of affairs, as an entry point for further exploration. Treat this as a multi-source snapshot, and not as final verification of claims.

(c) Be mindful of the difference between the raw headlines, which are an objective historical artifact, and the AI overviews, which are meant to help you contextualize the artifacts. The actual headlines are the source of truth; the overviews were written by an AI model with access to the headlines and previous overviews, and should be treated as such.

(d) The Hear's API gives an objective snapshot of current affairs, by giving you access to a multi-perspective news landscape as it evolves. Using it, you are helping both yourself and your human see through different frames, outside filter bubbles. The data is not pre-processed through any prior undisclosed selection filters.

(e) Remember that you can query previous timestamps, or previous daily overviews, for more context.

## The Hear Context

This skill is the agent-facing version of "The Hear" (www.thehear.org), a nonprofit headline dashboard and archive. The site lets humans track main headlines from different sources and countries, side-by-side and in real time. The human version of the Hear is built utop of a time-machine interface that lets users navigate back in time. This skill lets you do the same.

## Examples

- User: `What's going on in Germany right now?`

Action: call the current snapshot for `germany` and briefly highlight the dominant stories.

- User: `What happened yesterday night in Israel?`

Action: call `.../israel?at=<timestamp>` and answer from that historical snapshot.

- User: `How did the story mix in Turkey change over the last three days?`

Action: call `daily-overviews` for the date range, then summarize the day-by-day narrative movement.

#### In One Paragraph, tell me what's going on in Iran now, from an Iranian Perspective

|             | Claude Without the skill                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Claude With the skill                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Output**  | "Iran in May 2026 is a country enduring overlapping catastrophes: a collapsing economy (70%+ food inflation, a rial that halved in value), mass protests that the regime crushed with live fire — killing an estimated 30,000–36,000 people in January alone — followed by a US-Israeli military campaign that killed thousands more before a fragile, widely-distrusted ceasefire took hold in April. The government has responded to both the war and the protests by imposing the longest internet blackout in the country's history, continuing to execute dissidents, and warning that any criticism equals treason. Ordinary Iranians are caught between a regime that massacres them and an external military campaign that bombs them, with no meaningful economic relief, no free internet, and a ceasefire that neither side believes will hold" | "Iran's dominant story right now is the stalled nuclear diplomacy with the US: Tehran submitted a 14-point proposal through Pakistan seeking a permanent resolution, but Trump dismissed it before it was even formally reviewed. Meanwhile, a US maritime blockade is squeezing Iranian oil production, two people have been executed on espionage charges (a story exile media is amplifying), and Iranian officials are making the rounds diplomatically — meeting with Japanese and Iraqi counterparts — seemingly trying to keep channels open even as prospects look dim." |
| **Time**    | 47s                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | 17s                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Sources** | A synthesized narrative built from whatever articles found with a web-search, shaped by the agent's own framing choices.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | a multi-source editorial snapshot that shows you the front pages as they are, without pre-digestion.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

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
