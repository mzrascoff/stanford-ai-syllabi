# Methodology

How the "How Stanford Courses Handle AI — Spring 2026" dataset and dashboard were built.

## 1. Scope
All courses listed for Stanford's **Spring 2026** term, across **334 subject codes**. The goal was to characterize how each course's syllabus addresses **student use of AI / generative-AI tools**.

## 2. Collecting the syllabi
- **Course list & metadata** came from Stanford's official Syllabus tool (`syllabus.stanford.edu`), which exposes a per-subject course search. Iterating over all 334 subjects yielded **4,019 unique courses** (after removing cross-listed duplicates).
- **~1,394** of those courses had a syllabus available to authenticated Stanford users. (This number grows over time as instructors post syllabi closer to the term; the dataset has been re-swept to capture late uploads.)
- For each, the syllabus content was retrieved either as the inline text rendered by the Syllabus tool, as an uploaded file (PDF / Word) hosted on Canvas, or — where instructors published one — as a shared **Google Doc**.
- Text was extracted from PDFs and Word documents and normalized to plain text.

## 3. What "analyzed" means
A syllabus enters the analysis only if it has **machine-readable text**. Syllabi that are image-only, behind restricted links, or otherwise unreadable are excluded. This left **1,313 analyzed syllabi across 151 departments**.

## 4. Detecting and classifying AI policy
1. Each syllabus was scanned for any reference to AI (e.g., *AI, generative AI, ChatGPT, Claude, Gemini, LLM, Copilot, chatbot*). **457** syllabi contain such language.
2. For each of those, the relevant passage(s) were extracted and classified by a large language model into one of five patterns:

| Tier | Meaning |
|---|---|
| **Prohibited** | AI use is banned for coursework. |
| **Restricted / conditional** | Allowed only with permission, or for some tasks (e.g. editing) but not others. |
| **Allowed with disclosure** | Permitted if the student cites/acknowledges it. |
| **Encouraged** | AI use is actively encouraged, expected, or required. |
| **Mentions AI, no clear rule** | AI is named but no actual usage rule is given (often a course that is *about* AI). |

3. Classifications were spot-checked against the source wording, which is shown verbatim in the dashboard's evidence column so any reader can audit a call.

## 5. Headline numbers
Of the 457 AI-addressing syllabi: **Prohibited 31%**, **Restricted/conditional 30%**, **Allowed with disclosure 12%**, **Encouraged 3%**, **Mentions AI without a clear rule 24%**. Only ~35% of all analyzed syllabi mention student AI use at all.

## 6. Dataset (`data.json`)
- `manifest` — totals (courses offered, syllabi available, syllabi analyzed).
- `tier_counts` — count per tier.
- `documents[]` — one record per analyzed syllabus: `courseId`, `subject`, `num`, `title`, `instr`, `tier`, `rationale`, `quote`, `source`.

## 7. Limitations
- Tiers reflect **what the syllabus says**, not how an instructor applies a policy in practice.
- Classification is **automated and approximate**; edge cases exist.
- Some uploaded files could not be auto-matched to a course code or read; affected courses may show a generic label or count as "no AI policy" when the policy is simply unreadable.
- Syllabus availability is a moving target during the weeks before a term; this is a snapshot re-swept on the generation date.
- This is a descriptive snapshot for general understanding, **not** an official Stanford position. Not affiliated with or endorsed by Stanford University.
