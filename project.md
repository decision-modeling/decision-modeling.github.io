# Blue Ridge Summer League Scheduling Project

You are the scheduler for a 10-day summer basketball league running **Aug 1–10 (inclusive)**. The league is called the **Blue Ridge Summer League**. The teams are:

- Virginia Tech
- Radford
- James Madison
- VMI

One constraint up front: we are not modeling facilities or time slots. This is a day-by-day schedule. This simplification is on purpose: it keeps the focus on clean formulations, correct logic, and your ability to explain what Solver did.

This project has **three stages**. Each stage is its own Canvas Assignment submission. Build on your previous model each time.

---

## What You Are Scheduling

- 10 days: Aug 1–10
- A game is always between **two different teams**
- A team can play **at most one game per day**
- Each day has a **league-wide capacity** (how many games can be hosted that day)

### Daily League Capacity

Use these limits for Tasks 1–3:

- Aug 3 and Aug 7: **at most 1 game**
- All other days: **at most 2 games**

If you are thinking "why those two days?" Good. That is the point. Real schedules have weird constraints that are not elegant.

---

## Tools and Limits That Matter

- Use **Excel + Solver**
- Your model must run on the standard Solver configuration. That means staying under the **200 decision variable** limit. Treat this as a real design constraint: it rewards smart formulations and punishes overly granular ones.

---

## How Canvas Submissions Work

Each task has its own Canvas Assignment. For every task, you submit:

1. An Excel file (.xlsx) that actually solves the task
2. A short write-up (Canvas text entry)

The write-up is how you show you understand your own model.

---

## Task 1: Schedule As Many Games As Possible

### Goal
Maximize the total number of games scheduled across the 10 days.

For Task 1, focus on feasibility and structure.

### Required Constraints
Your model must enforce:

- Daily capacity is not exceeded (1 game on Aug 3 and Aug 7; 2 games otherwise)
- Each team plays at most one game per day
- No team plays itself

Matchups can repeat as much as Solver wants. That repetition is going to look silly, and that is fine. Task 1 is about structure.

### What You Submit on Canvas
**1) Excel (.xlsx)**  
Your spreadsheet should make it obvious where:
- decision variables live (BLUE)
- the objective cell is (ORANGE)
- the constraint left-hand sides are computed (YELLOW)

**2) Short write-up (about half a page)**  
Answer these:

- What are your decision variables?
- What is the objective, in plain English?
- What constraints did you include, and why?
- How many games did your optimal schedule produce?

---

## Task 2: Add Matchup Rules, Keep the Same Objective

Task 2 keeps the same objective, but now you have matchup rules to follow.

### Goal
Maximize the total number of games scheduled.

### New Matchup Constraints
For every pair of teams, over the full 10 days:

- They must play **at least 2** games
- They may play **at most 3** games

All Task 1 constraints still apply.

A quick reality check you should do before you even open Solver:
- There are 6 unique pairs in a 4-team league.
- The "at least 2" rule implies at least 12 games total.
- The "at most 3" rule implies at most 18 games total.
- Daily capacity implies at most 18 or 19 games depending on the pattern, but the pairwise cap is often the real limiter.

If you did not do that math, do it now. It will save you an hour of staring at "Solver could not find a feasible solution."

### What You Submit on Canvas
**1) Excel (.xlsx)**  
This should be your Task 1 file extended.

**2) Short write-up (half to one page)**  
Answer these:

- How did you implement the "2 to 3 games per pair" rule?
- How many games did Solver schedule?
- Which pairs ended up at 3 games, and which stayed at 2?
- What stopped the schedule from adding more games?

---

## Task 3: Keep Task 2 Rules, Improve Rest

Task 3 keeps the Task 2 rules, but now you care about rest. You will still produce a valid schedule, but you will choose among valid schedules by how much back-to-back play you create.

### Goal
Minimize total rest violations.

A "rest violation" means a team plays on consecutive days (day d and day d+1). You will model that with extra binary variables.

### Constraints
All Task 2 constraints remain fixed and must still hold:
- Daily capacity
- One game per team per day
- Each pair plays between 2 and 3 games total

Then you add whatever linking constraints are needed to define rest violations correctly.

### What You Submit on Canvas
**1) Excel (.xlsx)**  
Again, this is Task 2 extended, not a fresh start.

**2) Short write-up (about one page)**  
Answer these:

- How did you define and model a rest violation?
- What is the minimum number of rest violations you achieved?
- Is zero rest violations possible under the Task 2 rules? If yes, show how you know. If not, explain what forces violations.
- Which constraint felt like the main "bottleneck" once you started caring about rest?
- One reflection: minimizing total rest violations is not the same thing as fairness. Give one example of how an "optimal" schedule could still feel unfair.

---

## Grading Focus

We will look at:

- Correct logic (the model matches what the words say)
- Clear implementation (your spreadsheet is readable and auditable)
- Good explanations (you can defend your choices and interpret Solver output)

There is no single "right schedule." There are many wrong models, though. Most of them fail in predictable ways.

---

## Final Note

If your model blow pasts 200 decision variables, that is a formulation problem, not a computing problem. Shrink it. A good model usually looks simpler than you expected.
