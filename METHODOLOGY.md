# Methodology

How the "How Stanford Courses Handle AI — Spring 2026" dataset and dashboard were built.

## 1. Scope
All courses listed for Stanford's **Spring 2026** term, across **334 subject codes**. The goal was to characterize how each course's syllabus addresses **student use of AI / generative-AI tools**.

## 2. Collecting the syllabi
- **Course list & metadata** came from Stanford's official Syllabus tool (`syllabus.stanford.edu`), which exposes a per-subject course search. Iterating over all 334 subjects yielded **4,019 unique courses** (after removing cross-listed duplicates).
- **1,092** of those courses had a syllabus available to authenticated Stanford users.
- For each, the syllabus content was retrieved either as the inline text rendered by the Syllabus tool, as an uploaded file (PDF / Word) hosted on Canvas, or — where instructors published one — as a shared **Google Doc**.
- Text was extracted from PDFs and Word documents and normalized to plain text.

## 3. What "analyzed" means
A syllabus enters the analysis only if it has **machine-readable text**. Syllabi that are image-only, behind restricted links, or otherwise unreadable are excluded. This left **733 analyzed syllabi across ~110 departments**.

## 4. Detecting and classifying AI policy
1. Each syllabus was scanned for any reference to AI (e.g., *AI, generative AI, ChatGPT, Claude, Gemini, LLM, Copilot, chatbot*). **310** syllabi contain such language.
2. For each of those, the relevant passage(s) were extracted and classified by a large language model into one of five patterns:

| Tier | Meaning |
|---|---|
| **Prohibited** | AI use is banned for coursework. |
| **Restricted / conditional** | Allowed only with permission, or for some tasks (e.g. editing) but not others. |
| **Allowed with disclosure** | Permitted if the student cites/acknowledges it. |
| **Encouraged** | AI use is actively encouraged, expected, or required. |
| **Mentions AI, no clear rule** | AI is named but no actual usage rule is given. |

3. Classifications were spot-checked against the source wording, which is shown verbatim in the dashboard's evidence column so any reader can audit a call.

## 5. Headline numbers
Of the 310 AI-addressing syllabi: **Prohibited 28%**, **Restricted/conditional 32%**, **Allowed with disclosure 14%**, **Encouraged 4%**, **Mentions AI without a clear rule 23%**.

## 6. Dataset (`data.json`)
- `manifest` — totals (courses offered, syllabi available, syllabi analyzed).
- `tier_counts` — count per tier.
- `documents[]` — one record per analyzed syllabus: `courseId`, `subject`, `num`, `title`, `instr`, `tier`, `rationale`, `quote`, `source`.

## 7. Limitations
- Tiers reflect **what the syllabus says**, not how an instructor applies a policy in practice.
- Classification is **automated and approximate**; edge cases exist.
- ~19% of uploaded files could not be auto-matched to a course code; they are still counted in totals but may show a generic label.
- Some departments (e.g., MS&E) don't post to the central Syllabus tool, so their coverage depends on directly shared documents.
- This is a descriptive snapshot for general understanding, **not** an official Stanford position. Not affiliated with or endorsed by Stanford University.
