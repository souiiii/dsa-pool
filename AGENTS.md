# AGENTS.md

## Purpose

This repository has one narrow purpose:

Build a high-quality shuffled DSA practice pool for interview preparation.

The user's main goal is **pattern identification**.

A practice question must not reveal its expected technique before the user attempts it.

Do not turn this into a larger planner, recommendation engine, dashboard, or DSA curriculum.

---

## Repository Structure

```text
dsa-question-pool/
├── AGENTS.md
├── Sources/
│   └── DSA_Pattern_Index.md
├── Output/
│   ├── practice_questions.md
│   └── answer_key.md
└── State/
    └── question_pool.json
```

Do not add files or folders unless they are genuinely necessary.

---

## Source of Truth

Before selecting questions, read and analyze:

`Sources/DSA_Pattern_Index.md`

This file defines the problem triggers and DSA patterns that the practice pool should exercise.

Do not merely extract section headings.

Understand the actual trigger → technique relationships described in the file.

The pool should provide meaningful coverage of those patterns without exposing them to the user in advance.

---

## Primary Objective

Create a pool where the user can repeatedly perform:

```text
read problem
→ infer constraints
→ identify likely pattern
→ derive approach
→ solve
→ check answer key afterward
```

The question list itself must not make the pattern obvious through grouping, headings, ordering, filenames, hints, or metadata.

---

## Question Selection

Prefer:

- mostly Medium problems
- a smaller number of Hard problems
- only a limited number of Easy problems when they are unusually useful for pattern recognition
- problems with clear but non-trivial structural signals
- problems that reward recognizing the correct technique
- questions covering the major triggers in `DSA_Pattern_Index.md`
- less obvious and less overused interview problems
- questions available on an actual coding platform

Do not flood the list with Easy questions.

A reasonable default difficulty distribution is approximately:

```text
Medium: 75–85%
Hard:   10–20%
Easy:    0–10%
```

This is guidance, not a reason to force exact percentages.

Quality is more important than hitting a mathematical quota.

---

## Avoid Common Already-Solved Problems

Assume the user has already solved around 300 LeetCode-style problems.

Therefore aggressively avoid extremely common DSA staples unless there is a strong reason to include them.

Examples of questions that are usually too obvious/common include things like:

- Two Sum
- Valid Parentheses
- Maximum Subarray
- Binary Search
- Merge Two Sorted Lists
- Reverse Linked List
- Number of Islands
- Climbing Stairs
- House Robber
- Coin Change
- Longest Increasing Subsequence
- Course Schedule
- Kth Largest Element
- Merge Intervals
- Product of Array Except Self

This list is illustrative, not exhaustive.

Do not simply exclude these names and then fill the pool with equally common Top-100 interview questions.

Prefer problems that are still interview-relevant but are less likely to have already been memorized.

---

## Coding Platform Requirement

Every practice question must have a usable link to a coding platform where the user can actually solve and submit it.

Preferred platforms include:

1. LeetCode 
2. HackerRank
3. GeeksforGeeks
4. CodeChef
5. AtCoder
6. InterviewBit
7. other reputable coding platforms with an actual problem-solving interface (except codeforces)

   The interface should have proper boiler plate and support thats why i excluded codeforces.

If using a company-tagged or company-reported problem, it must still have a corresponding coding-platform problem link.

Do not include:

- blog-only questions
- screenshots
- vague interview recollections without a solvable version
- inconsistent questions
- inaccessible private company portals
- descriptions without a reliable problem URL

Verify that links correspond to the intended problem.

---

## Company Questions

Company-associated problems are useful, but company tags are secondary to problem quality.

If company information is available and reasonably trustworthy, store it in the internal state and answer key.

Do not place company names prominently in the practice list if they could bias the user's expectations about the problem.

Do not invent company associations.

---

## Pattern Coverage

Use `Sources/DSA_Pattern_Index.md` to determine coverage.

Coverage should include the important patterns represented there, but question counts do not need to be equal across every pattern.

Favor patterns that:

- appear frequently in interviews
- are easy to confuse with another technique
- require recognizing a structural trigger
- represent known weak points or high-value interview skills

Include some questions where multiple approaches initially appear plausible.

Those are valuable because the user's goal is pattern recognition, not mechanical template matching.

---

## No Pattern Leakage

`Output/practice_questions.md` must NOT expose:

- pattern names
- technique names
- categories such as "Sliding Window"
- grouped sections by data structure
- hints revealing the approach
- answer-key information
- trigger descriptions
- filenames containing the technique
- ordering that makes categories obvious

Bad:

```text
## Sliding Window Questions
1. ...
2. ...
```

Bad:

```text
17. Minimum Window Substring — use variable sliding window
```

Good:

```text
17. Problem Title — Medium
https://leetcode.com/...
```

The user should encounter each question with as little algorithmic priming as possible.

---

## Real Shuffling Requirement

The final practice order must be genuinely randomized.

Do not simulate randomness by:

- manually alternating categories
- rotating patterns
- sorting by difficulty
- sorting alphabetically
- preserving research/discovery order
- taking one question from each category repeatedly
- arranging questions to "feel random"

