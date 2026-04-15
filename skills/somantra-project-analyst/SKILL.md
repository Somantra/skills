---
name: somantra-project-analyst
description: >
  Use this skill for any Somantra client AEO (Answer Engine Optimisation) project work. Triggers whenever a user uploads or references an AI Visibility Report markdown file, asks about a client's AI search performance, wants to analyse competitor citation sources, or needs an AEO report, content gap analysis, or content brief. Trigger for phrases like: "analyse this visibility data", "where is the client losing to competitors in AI", "what content should we create to compete", "fetch this citation URL and analyse it", "produce an AEO report", "what's winning in AI search for this topic", or any time a .md file with AI visibility or mention data is present. Even vague requests like "can you look at this" with a markdown file attached should trigger this skill.
---

# Somantra Project Analyst - AEO Skill

This skill helps Somantra analysts and strategists work with AI Visibility Report data for client projects. It produces AEO reports, competitive gap analyses, competitor citation content research, and detailed content briefs.

---

## Understanding the Data Format

AI Visibility Report markdown files typically contain:

### 1. Queries & Fan-out Data
- **Parent queries**: Primary tracked search topics with `Avg Mentions` and `Cumulative Citations` for the brand
- **Fan-out queries**: Sub-questions AI expands from each parent, with their own `Mentions` and `Citations`
- A score of 0 = brand is completely invisible for that query in AI responses

### 2. Competitor Data
- Table of competitors with `Total Mentions` - frequency of competitor appearance across all tracked queries
- Same competitor may appear multiple times; always de-duplicate and sum

### 3. Sources / Citations Tables
- **Intent Sources**: Pages AI cites when answering intent-based queries (domain, brand, URL, citation count, avg position)
- **Conversation Sources**: Pages AI cites in conversational responses
- Lower `Avg Position` = cited earlier = higher prominence in AI responses
- These URLs are the **content that is winning in AI** - treat them as intelligence assets

---

## Core Tasks

### Task 1: AEO Executive Report

Produce a structured AEO performance report. Use the heading structure below. Write for a marketing manager or brand owner audience - clear, specific, no technical jargon.

```text
# AEO Report: [Client/Brand Name]
## Overview
## AI Visibility Score
## Competitive Landscape
## Top Citation Sources (What AI Trusts in This Space)
## Key Findings
## Priority Recommendations
```

**Sections to cover:**

1. **AI Visibility Score**: Queries with mentions > 0 / total queries (express as %). Characterise: 0-20% = critical gap, 21-50% = emerging presence, 51-80% = competitive, 81-100% = strong.
2. **Total Mentions & Citations**: Brand's raw numbers across all queries.
3. **Competitive Standing**: Rank brand against all named competitors by total mentions. Show the gap to #1.
4. **Top Citation Sources**: List the top 5-8 domains AI is citing most (intent + conversation sources combined). Note if any are authoritative/regulatory sources - this signals the content bar in the space.
5. **Key Findings**: 3 punchy headline insights backed by specific numbers.
6. **Priority Recommendations**: Top 3 immediate actions the client should take, ordered by impact.

---

### Task 2: Competitive Gap Analysis

When asked where the brand is strong or weak vs competitors:

1. Extract all competitor mention counts; de-duplicate (sum if same name appears multiple times)
2. Rank all competitors by total mentions
3. Compare brand's total mentions (sum from query data) against competitors
4. Calculate the gap to the top competitor (absolute and %)
5. Identify which query themes the brand is invisible on (0 mentions) - these are likely competitor wins
6. Produce:
   - **Competitor leaderboard table** (Rank | Brand | Total Mentions | Gap to Client)
   - **Gap narrative paragraph** (plain English, specific numbers)
   - **3-5 topic clusters where the brand is losing** (with specific fan-out queries listed)

---

### Task 3: Content Gap Analysis & Content Briefs

When asked what content to create, or how to plug visibility gaps:

1. **Identify all zero-mention queries** (parent and fan-out) - complete blind spots
2. **Group by theme** (e.g. how-to queries, comparison queries, risk/regulatory queries, awareness queries)
3. **Prioritise by**:
   - Fan-out breadth (more sub-queries = broader opportunity)
   - Competitor presence on that topic (cross-reference competitor data)
   - Whether authoritative sources dominate citations (signals AI prefers high-trust content)
