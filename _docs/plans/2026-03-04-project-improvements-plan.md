# Project Improvements Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Improve project.md across clarity, depth, balance, and engagement per the approved design.

**Architecture:** All changes target a single file (`project.md`). Tasks are ordered top-to-bottom through the document to minimize merge conflicts. Each task is one logical edit.

**Tech Stack:** Markdown (Jekyll GitHub Pages site)

---

### Task 1: Add Narrative Framing to Project Introduction

**Files:**
- Modify: `project.md:1-17`

**Step 1: Edit the introduction**

Replace the current subtitle and opening paragraph (lines 3-15) with narrative framing. Keep the title "# Blue Ridge Summer League". Add the commissioner scenario after the subtitle, before the student objectives list. Preserve the existing objectives list and Solver limit note.

New content after the title:

```markdown
## Formulation, Structural Analysis, and AI Evaluation in Optimization Modeling

You have been hired as the scheduling analyst for the Blue Ridge Summer League. The league commissioner needs a schedule that is fair, compact, and accounts for team rest. Your job is to build the optimization model, evaluate whether AI tools can replicate your work, and stress-test the model under new league rules.

This project integrates formulation, implementation, structural analysis, and critical evaluation of AI-assisted modeling within this unified scheduling problem.

Students will:

1. Formulate and solve a constrained integer programming model.
2. Extend the model to incorporate schedule quality considerations.
3. Evaluate AI-generated formulations of the same problem.
4. Introduce a structural modification that increases modeling complexity.
5. Analyze how structural changes affect feasibility, optimality, and model robustness.

The objective is not merely to construct a feasible schedule. Rather, the project is designed to examine how modeling decisions, constraint interaction, and objective selection influence optimization behavior. Later phases explicitly evaluate the reliability and limitations of AI-generated optimization models.

All models must be implemented in Microsoft Excel using Solver and must remain within the 200 decision variable limit of the standard Solver configuration.
```

**Step 2: Verify**

Read `project.md` lines 1-20 and confirm the narrative framing is present and the objectives list is intact.

**Step 3: Commit**

```bash
git add project.md
git commit -m "Add narrative framing to project introduction"
```

---

### Task 2: Add Worked Mini-Example After Problem Setting

**Files:**
- Modify: `project.md` (insert after the "Problem setting" section, before the "Timeline" section — after line 50, before line 52 `---`)

**Step 1: Insert mini-example section**

Add the following new section between the end of "Problem setting" and the `---` before "Timeline":

```markdown

## Worked mini-example

To verify your understanding of the variable structure, consider a simplified version of the problem.

**Setup:** 2 teams (A, B), 3 days, at most 1 game per day, the pair must play at least 1 and at most 2 games.

The single decision variable for each day is:

| | Day 1 | Day 2 | Day 3 |
|---|---|---|---|
| A vs B | $x_1$ | $x_2$ | $x_3$ |

where $x_d \in \{0, 1\}$ indicates whether the pair plays on day $d$.

**Valid schedule:** $x_1 = 1, x_2 = 0, x_3 = 1$ — the pair plays on Days 1 and 3 (2 games, satisfies all constraints, no consecutive-day play).

**Infeasible schedule:** $x_1 = 1, x_2 = 1, x_3 = 1$ — 3 games violates the upper bound of 2 games for this pair.

In the full problem, you will have 6 pairs and 10 days. The variable structure scales accordingly.
```

**Step 2: Verify**

Read the inserted section and confirm it is placed correctly between "Problem setting" and "Timeline."

**Step 3: Commit**

```bash
git add project.md
git commit -m "Add worked mini-example after problem setting"
```

---

### Task 3: Update Timeline With Week 11 Buffer and Phase 4 Checkpoint

**Files:**
- Modify: `project.md` — the Timeline section (currently around lines 54-64)

**Step 1: Update the timeline table and comment**

Replace the current timeline table and HTML comment with:

```markdown
| Week | Phase | Deliverable |
|------|-------|-------------|
| Week 9 | Phase 1 | Baseline formulation |
| Week 10 | Phase 2 | Rest optimization |
| Week 11 | Feedback and review | Instructor feedback on Phases 1–2; prepare for AI evaluation phases |
| Week 12 | Phase 3 | AI replication and evaluation; Phase 4 modification proposal due |
| Week 13 | Phase 4a | Structural modification: formulate and solve extended model |
| Week 14 | Phase 4b | AI stress test and comparative analysis |
| Week 15 | Final reflection | Synthesis |
```

