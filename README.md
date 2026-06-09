# How Stanford Courses Handle AI - Spring 2026

An interactive dashboard analyzing how Stanford University course syllabi address student use of AI / generative-AI tools in Spring 2026.

**Live site:** enable GitHub Pages (Settings -> Pages -> Deploy from branch: main / root).

## Contents
- index.html - the self-contained interactive dashboard (Chart.js via CDN, all data embedded).
- data.json - the full coded dataset: every analyzed syllabus with its AI-policy classification and supporting quote.

## Method
Syllabi were collected from Stanford's central Syllabus tool plus instructor-published Google Docs. Each syllabus with readable text was scanned for AI references and classified into five patterns (Prohibited, Restricted/conditional, Allowed with disclosure, Encouraged, or mentions-AI-no-clear-rule) by language model, then spot-checked against the source wording.

## Headline
Of ~733 analyzed syllabi across ~110 departments, only ~42% mention student AI use. Among those that do, most ban or conditionally restrict it; few actively encourage it.

## Caveats
Classifications are automated and approximate, and reflect syllabus text only - not how instructors apply policies in practice. Not affiliated with or endorsed by Stanford University.
