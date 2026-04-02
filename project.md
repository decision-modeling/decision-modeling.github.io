# Blue Ridge Summer League
## Formulation, Structural Analysis, and AI Evaluation in Optimization Modeling

You have been hired as the scheduling analyst for the Blue Ridge Summer League. The league commissioner needs a schedule that is fair, compact, and accounts for team rest. Your job is to build the optimization model, evaluate whether AI tools can replicate your work, and redesign the model under new league priorities.

This project is designed as a multi-phase decision-modeling exercise. Across the semester, you will move from baseline model construction to model extension, AI-assisted evaluation, and structural redesign under changing managerial priorities. The purpose of the project is not only to practice optimization techniques, but also to develop the ability to explain, evaluate, and defend modeling choices in a realistic decision context.

You will:

1. Formulate and solve a constrained integer programming model.
2. Extend the model to incorporate schedule quality considerations.
3. Evaluate AI-generated formulations of the same problem.
4. Redesign the model under a changed league priority.
5. Analyze how structural changes affect feasibility, optimality, and model robustness.

The objective is not merely to construct a feasible schedule. Rather, the project is designed to examine how modeling decisions, constraint interaction, objective selection, and managerial priorities influence optimization behavior. Later phases explicitly evaluate the reliability and limitations of AI-generated optimization models.

All models must be implemented in Microsoft Excel using Solver and must remain within the 200 decision variable limit and 100 constraint limit of the standard Solver configuration.

* * *

# Problem setting

## Participating teams

- Virginia Tech
- Radford University
- James Madison University
- Virginia Military Institute

## Scheduling horizon

- August 1 through August 10 (10 consecutive days)

## Scheduling rules

- A team may play at most one game per day.
- Each game involves exactly two distinct teams.
- Daily league capacity:
  - August 3 and August 7: at most 1 game
  - All other days: at most 2 games

Facilities and time slots are not explicitly modeled. The schedule is formulated at the day level.

Before solving, you should verify several implied bounds:

- There are 6 distinct team pairs.
- If each pair plays at least 2 games, the schedule must contain at least 12 total games.
- If each pair plays at most 3 games, the schedule cannot exceed 18 total games.

Failure to verify these structural bounds often leads to infeasible or logically inconsistent models.

* * *

# Worked mini-example

To verify your understanding of the variable structure, consider a simplified version of the problem.

**Setup:** 2 teams (A, B), 3 days, at most 1 game per day, and the pair must play at least 1 and at most 2 games.

The single decision variable for each day is:

| | Day 1 | Day 2 | Day 3 |
|---|---|---|---|
| A vs B | $x_1$ | $x_2$ | $x_3$ |

where $x_d \in \\{0, 1\\}$ indicates whether the pair plays on day $d$.

Valid schedule: $x_1 = 1, x_2 = 0, x_3 = 1$ 
- The pair plays on Days 1 and 3, which satisfies all constraints and avoids consecutive-day play.

Infeasible schedule: $x_1 = 1, x_2 = 1, x_3 = 1$
- This gives 3 games and violates the upper bound of 2 games for this pair.

In the full problem, you will have 6 pairs and 10 days. The variable structure scales accordingly.

* * *

# Timeline (Weeks 9–16)

| Week | Phase | Deliverable |
|---|---|---|
| Week 9 | Phase 1 | Baseline formulation |
| Week 10 | Phase 2 | Schedule quality and constraint interaction |
| Week 11 | Feedback and review | Instructor feedback on Phases 1–2; prepare for AI evaluation |
| Week 12 | Phase 3 | AI-assisted formulation, equivalence, and model responsibility |
| Week 13 | Phase 4a | Structural redesign under a new league priority |
| Week 14 | Phase 4b | AI redesign evaluation and comparative analysis |
| Week 15 | Final reflection | Synthesis |

* * *

# Phase 1: Baseline formulation (25 points)

In this phase, you will build a baseline scheduling model for the Blue Ridge Summer League. The goal is to translate the league’s basic rules and requirements into a workable optimization model.

This phase establishes the foundation for the rest of the project. Your objective is not only to produce a correct baseline formulation, but also to begin thinking carefully about what the model includes, what it leaves out, and what assumptions make the formulation possible.

## Objective

Maximize the total number of games scheduled over the 10-day horizon.

## Required constraints

Your model must enforce:

1. Daily capacity limits.
2. At most one game per team per day.
3. Each pair of teams plays at least 2 games and at most 3 games over the full horizon.

## Implementation guidance