First finalize the complete accepted candidate pool.

Only after selection, validation, deduplication, and coverage checks are complete should the final practice order be shuffled.

Use an actual randomization mechanism available in the environment.

Examples include:

```python
random.SystemRandom().shuffle(...)
```

or another genuine random shuffle.

Do not use a fixed seed unless reproducibility is explicitly requested.

Store the resulting final order in `State/question_pool.json`.

`practice_questions.md` and `answer_key.md` must use the same randomized question IDs/order.

Do not reshuffle every time an output file is regenerated unless explicitly asked.

---

## Prevent Hidden Ordering Bias

Before shuffling, the internal candidate pool may contain pattern labels.

After the final shuffle, verify that the resulting sequence is not accidentally still structured by:

- pattern
- difficulty
- platform
- company
- source discovery order

Do not "improve" the random ordering afterward merely because several similar questions happen to appear near one another.

A real shuffle is allowed to produce clusters.

The objective is randomness, not visually perfect alternation.

---

## Deduplication

Avoid:

- exact duplicate questions
- the same problem mirrored across multiple platforms
- obvious renamed clones
- near-identical variants testing effectively the same scenario
- several questions whose solution and reasoning are almost identical

Some repeated use of the same broad DSA pattern is expected and desirable.

Duplicate pattern != duplicate problem.

---

## State File

`State/question_pool.json` is the machine-readable source of truth.

Each question should contain enough internal metadata for validation.

Recommended shape:

```json
{
  "id": 1,
  "title": "Problem title",
  "url": "https://...",
  "platform": "LeetCode",
  "difficulty": "Medium",
  "primary_pattern": "internal only",
  "secondary_patterns": [],
  "trigger": "internal explanation",
  "company_tags": [],
  "selection_reason": "why this problem belongs in the pool",
  "commonness": "low|medium|high",
  "final_order": 1
}
```

Fields may be adjusted if needed.

Do not expose internal pattern fields in `practice_questions.md`.

---

## practice_questions.md

This is the file the user actually practices from.

Keep it minimal.

Recommended format:

```markdown
# DSA Practice Pool

1. Problem Title — Medium  
   https://...

2. Problem Title — Hard  
   https://...

3. Problem Title — Medium  
   https://...
```

Do not add explanations under questions.

Do not add pattern labels.

Do not add hints.

Do not add solution summaries.

Do not separate questions into categories.

---

## answer_key.md

This file is checked only after an attempt.

For each question include:

```markdown
## 17. Problem Title

Primary pattern: Prefix Sum + Hash Map

Trigger:
The problem asks for contiguous subarray counts while negative values prevent a monotonic sliding window.

Why:
Store previously seen prefix sums and check whether currentPrefix - target has appeared.

Possible alternatives:
...
```

Keep explanations concise.

The purpose is to validate the user's recognition, not provide a full editorial.

---

## Research Behavior

Research broadly enough to create a strong pool, but do not recursively over-research.

Do not spend excessive effort trying to prove that a problem has never appeared in an interview or that the user has definitely never solved it.

Use practical signals of commonness.

Avoid obvious canonical questions and heavily repeated "Top Interview" staples.

Once a candidate is clearly suitable and its link is verified, move on.

Reuse already gathered information instead of repeatedly searching for the same fact.

---

## Selection Workflow

Follow this order:

```text
1. Read AGENTS.md
2. Read Sources/DSA_Pattern_Index.md completely
3. Extract the important trigger → pattern relationships internally
4. Determine reasonable coverage targets
5. Research candidate problems
6. Reject overly common / trivial / duplicate problems
7. Verify coding-platform links
8. Build the complete candidate pool
9. Validate difficulty balance
10. Validate pattern coverage
11. Validate duplicates and near-duplicates
12. Freeze the accepted pool
13. Perform a genuine random shuffle
14. Save final order to State/question_pool.json
15. Generate Output/practice_questions.md
16. Generate Output/answer_key.md using the exact same order
17. Perform one final consistency check
18. Stop
```

Do not repeatedly reconsider the entire pool after step 12 unless a validation failure is discovered.

---

## Quality Checks Before Completion

Before declaring completion, verify:

- every question has a working coding-platform URL
- the majority are Medium
- only a small portion are Hard
- Easy problems do not dominate
- extremely common LeetCode staples have been avoided
- major patterns from the source index receive reasonable coverage
- questions are not grouped by pattern
- practice output leaks no solution technique
- duplicate and near-duplicate problems have been removed
- company questions are solvable on a coding platform
- the final order was produced by a real shuffle
- practice list and answer key have identical IDs and ordering
- internal JSON contains the necessary pattern metadata
- no unnecessary repository complexity was introduced

---

## Scope Discipline

Do not:

- redesign the broader placement planner
- modify unrelated repository files
- create a web app
- create a database
- build recommendation infrastructure
- implement spaced repetition
- build analytics
- create a large automation system
- generate full solutions for every question
- reorganize the pattern index
- change the user's existing DSA methodology

This project exists only to produce a strong, shuffled, pattern-blind DSA practice pool.

Make the smallest implementation that achieves that well.
