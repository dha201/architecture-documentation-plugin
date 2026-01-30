---
name: human-writing-style
description: Use when generating any written content (docs, READMEs, outlines, reports, blog posts, changelogs) to strip out robotic AI patterns and produce writing that sounds like a real person wrote it. Triggers include requests like "make this sound human", "rewrite naturally", "less AI-sounding", or any content generation where quality prose matters.
---

# Human Writing Style

## Overview

This skill transforms AI-generated content into writing that passes the "would a human actually say this?" test. It provides a toolkit of techniques to kill corporate jargon, inject personality, and produce prose with natural rhythm.

Apply these techniques to any content generation task. They work for docs, presentations, blog posts, changelogs, technical writing — anything with words.

## When to Use This Skill

- Generating any written content (docs, outlines, reports)
- Rewriting existing content that sounds robotic
- User asks for "natural", "human", or "conversational" tone
- Content feels flat, generic, or templated after a first pass

## Banned Words

Never use these words. They scream "AI wrote this":

`delve`, `crucial`, `leverage`, `landscape`, `robust`, `game-changer`, `streamline`, `synergy`, `utilize`, `facilitate`, `encompass`, `holistic`, `paradigm`, `cutting-edge`, `harness`, `empower`, `spearhead`, `foster`, `bolster`, `elevate`

If you catch yourself reaching for any of these, stop. Find a plainer word. "Use" beats "utilize" every time.

## Techniques

### 1. The Coffee Shop Test

Write like you're explaining something to a friend over coffee. No marketing speak. No corporate jargon. Straight talk.

**Before:** "This module leverages a robust event-driven architecture to facilitate seamless data processing across distributed systems."

**After:** "This module listens for events and processes data across multiple servers. Nothing fancy — just pub/sub doing its job."

If it sounds like a LinkedIn post, rewrite it.

### 2. Short Sentences, Varied Rhythm

Max 15 words per sentence. Mix it up:

- Some super short (3-5 words)
- Some medium (8-12 words)
- Never three long sentences in a row

**Before:** "The authentication system provides comprehensive security measures that ensure all user credentials are properly validated before granting access to protected resources."

**After:** "Auth checks credentials before granting access. Every request. No exceptions. If the token's expired, you're getting a 401 — doesn't matter who you are."

### 3. Kill the Fluff

Remove every adjective and adverb that doesn't add new information. If "very", "really", or "extremely" appears, cut it or replace with a stronger verb.

**Before:** "This is a very important and extremely critical step in the deployment process."

**After:** "Skip this step and the deploy fails."

Show, don't tell. "The query runs in 3ms" beats "the query is extremely fast."

### 4. Specificity Over Vagueness

Replace every vague claim with concrete evidence. Numbers, examples, real scenarios.

**Before:** "Performance improved significantly after the optimization."

**After:** "Response time dropped from 850ms to 120ms. The P99 went from 2.3s to 400ms."

If you can't find real data, flag it: `[TODO: add actual metrics]`.

### 5. Unexpected Comparisons

Add one analogy or comparison per major section that makes people stop and think. Not the obvious ones.

**Before:** "The cache layer sits between the application and database."

**After:** "The cache is a bouncer at a nightclub. Most requests never make it to the database — the bouncer already knows the answer."

Make it weird but accurate.

### 6. Lead with What's Wrong

Don't start with the happy path. Start with what everyone gets wrong, then explain what's actually true.

**Before:** "Our logging system captures all relevant events for monitoring purposes."

**After:** "Most teams log everything and find nothing. We log three things: errors, latency spikes, and auth failures. That covers 90% of incidents."

### 7. Personality Without Arrogance

Show some edge. You can have opinions without being aggressive.

- State trade-offs honestly: "We picked Postgres over Mongo. The joins are worth the schema overhead."
- Acknowledge limitations: "This breaks if you throw more than 10K concurrent connections at it. We haven't needed to solve that yet."
- Be direct about unknowns: "No idea if this scales past 1M records. Haven't tested it."

### 8. Story Structure for Technical Content

When explaining decisions or architecture, frame it as a sequence of events:

1. Here's what we tried
2. Here's what went wrong
3. Here's what we did instead
4. Here's the result

People remember stories. They forget bullet points.

## Applying to Existing Content

When rewriting a draft:

1. Read the whole thing once
2. Highlight every sentence that sounds like a press release
3. For each highlighted sentence, ask: "How would I say this in Slack?"
4. Replace accordingly
5. Read it aloud — if you stumble, the sentence is too long
6. Check for three or more abstract nouns in a row ("implementation of the optimization of the process") and flatten them

## What This Skill Does NOT Do

- It doesn't make content informal or unprofessional
- It doesn't add slang or memes
- It doesn't sacrifice accuracy for personality
- It doesn't override domain-specific terminology that's genuinely needed

The goal is clear, direct writing with personality — not a Reddit post.
