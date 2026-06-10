# Methodology

How the "How Stanford Courses Handle AI" dataset and dashboard were built, covering the **2025–26 academic year** (Fall 2025, Winter 2026, Spring 2026).

## 1. Scope
All courses listed for each quarter across Stanford's 334 subject codes. The goal: characterize how each course's syllabus addresses **student use of AI / generative-AI tools**, and how that shifted over the year.

## 2. Collecting the syllabi
- Course lists and metadata come from Stanford's official Syllabus tool (`syllabus.stanford.edu`), queried per subject per term.
- Syllabus content was retrieved as inline text, as uploaded Canvas files (PDF/Word), or as instructor-shared Google Docs, then extracted to plain text.

## 3. What "analyzed" means
A syllabus enters the analysis only if it has **machine-readable text**. Image-only or unreadable syllabi are excluded. Readable counts per quarter:

| Quarter | Syllabi analyzed | Departments | Address AI |
|---|---|---|---|
| Fall 2025 | 956 | 138 | 361 |
| Winter 2026 | 1,084 | 133 | 376 |
| Spring 2026 | 1,313 | 151 | 457 |

(Fall and Winter had more image-only syllabi than Spring, so their absolute totals are lower. Compare the **percentages**, which are robust to coverage differences.)

## 4. Detecting and classifying AI policy
Each syllabus was scanned for any reference to AI (AI, generative AI, ChatGPT, Claude, Gemini, LLM, Copilot, chatbot, …). The relevant passage was classified by a large language model into five patterns, then spot-checked against the source wording (shown verbatim in the dashboard's evidence column):

| Tier | Meaning |
|---|---|
| **Prohibited** | AI use is banned for coursework. |
| **Restricted / conditional** | Allowed only with permission, or for some tasks (e.g. editing) but not others. |
| **Allowed with disclosure** | Permitted if the student cites/acknowledges it. |
| **Encouraged** | AI use is actively encouraged, expected, or required. |
| **Mentions AI, no clear rule** | AI is named but no actual usage rule is given (often a course *about* AI). |

## 5. Headline trend (share of AI-addressing syllabi)
| Tier | Fall 2025 | Winter 2026 | Spring 2026 |
|---|---|---|---|
| Prohibited | 26% | 24% | 31% |
| Restricted / conditional | 35% | 41% | 30% |
| Allowed with disclosure | 12% | 10% | 12% |
| Encouraged | 5% | 4% | 3% |
| Mentions AI, no rule | 21% | 22% | 24% |

The number of syllabi that engage AI at all grew over the year (361 → 376 → 457). Conditional/restricted policies peaked in Winter; outright prohibition rose by Spring; active encouragement stayed rare and declined each quarter.

## 6. Dataset (`data.json`)
`manifest` and `trend` give per-quarter totals; `documents[]` is one record per analyzed syllabus: `courseId`, `subject`, `num`, `title`, `instr`, `term`, `tier`, `rationale`, `quote`.

## 7. Limitations
Tiers reflect what a syllabus *says*, not classroom practice. Classification is automated and approximate. Image-only syllabi and a small share of unmatched files are excluded. Syllabus availability grows as a term approaches; each quarter is a snapshot. Not affiliated with or endorsed by Stanford University.
