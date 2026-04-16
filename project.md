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

For Phases 1 and 2, AI tools may not be used to formulate or revise the mathematical model. The first phase in which AI may be asked to create or redesign a model is Phase 3. In Phase 2, AI may be used only for solver scaffolding code if you are solving a formulation that you created yourself outside Excel.

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

- **Stay nonlinear**: keep the model within limits and use Excel's Evolutionary solver. This may find a feasible or good solution, but it does not guarantee a globally optimal solution.
- **Linearize fully**: properly link rest variables to game variables with linear constraints, then use [LibreOffice Calc](https://www.libreoffice.org/discover/calc/)'s [solver](https://help.libreoffice.org/latest/en-US/text/scalc/01/solver.html), which supports larger models and provides a spreadsheet experience similar to Excel. You may use AI to generate scaffolding code to solve the model with other solvers such as [PuLP](https://coin-or.github.io/pulp/), but not to formulate or revise the Phase 2 model itself.

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

The purpose of this phase is **not** to produce a perfect model. It is to make you responsible for the final model you submit. AI tools make mistakes: they may misinterpret constraints, introduce nonlinearities, omit key requirements, or produce formulations that are technically solvable but logically wrong. They may also get things largely right. In either case, your job is to decide what to adopt, what to discard, and what to correct. The final model you submit is yours, not the AI's.

If the AI system cannot produce a correct model within the assignment constraints, document that limitation rather than treating the attempt as successful. Explain what failed, what follow-up prompts you tried, and why the result still did not satisfy the requirements. You may repair or rebuild the model yourself, but make clear which parts reflect human correction or reconstruction.

Your task is to compare the two formulations, identify where they agree and where they differ, and build the final model you are willing to defend, drawing from either or both as your judgment requires.

## Required steps

1. Include the exact prompt used and the name of the AI system and model version.
2. Prompt a publicly available AI system to formulate the Phase 2 problem.
3. Implement the AI-generated model exactly as generated.
4. Attempt to solve the AI-generated model before making any corrections.
5. Compare your Phase 2 model, the AI-generated model, and your final responsible model.

Do **not** correct the AI-generated model before analyzing it.

> **Note on linearity and solver compatibility**: Your prompt to the AI must explicitly require a linear formulation. AI tools often produce nonlinear formulations (e.g., products of binary variables) that are incompatible with Excel Solver's Simplex LP method. If the AI-generated model is nonlinear despite your instruction, use follow-up prompts to request a linear formulation. If the AI still cannot produce a linear, logically correct, constraint-compliant model, document that failure and proceed with your final responsible model. If the resulting linear model exceeds Excel Solver's 200-variable or 100-constraint limit, use [LibreOffice Calc](https://www.libreoffice.org/discover/calc/)'s [solver](https://help.libreoffice.org/latest/en-US/text/scalc/01/solver.html), which supports larger models and provides a spreadsheet experience similar to Excel. You are also encouraged to use AI to generate scaffolding code to solve the model with other solvers such as [PuLP](https://coin-or.github.io/pulp/).

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
| What you adopted from this version, and why |  |  |  |

The final responsible model may draw from your Phase 2 model, from the AI-generated model, or from both. A strong submission does **not** require the AI to be wrong, nor does it require you to pick one version wholesale. What it requires is that every element in the final model reflects a deliberate choice you can explain and defend.

## Required reflection

Briefly address the following:

1. Which AI suggestions did you adopt in your final model, and why?
2. Which AI suggestions did you reject or modify, and why?
3. What does your final model include that neither the AI nor your Phase 2 model captured well on its own?
4. If your judgment turns out to be wrong, what is the most likely downstream consequence for the league?

## Submission requirements

- Updated Excel file for the AI-generated model
- Updated Excel file for the final responsible model
- Written analysis (approximately 2 pages)
- Brief reflection (2–3 sentences): What did the AI appear to understand, and what still required human judgment?

### Phase 3 rubric (50 points)

| Criterion | Points |
|---|---:|
| Accurate implementation of the AI-generated model | 5 |
| Evaluation of AI output: correctness, gaps, and quality | 10 |
| Quality of comparison across model versions | 10 |
| Deliberateness of the final model: what was adopted, rejected, or synthesized, and why | 15 |
| Clarity, specificity, and supporting evidence | 10 |
| **Total** | **50** |

* * *

# Phase 4: Creative structural redesign under a real-world scheduling priority (60 points)

In this phase, the league commissioner has asked you to make the Blue Ridge Summer League more realistic, more interesting, or more strategically defensible. Your task is not simply to add another constraint. Instead, you must research how real sports leagues or tournaments think about scheduling, borrow or adapt one scheduling idea, and redesign the model so that it reflects a meaningful change in what the league values.

You may draw inspiration from professional, college, or amateur sports contexts, such as the ACC, NBA, MLB, WNBA, NCAA tournaments, travel leagues, or local recreational leagues. Real schedulers consider issues such as travel burden, rest equity, venue availability, competitive balance, rivalry games, broadcast windows, fan experience, compactness, academic calendars, and fairness across teams. Your redesign should adapt one such idea to the smaller Blue Ridge Summer League setting.

The purpose of this phase is to evaluate your ability to revise a model when managerial priorities shift, and to assess whether AI can meaningfully support that redesign. A strong redesign should do more than make the model more complicated. It should make clear where the scheduling idea came from, what value is being protected, what tradeoff is being introduced, and what new limitations arise.

As in Phase 3, AI output is not automatically acceptable. If the AI-generated redesign cannot satisfy the new priority, the original scheduling rules, or the solver constraints, document the failure, explain what follow-up attempts you made, and decide what must be corrected or rebuilt by you.

## Structural redesign

Select **one** substantive structural redesign inspired by a real-world scheduling concern. Examples include, but are not limited to:

- A fairness requirement that limits how unevenly rest burden is distributed across teams
- A compactness requirement that reduces the overall schedule span or limits long idle gaps
- Asymmetric team availability constraints
- An equity rule related to total idle days or inconvenient scheduling patterns
- A revised objective that balances total games against another league priority
- A travel-related rule that clusters games or reduces repeated long-distance trips
- A rivalry or marquee-game requirement that protects specific matchups
- A venue-availability or preferred-date constraint
- A fan-experience rule that avoids long gaps, overloaded days, or poorly spaced rematches

Merely changing numerical parameter values does **not** count as a structural redesign.

## Required steps

1. Research how a real sports league, tournament, or scheduling context handles a scheduling concern.
2. Select and justify one new league priority adapted from that real-world example.
3. Redesign and solve your extended model.
4. Compare the redesigned model with your previous responsible model before the new priority was introduced.
5. Prompt AI to formulate the redesigned problem. Include the exact prompt used and the name of the AI system and model version.
6. Test the AI-generated redesign exactly as generated, before making any corrections.
7. Evaluate the AI-generated redesign and decide what to adopt, reject, or modify.
8. Build your final responsible redesign, drawing from either or both versions as your judgment requires.
9. Provide a final recommendation to the league commissioner under the new priority.

> **Note on linearity and solver compatibility**: Your prompt to the AI must explicitly require a linear formulation. AI tools often produce nonlinear formulations (e.g., products of binary variables) that are incompatible with Excel Solver's Simplex LP method. If the AI-generated redesign is nonlinear despite your instruction, use follow-up prompts to request a linear formulation. If the AI still cannot produce a linear, logically correct, constraint-compliant redesign, document that failure and proceed with your final responsible redesign. If the resulting linear model exceeds Excel Solver's 200-variable or 100-constraint limit, use [LibreOffice Calc](https://www.libreoffice.org/discover/calc/)'s [solver](https://help.libreoffice.org/latest/en-US/text/scalc/01/solver.html), which supports larger models and provides a spreadsheet experience similar to Excel. You are also encouraged to use AI to generate scaffolding code to solve the model with other solvers such as [PuLP](https://coin-or.github.io/pulp/).

## Your analysis should address

- What new league priority did you introduce?
- What real-world scheduling practice, league, tournament, or scheduling concern inspired your redesign?
- How did you adapt that idea to the Blue Ridge Summer League setting?
- Why does this change require a structural redesign rather than a simple parameter adjustment?
- How does your redesigned formulation differ from the earlier model?
- What did the redesign improve?
- What did the redesign make worse?
- What tradeoff did the redesign introduce or intensify?
- How did the redesign affect feasibility, objective value, or schedule quality?
- Is the AI-generated redesign correct? Where does it succeed and where does it fall short?
- What did you adopt from the AI-generated redesign, what did you reject, and why?
- How does your final redesign compare to both earlier versions in terms of interpretability, defensibility, and extensibility?
- Where did AI remain useful, and where did it require correction or replacement?

A strong submission will focus not only on technical changes, but also on the managerial consequences of the redesign. As in Phase 3, the final redesign you submit is yours to own and defend, regardless of how much or how little it draws from the AI.

## Executive recommendation

Write a short executive recommendation (200–300 words) to the league commissioner that addresses:

- What new priority you incorporated
- What real-world scheduling idea inspired the redesign
- What your redesigned model achieved
- What tradeoff or cost the league had to accept
- One important limitation or remaining risk
- Which elements of the final redesign you would defend, and why — noting what you took from your own work, from the AI, or from combining both

## Submission requirements

- Updated Excel file for your final redesigned model
- Written analysis (approximately 2 pages)
- Executive recommendation (200–300 words)
- Brief reflection (2–3 sentences): How did the new league priority change the kind of judgment required from you as the modeler?

### Phase 4 rubric (60 points)

| Criterion | Points |
|---|---:|
| Quality and justification of the structural redesign | 15 |
| Correctness of the final redesigned formulation | 10 |
| Analysis of tradeoffs and managerial consequences | 10 |
| Evaluation of the AI-generated redesign: correctness, gaps, and quality | 10 |
| Deliberateness of the final redesign: what was adopted, rejected, or synthesized, and why | 10 |
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