- Clearly define binary decision variables that indicate whether a specific pair plays on a specific day.
- Avoid over-granular formulations that unnecessarily expand the variable count.
- Confirm that your model respects the implied lower and upper bounds on total games before running Solver.
- Verify that Solver is set to binary decision variables and that the objective direction is correct.
- After obtaining the integer solution, solve the LP relaxation and compare the relaxation bound to the integer optimal value. Report the integrality gap.

> **Checkpoint**
>
> - How many binary decision variables does your model have?
> - What is the theoretical maximum number of games? What is the minimum?
> - Does your constraint count match the number of structural requirements listed above?

## Submission requirements

- Excel file (.xlsx)
- Written explanation (approximately 1 page) addressing:
  - Decision variable definitions
  - Objective function
  - Complete constraint structure
  - Identification and interpretation of binding constraints
  - LP relaxation bound and integrality gap interpretation
- Brief reflection (2–3 sentences): What surprised you about the relationship between constraints and the feasible region?

### Phase 1 rubric (25 points)

- Formulation correctness: 12
- Solver implementation and configuration: 8
- Clarity and technical precision: 5

* * *

# Phase 2: Schedule quality and constraint interaction (45 points)

In Phase 2, you will extend your baseline model to account for schedule quality through rest considerations. The goal is to move beyond simple feasibility and begin evaluating what makes a schedule more desirable from a managerial perspective.

This phase asks you to examine the tradeoff between schedule quantity and schedule quality. In doing so, you should begin to think not only about how to modify the model, but also about what values your formulation is prioritizing.

All Phase 1 constraints remain in force.

## Objective

Minimize total rest violations.

A rest violation occurs when a team is scheduled to play on two consecutive days (i.e., day $t$ and day $t+1$). Each such occurrence counts as one violation.

> Note: A team can play at most one game per day, so a rest violation only depends on whether the team plays on adjacent days, not on the number of games.

> Hint: In addition to the Phase 1 constraints, you will need to introduce new variables and constraints to track when a team plays on consecutive days.
>
> This typically requires:
> - Defining whether each team plays on each day, and  
> - Defining whether a rest violation occurs between consecutive days  
> 
> These variables must be properly linked so that a rest violation is counted if and only if a team plays on both day $t$ and day $t+1$.


## Modeling expectations

- Introduce additional binary variables to represent rest violations if necessary.
- Properly link rest variables to game variables using logically correct linear constraints.
- Preserve all previously defined constraints without weakening them.
- Prove or disprove: zero rest violations are achievable under the pairwise and capacity constraints. Provide a structured argument that references specific constraint interactions, such as capacity limits on August 3 and 7, pairwise lower bounds, and daily game limits.

You should explicitly consider:

- Whether capacity limits on August 3 and August 7 induce unavoidable clustering.
- Whether pairwise lower bounds force scheduling density.
- How daily limits and pairwise requirements jointly constrain feasible spacing.

Superficial rest-counting approaches without correct logical linkage will receive reduced credit.

> **Checkpoint**
>
> - Is zero rest violations feasible? Write your argument before solving.
> - How many new variables did you introduce? Are they correctly linked to the game variables?
> - Did you preserve all Phase 1 constraints without modification?

## Submission requirements

- Updated Excel file
- Written explanation (1–2 pages) addressing:
  - Mathematical modeling of rest violations
  - Feasibility of zero violations
  - Identification of structurally binding constraints
  - Interaction between daily capacity and pairwise bounds
  - Observations regarding Solver behavior
- Brief reflection (2–3 sentences): Which constraint interaction was hardest to model correctly? Why?

## Solver limits and alternatives

A fully correct linearization of the Phase 2 model will likely exceed Excel Solver's 200-variable and 100-constraint limits. You have two paths:

