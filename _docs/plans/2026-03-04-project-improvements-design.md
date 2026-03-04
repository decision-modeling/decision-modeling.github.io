# Project Improvements Design

**Date:** 2026-03-04
**Scope:** Comprehensive improvements to project.md across clarity, depth, balance, and engagement

---

## Context

The Blue Ridge Summer League project is a multi-phase optimization assignment for BIT 2406 at Virginia Tech. Students formulate, extend, and critically evaluate integer programming models in Excel Solver. The project is well-structured but needs improvements across four dimensions: student clarity, pedagogical depth, scope/balance, and engagement.

## Approach

Targeted refinements within the existing structure (Approach A), incorporating structured comparison and integrated narrative elements from Approach B.

---

## 1. Clarity & Scaffolding

### 1.1 Worked Mini-Example
Add a concrete mini-example after the "Problem setting" section, before Phase 1:
- 2 teams, 3 days, simplified constraints
- Show the decision variable matrix, one valid schedule, one infeasible schedule
- Purpose: students verify they understand the variable structure before scaling up

### 1.2 Checkpoint Questions
Add checkpoint questions in visually distinct callout boxes (blockquote + emoji) at the end of each phase's guidance section:
- Phase 1: "How many decision variables? What are the theoretical min/max games?"
- Phase 2: "Is zero rest violations feasible? Why or why not?"
- Phase 3: "Does your AI prompt include the full problem? A vague prompt yields a meaningless comparison."
- Phase 4: "How does your modification change the feasible region?"

### 1.3 AI Prompt Guidance
Expand Phase 3 instructions to set expectations for prompt quality. A prompt like "make a sports schedule" is insufficient. Students must include the full problem description and constraints.

---

## 2. Pedagogical Depth

### 2.1 LP Relaxation (Phase 1)
Require students to solve the LP relaxation (without integrality) and compare the bound to the integer solution. Introduces the integrality gap concept concretely.

### 2.2 Feasibility Proof (Phase 2)
Make the feasibility analysis of zero rest violations explicit and required. Students must provide a structured argument referencing specific constraint interactions (capacity limits on Aug 3/7, pairwise lower bounds, daily limits).

### 2.3 Structured Comparison Table (Phase 3)
Replace vague "critique the AI model" with a side-by-side comparison table. Dimensions:
- Variable definitions
- Constraint count and correctness
- Objective function formulation
- Solver feasibility
- Compliance with 200-variable limit

### 2.4 Marginal Impact Analysis (Phase 4)
Require quantitative analysis: How does the objective value change with the structural modification? Does the feasible region shrink? By how much? Pushes beyond "I added a constraint" toward structural reasoning.

---

## 3. Scope & Balance

### 3.1 Point Rebalancing

| Component | Current | Proposed | Rationale |
|-----------|---------|----------|-----------|
| Phase 1 | 30 | 25 | Setup exercise, less complex |
| Phase 2 | 40 | 45 | Core modeling work, significantly harder |
| Phase 3 | 50 | 50 | Shift 5pts from implementation to analysis |
| Phase 4 | 60 | 60 | Unchanged |
| Reflection | 20 | 20 | Unchanged |
| **Total** | **200** | **200** | |

Phase 3 internal rebalancing:
- AI implementation: 10 -> 5 pts (mechanical task)
- Structural deficiency identification: 20 -> 25 pts
- Comparative reasoning: 15 pts (unchanged)
- Clarity/evidence: 5 pts (unchanged)

### 3.2 Phase 4 Intermediate Checkpoint
Week 13: formulate and solve the extended model. Week 14: AI stress test and comparative analysis.

### 3.3 Week 11 Buffer
Make explicit that Week 11 is a feedback/buffer week for Phases 1-2 before starting AI evaluation phases.

---

## 4. Engagement

### 4.1 Narrative Framing
Open with a scenario: "You have been hired as the scheduling analyst for the Blue Ridge Summer League. The league commissioner needs a schedule that is fair, compact, and accounts for team rest."

### 4.2 Student Agency in Phase 4
Reframe the structural modification examples as inspiration, not a menu. Students propose their own modification and submit a 1-paragraph proposal by end of Week 12 for instructor approval.

### 4.3 Per-Phase Mini-Reflections
Add 2-3 sentence reflection prompts at the end of each phase:
- Phase 1: "What surprised you about constraints and the feasible region?"
- Phase 2: "Which constraint interaction was hardest to model? Why?"
- Phase 3: "What did the AI get right that you expected wrong, or vice versa?"
- Phase 4: "How did your modification change problem difficulty?"

Final reflection becomes a synthesis of these, plus the original big-picture questions.

---

## Implementation Notes

- All changes are to `project.md`
- Callout boxes use markdown blockquote syntax with emoji markers
- Mini-example should be self-contained and verifiable by hand
- Side-by-side comparison table should be a template students can copy
- Point totals must remain at 200