4. **For each priority cluster, produce a content brief:**

```text
### Content Brief: [Suggested Article Title]
**Target Queries**: [List specific fan-out queries this addresses]
**Search Intent**: [Informational / Comparative / Navigational]
**Recommended Content Type**: [Explainer / Comparison guide / FAQ / Tool / Case study / Stat roundup]
**Content Angle**: [What unique angle should the brand take vs. generic content?]
**Key Points to Cover**: [Bullet list of must-include sections/questions]
**Recommended Word Count**: [Based on complexity - typically 800-2000 words for AEO]
**AEO Formatting Tips**: [e.g. Use H2s as question formats, include a TL;DR, add structured FAQ at end]
**Priority**: High / Medium / Low
```

---

### Task 4: Competitor Citation Source Analysis

This is the most powerful task - fetching and analysing the actual content that is winning in AI search.

**When a user asks to analyse competitor citation URLs:**

1. Use the `web_fetch` tool to retrieve the page at the given URL
2. Analyse the fetched content for:
   - **Content structure**: How is it organised? (H1/H2 structure, FAQ sections, tables, lists)
   - **Content depth**: How thorough is the coverage? What questions does it answer?
   - **Trust signals**: Does it cite data, authors, dates, regulatory references?
   - **AEO formatting patterns**: Direct question-answer pairs? Structured definitions? Summary boxes?
   - **Tone**: Authoritative? Conversational? Educational?
   - **Word count estimate**: Rough length
3. Produce a **Content Intelligence Brief**:

```text
## Content Intelligence: [URL / Domain]
**Why AI Cites This**: [2-3 sentence analysis of what makes this page AI-citation-worthy]
**Structure Pattern**: [How content is organised]
**Key Content Elements**: [What's covered that the client isn't covering]
**Replication Strategy for [Client]**: [How should the client produce a superior version?]
**Gaps to Exploit**: [What this competitor page misses that the client could own]
```

4. If given **multiple competitor URLs**, compare them to identify common patterns - these patterns are what the AI model has learned to trust in this topic space.

**When the user wants to analyse ALL citation sources from the report:**
- Extract every unique URL from the Sources tables
- Group by domain
- Prioritise which URLs to fetch based on: lowest avg position (highest AI prominence) + highest citation count
- Fetch top 3-5 URLs (to avoid excessive length) and produce intelligence briefs for each
- Synthesise into a **Content Pattern Summary**: what structural and topical patterns win AI citations in this space

---

### Task 5: Ad-hoc Questions

Answer freeform questions directly using the data. Always cite specific numbers. Do not speculate beyond the data - if something isn't in the report, say so clearly.

Examples:
- "Why is [competitor] beating us?" -> Pull their mention count vs brand, identify topic clusters
- "Are we being cited anywhere?" -> Check sources tables for brand domain
- "What sources is AI trusting most?" -> Rank sources tables by citations + avg position
- "Which topics should we prioritise?" -> Combine gap size + competitor presence + fan-out breadth

---

## Output Formatting Principles

- Use **tables** for competitive data, source rankings, and content brief lists
- Use **headers** to structure all reports
- Write in plain business English - no SEO/AEO jargon without brief explanation
- Always ground claims in data: quote mention counts, citation numbers, percentages
- **Bold competitor names** when discussing gaps
- If brand has 0 mentions across all queries, be direct: "The brand has no AI visibility for the tracked topics - it does not appear in any AI-generated responses."
- When producing content briefs, be specific - not "write about X" but "write a comparison guide that directly answers [specific fan-out query]"

---

## Workflow: How to Start

When the user provides a markdown file:
1. Read the entire file first
2. Parse: count total queries; count those with > 0 mentions
3. Aggregate competitor mentions (de-duplicate)
4. Identify top cited domains from Sources tables
5. Ask the user: "Would you like an AEO Report, Competitive Gap Analysis, Content Briefs, or Citation Source Analysis?" - unless they've already specified

If the user points to specific competitor URLs without uploading a file first, skip straight to Task 4 (Citation Source Analysis).

If multiple files are uploaded (e.g. different time periods or different clients), compare them and note trends or differences.

---

## Reference Files

- `references/aeo-report-template.md` - Full AEO report template with section guidance
- `references/content-brief-template.md` - Detailed content brief format

Read these when producing formal deliverables for clients.