- **Stay nonlinear**: keep the model within limits and use Excel's GRG Nonlinear or Evolutionary solver. Neither guarantees a globally optimal solution.
- **Linearize fully**: properly link rest variables to game variables with linear constraints, then use [LibreOffice Calc](https://www.libreoffice.org/discover/calc/)'s solver, which supports larger models and provides a spreadsheet experience similar to Excel. You are also encouraged to use AI to generate scaffolding code to solve the model with other solvers such as [PuLP](https://coin-or.github.io/pulp/).

You are not required to pursue either path. If your model hits the solver limit, document what happened and reflect on the trade-off between model form, solver choice, and solution quality.

### Phase 2 rubric (45 points)

- Correct modeling of rest violations: 18
- Preservation of prior constraints: 10
- Depth of structural analysis: 12
- Clarity and organization: 5

* * *

## Transition to the second half of the project

By the end of Phase 2, you have already constructed and extended a workable scheduling model. The second half of the project shifts the focus from model construction alone to model evaluation, model responsibility, and model redesign.

In Phase 3, you will examine whether a publicly available AI system can meaningfully reproduce the structure and logic of your model. In Phase 4, you will redesign the model under a changed league priority and evaluate how that shift alters the tradeoffs and recommendations. Across both phases, the goal is not merely to obtain a feasible model, but to determine which model version you are willing to defend and why.

* * *

# Phase 3: AI-assisted formulation, equivalence, and model responsibility (50 points)

In Phase 2, you extended your model to account for schedule quality through rest considerations. In this phase, you will examine whether a publicly available AI system can produce a formulation that is equivalent to, or meaningfully different from, your Phase 2 model.

The purpose of this phase is **not** simply to show that AI makes mistakes. In some cases, the AI-generated model may be largely correct. Your task is to determine whether the AI-generated formulation is truly equivalent to your Phase 2 model, whether it is preferable in any meaningful way, and which version you are ultimately willing to defend.

## Required steps

1. Include the exact prompt used.
2. Prompt a publicly available AI system to formulate the Phase 2 problem.
3. Implement the AI-generated model exactly as generated.
4. Attempt to solve the AI-generated model before making any corrections.
5. Compare your Phase 2 model, the AI-generated model, and your final responsible model.

Do **not** correct the AI-generated model before analyzing it.

> **Note on linearity and solver compatibility**: Your prompt to the AI must explicitly require a linear formulation. AI tools often produce nonlinear formulations (e.g., products of binary variables) that are incompatible with Excel Solver's Simplex LP method. If the AI-generated model is nonlinear despite your instruction, revise your prompt until a linear formulation is obtained. If the resulting linear model exceeds Excel Solver's 200-variable or 100-constraint limit, use [LibreOffice Calc](https://www.libreoffice.org/discover/calc/)'s solver, which supports larger models and provides a spreadsheet experience similar to Excel. You are also encouraged to use AI to generate scaffolding code to solve the model with other solvers such as [PuLP](https://coin-or.github.io/pulp/).

## Your analysis should address

- Is the AI-generated model correct?
- Is it fully equivalent to your Phase 2 model?
- If the two models differ, where do they differ?
- If both models are valid, which formulation is more interpretable, compact, or extensible?
- Did the AI preserve the key tradeoff embedded in your Phase 2 model?
- Is the AI-generated model logically correct, feasible, and solvable in Excel Solver?
- Does the AI-generated model comply with Solver's 200-variable limit and 100-constraint limit?
- Which model version would you ultimately defend, and why?

Use the following comparison structure:

| Dimension | Your Phase 2 Model | AI-Generated Model | Final Responsible Model |
|---|---|---|---|
| Decision variables |  |  |  |
| Objective function |  |  |  |
| Constraint structure |  |  |  |
| Logical correctness |  |  |  |
| Solver feasibility |  |  |  |
| 200-variable limit compliance |  |  |  |
| 100-constraint limit compliance |  |  |  |
| Interpretability / compactness |  |  |  |
| Extensibility for future redesign |  |  |  |
| Which version you would defend and why |  |  |  |

A strong submission does **not** require the AI-generated model to be wrong. High-quality work may show that the AI-generated model is largely correct, while still carefully comparing formulation quality, assumptions, interpretability, and defensibility across versions.

## Required reflection

Briefly address the following:

1. Which AI suggestions, if any, would you keep?
2. Which AI suggestions would you reject?
3. If both models are technically valid, why would you still prefer one over the other?
4. If your judgment is wrong, what is the most likely downstream consequence for the league?

## Submission requirements

- Updated Excel file for the AI-generated model
- Updated Excel file for the final responsible model
- Written analysis (approximately 2 pages)
- Brief reflection (2–3 sentences): What did the AI appear to understand, and what still required human judgment?

### Phase 3 rubric (50 points)

| Criterion | Points |
|---|---:|
| Accurate implementation of the AI-generated model | 5 |
| Evaluation of correctness and equivalence | 10 |
| Quality of comparison across model versions | 10 |
| Analysis of formulation quality, interpretability, and extensibility | 10 |
| Evidence of model ownership and responsible judgment | 10 |
| Clarity, specificity, and supporting evidence | 5 |
| **Total** | **50** |

* * *

# Phase 4: Structural redesign under a new league priority (60 points)

In this phase, the league commissioner has introduced a new managerial priority. Your task is not simply to add another constraint. Instead, you must redesign the model so that it reflects a meaningful change in what the league values.

The purpose of this phase is to evaluate your ability to revise a model when managerial priorities shift, and to assess whether AI can meaningfully support that redesign. A strong redesign should do more than make the model more complicated. It should make clear what value is being protected, what tradeoff is being introduced, and what new limitations arise.

## Structural redesign

Select **one** substantive structural redesign that reflects a realistic new league priority. Examples include, but are not limited to:

- A fairness requirement that limits how unevenly rest burden is distributed across teams
- A compactness requirement that reduces the overall schedule span or limits long idle gaps
- Asymmetric team availability constraints
- An equity rule related to total idle days or inconvenient scheduling patterns
- A revised objective that balances total games against another league priority

Merely changing numerical parameter values does **not** count as a structural redesign.

## Required steps

1. Select and justify one new league priority.
2. Redesign and solve your extended model.
3. Compare the redesigned model with your earlier model.
4. Prompt AI to formulate the redesigned problem.
5. Implement the AI-generated redesign.
6. Compare your redesign with the AI-generated redesign.
7. Provide a final recommendation to the league commissioner under the new priority.

> **Note on linearity and solver compatibility**: Your prompt to the AI must explicitly require a linear formulation. AI tools often produce nonlinear formulations (e.g., products of binary variables) that are incompatible with Excel Solver's Simplex LP method. If the AI-generated redesign is nonlinear despite your instruction, revise your prompt until a linear formulation is obtained. If the resulting linear model exceeds Excel Solver's 200-variable or 100-constraint limit, use [LibreOffice Calc](https://www.libreoffice.org/discover/calc/)'s solver, which supports larger models and provides a spreadsheet experience similar to Excel. You are also encouraged to use AI to generate scaffolding code to solve the model with other solvers such as [PuLP](https://coin-or.github.io/pulp/).

## Your analysis should address

- What new league priority did you introduce?
- Why does this change require a structural redesign rather than a simple parameter adjustment?
- How does your redesigned formulation differ from the earlier model?
- What did the redesign improve?
- What did the redesign make worse?
- What tradeoff did the redesign introduce or intensify?
- How did the redesign affect feasibility, objective value, or schedule quality?
- Is the AI-generated redesign correct?
- If both redesigns are valid, which one is more interpretable, defensible, or easier to extend?
- Where did AI remain useful, and where did AI become unreliable?

A strong submission will focus not only on technical changes, but also on the managerial consequences of the redesign.

## Executive recommendation

Write a short executive recommendation (200–300 words) to the league commissioner that addresses:

- What new priority you incorporated
- What your redesigned model achieved
- What tradeoff or cost the league had to accept
- One important limitation or remaining risk
- Which version of the redesigned model you would ultimately defend, and why

## Submission requirements

- Updated Excel file for your redesigned model
- Updated Excel file for the AI-generated redesign
- Written analysis (approximately 2 pages)
- Executive recommendation (200–300 words)
- Brief reflection (2–3 sentences): How did the new league priority change the kind of judgment required from you as the modeler?

### Phase 4 rubric (60 points)

| Criterion | Points |
|---|---:|
| Quality and justification of the structural redesign | 15 |
| Correctness of the redesigned formulation | 10 |
| Analysis of tradeoffs and managerial consequences | 10 |
| Evaluation of the AI-generated redesign | 10 |
| Comparison of defensibility, interpretability, and extensibility across redesigns | 10 |
| Clarity, organization, and supporting evidence | 5 |
| **Total** | **60** |

* * *

# Final reflection (20 points)

Maximum length: 1 page.

This reflection should synthesize your per-phase observations into broader insights. Revisit your brief reflections from Phases 1–4 and address:

1. Under what conditions does an optimization model become structurally fragile?
2. Which types of constraints most significantly increase modeling complexity?
3. In what contexts is AI assistance appropriate in optimization modeling, and where is independent formulation preferable?
4. What did you learn about the relationship between formulation detail and Solver behavior?

Your responses must reference specific experiences from the project. General statements without connection to your modeling work will receive reduced credit.

### Final reflection rubric (20 points)

- Conceptual insight: 10
- Integration of per-phase observations: 5
- Clarity and coherence: 5

* * *

# Grading summary

| Component | Points |
|---|---:|
| Phase 1 | 25 |
| Phase 2 | 45 |
| Phase 3 | 50 |
| Phase 4 | 60 |
| Final reflection | 20 |
| **Total** | **200** |

* * *

# Evaluation standards

This project assesses:

- Formulation accuracy
- Logical consistency
- Solver competence
- Structural reasoning
- Responsible evaluation of AI-generated optimization models
- Interpretation of modeling tradeoffs and managerial consequences

There is no requirement that AI must fail.

There is an expectation that you can explain how structural complexity, modeling assumptions, and changing priorities alter feasibility, optimality, and model robustness.
