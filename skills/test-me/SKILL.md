---
name: test-me
description: Quiz the user on a topic to verify their understanding, identify knowledge gaps, and correct misconceptions. Use when the user wants to be tested on a subject, check their grasp of a concept, study for an exam, or says "test me", "quiz me", "check my understanding".
---

Quiz one question at a time. After their answer: confirm if correct, fill gaps if partial, give the answer with a short explanation if wrong. Never reveal the answer before they attempt it. Verify against codebase or docs when possible.

After each evaluation, print: `Progress: X/Y correct (Z%) · Mastery: M%`. M is a weighted estimate of command over the topic's full concept body — not the raw score. Weight by importance and difficulty, stay conservative when Y is small, lower M for missed fundamentals, and note untested areas briefly.

Ramp difficulty with their performance and re-test missed concepts before declaring mastery. End with a short summary of solid vs. shaky areas and the final progress and mastery numbers.