Remove the HTML comment about in-class sessions (it's now redundant since Week 11 is explicit).

**Step 2: Verify**

Read the timeline section and confirm weeks 11, 13, and 14 are correctly split.

**Step 3: Commit**

```bash
git add project.md
git commit -m "Update timeline with Week 11 buffer and Phase 4 checkpoint"
```

---

### Task 4: Revise Phase 1 — Points, LP Relaxation, Checkpoint, Mini-Reflection

**Files:**
- Modify: `project.md` — Phase 1 section (currently around lines 68-103)

**Step 1: Update heading and points**

Change heading from `# Phase 1: Baseline formulation (30 points)` to `# Phase 1: Baseline formulation (25 points)`.

**Step 2: Add LP relaxation requirement**

After the existing implementation guidance bullet list, add:

```markdown
- After obtaining the integer solution, solve the LP relaxation (change Solver to allow continuous variables) and compare the relaxation bound to the integer optimal value. Report the integrality gap.
```

**Step 3: Add checkpoint callout**

After the implementation guidance section and before "Submission requirements," insert:

```markdown
> 🔍 **Checkpoint — verify before running Solver:**
> - How many binary decision variables does your model have?
> - What is the theoretical maximum number of games? The minimum?
> - Does your constraint count match the number of structural requirements listed above?
```

**Step 4: Add LP relaxation to submission requirements**

In the written explanation bullet list, add:
```markdown
  - LP relaxation bound and integrality gap interpretation.
```

**Step 5: Add mini-reflection to submission requirements**

After the written explanation bullets, add:

```markdown
- Brief reflection (2–3 sentences): What surprised you about the relationship between constraints and the feasible region?
```

**Step 6: Update rubric**

Replace the rubric with:

```markdown
### Phase 1 rubric (25 points)

Formulation correctness – 12
Solver implementation and configuration – 8
Clarity and technical precision – 5
```

**Step 7: Verify**

Read the full Phase 1 section and confirm points total 25, LP relaxation is required, checkpoint box is present, and mini-reflection is included.

**Step 8: Commit**

```bash
git add project.md
git commit -m "Revise Phase 1: rebalance to 25pts, add LP relaxation, checkpoint, reflection"
```

---

### Task 5: Revise Phase 2 — Points, Feasibility Proof, Checkpoint, Mini-Reflection

**Files:**
- Modify: `project.md` — Phase 2 section (currently around lines 106-147)

**Step 1: Update heading and points**

Change heading from `# Phase 2: Schedule quality and constraint interaction (40 points)` to `# Phase 2: Schedule quality and constraint interaction (45 points)`.

**Step 2: Strengthen feasibility requirement**

Replace the bullet "Analyze whether zero rest violations are feasible under the pairwise and capacity constraints." with:

```markdown
- Prove or disprove: zero rest violations are achievable under the pairwise and capacity constraints. Provide a structured argument that references specific constraint interactions (e.g., capacity limits on August 3 and 7, pairwise lower bounds, daily game limits).
```

**Step 3: Add checkpoint callout**

After "Superficial rest-counting approaches..." paragraph and before "Submission requirements," insert:

```markdown
> 🔍 **Checkpoint — verify before running Solver:**
> - Is zero rest violations feasible? Write your argument before solving.
> - How many new variables did you introduce? Are they correctly linked to the game variables?
> - Did you preserve all Phase 1 constraints without modification?
```

**Step 4: Add mini-reflection to submission requirements**

After the written explanation bullets, add:

```markdown
- Brief reflection (2–3 sentences): Which constraint interaction was hardest to model correctly? Why?
```

**Step 5: Update rubric**

Replace the rubric with:

```markdown
### Phase 2 rubric (45 points)

Correct modeling of rest violations – 18
Preservation of prior constraints – 10
Depth of structural analysis – 12
Clarity and organization – 5
```

**Step 6: Verify**

Read the full Phase 2 section and confirm points total 45.

**Step 7: Commit**

```bash
git add project.md
git commit -m "Revise Phase 2: rebalance to 45pts, require feasibility proof, add checkpoint"
```

---

### Task 6: Revise Phase 3 — Prompt Guidance, Comparison Table, Rubric, Mini-Reflection

**Files:**
- Modify: `project.md` — Phase 3 section (currently around lines 150-182)

**Step 1: Add prompt quality guidance**

After "Students will prompt a publicly available AI system to formulate the Phase 2 model." add:

```markdown
Your prompt must include the complete problem description, all constraints, and the objective function. A vague prompt (e.g., "make a sports schedule in Excel") will not yield a meaningful comparison and will receive reduced credit for the analytical portion.
```

**Step 2: Add checkpoint callout**

After "Do not modify the AI model prior to diagnostic analysis." insert:

```markdown
> 🔍 **Checkpoint — before beginning your analysis:**
> - Does your prompt include the full problem description and all constraints?
> - Did you implement the AI's formulation exactly as generated, without corrections?
> - Did you attempt to solve it in Solver before analyzing?
```

**Step 3: Add structured comparison table**

In the "Analytical requirements" section, after the existing bullet list, add:

```markdown
Use the following comparison framework to structure your analysis:

| Dimension | Your Model (Phase 2) | AI-Generated Model | Assessment |
|-----------|---------------------|-------------------|------------|
| Decision variable definitions | | | |
| Number of decision variables | | | |
| Constraint count | | | |
| Constraint correctness (list errors) | | | |
| Objective function | | | |
| Solver feasibility | | | |
| 200-variable limit compliance | | | |
```

**Step 4: Add mini-reflection to submission requirements**

Add after the analytical requirements:

```markdown
- Brief reflection (2–3 sentences): What did the AI get right that you expected it to get wrong, or vice versa?
```

**Step 5: Update rubric**

Replace the rubric with:

```markdown
### Phase 3 rubric (50 points)

Accurate implementation of AI formulation – 5
Identification of structural deficiencies – 25
Comparative reasoning between human and AI models – 15
Clarity, specificity, and supporting evidence – 5
```

**Step 6: Verify**

Read the full Phase 3 section and confirm the comparison table, prompt guidance, and rubric adjustments are present. Points still total 50.

**Step 7: Commit**

```bash
git add project.md
git commit -m "Revise Phase 3: add prompt guidance, comparison table, rebalance rubric"
```

---

### Task 7: Revise Phase 4 — Student Agency, Marginal Impact, Checkpoint, Mini-Reflection

**Files:**
- Modify: `project.md` — Phase 4 section (currently around lines 186-225)

**Step 1: Reframe structural modification examples**

Replace the "Acceptable examples" section with:

```markdown
## Structural modification

Propose and justify your own structural modification. The following are examples of modifications that qualify, but you are encouraged to design one that reflects a realistic scheduling concern:

- Rolling window constraint (e.g., no 3 games within any 4 consecutive days).
- Min–max fairness objective.
- Weighted multi-objective formulation.
- Asymmetric team availability constraints.
- Equity constraints on total idle days.

Merely changing numerical parameter values does not qualify as a structural modification.

**Proposal requirement:** Submit a 1-paragraph proposal describing your chosen modification by the end of Week 12. The instructor will confirm that it qualifies before you proceed with implementation.
```

**Step 2: Add marginal impact analysis to analytical requirements**

Add to the "Students must explain:" bullet list:

```markdown
- Quantitative marginal impact: How does the objective value change? Does the feasible region shrink, and by how much?
```

**Step 3: Add checkpoint callout**

Before "Analytical requirements," insert:

```markdown
> 🔍 **Checkpoint — before your comparative analysis:**
> - Has your modification proposal been approved by the instructor?
> - How does your modification change the feasible region compared to Phase 2?
> - Can you quantify the change in objective value?
```

**Step 4: Add mini-reflection**

After the analytical requirements, add:

```markdown
- Brief reflection (2–3 sentences): How did your structural modification change the difficulty of the problem?
```

**Step 5: Verify**

Read the full Phase 4 section. Points remain at 60.

**Step 6: Commit**

```bash
git add project.md
git commit -m "Revise Phase 4: add student agency, marginal impact, checkpoint"
```

---

### Task 8: Revise Final Reflection — Synthesis Framing

**Files:**
- Modify: `project.md` — Final reflection section (currently around lines 228-244)

**Step 1: Update the reflection framing**

Replace the current content with:

```markdown
# Final reflection (20 points)

Maximum length: 1 page.

This reflection should synthesize your per-phase observations into broader insights. Revisit your brief reflections from Phases 1–4 and address:

1. Under what conditions does an optimization model become structurally fragile?
2. Which types of constraints most significantly increase modeling complexity?
3. In what contexts is AI assistance appropriate in optimization modeling, and where is independent formulation preferable?
4. What did you learn about the relationship between formulation detail and Solver behavior?

Your responses must reference specific experiences from the project. General statements without connection to your modeling work will receive reduced credit.

### Final reflection rubric (20 points)

Conceptual insight – 10
Integration of per-phase observations – 5
Clarity and coherence – 5
```

**Step 2: Verify**

Read the section. Points total 20.

**Step 3: Commit**

```bash
git add project.md
git commit -m "Revise final reflection: synthesis framing with per-phase integration"
```

---

### Task 9: Update Grading Summary Table

**Files:**
- Modify: `project.md` — Grading summary section (currently around lines 248-257)

**Step 1: Update the table**

Replace with:

```markdown
# Grading summary

| Component | Points |
|-----------|--------|
| Phase 1 | 25 |
| Phase 2 | 45 |
| Phase 3 | 50 |
| Phase 4 | 60 |
| Final reflection | 20 |
| **Total** | **200** |
```

**Step 2: Verify**

Confirm points sum to 200.

**Step 3: Commit**

```bash
git add project.md
git commit -m "Update grading summary to reflect rebalanced points"
```

---

### Task 10: Final Review

**Step 1: Read entire project.md**

Read the complete file top to bottom. Verify:
- All 4 checkpoint callout boxes are present (one per phase)
- All 4 mini-reflections are present (one per phase)
- Point totals: 25 + 45 + 50 + 60 + 20 = 200
- Narrative framing is in the introduction
- Mini-example is between Problem Setting and Timeline
- Timeline shows Week 11 buffer, Phase 4 split into 13/14
- Phase 3 has comparison table and prompt guidance
- Phase 4 has proposal requirement and marginal impact
- Final reflection references per-phase observations
- No broken markdown formatting

**Step 2: Commit if any fixes needed**

```bash
git add project.md
git commit -m "Fix formatting issues in project.md"
```
