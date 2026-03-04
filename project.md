# Blue Ridge Summer League

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

---

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
  - August 3 and August 7: at most 1 game.
  - All other days: at most 2 games.

Facilities and time slots are not explicitly modeled. The schedule is formulated at the day level.

Students are encouraged to verify implied bounds before solving. For example:

- There are 6 distinct team pairs.
- If each pair plays at least 2 games, the schedule must contain at least 12 total games.
- If each pair plays at most 3 games, the schedule cannot exceed 18 total games.

Failure to verify these structural bounds typically results in infeasible or logically inconsistent models.

---

## Worked mini-example

To verify your understanding of the variable structure, consider a simplified version of the problem.

**Setup:** 2 teams (A, B), 3 days, at most 1 game per day, the pair must play at least 1 and at most 2 games.

The single decision variable for each day is:

| | Day 1 | Day 2 | Day 3 |
|---|---|---|---|
| A vs B | $x_1$ | $x_2$ | $x_3$ |

where $x_d \in \\{0, 1\\}$ indicates whether the pair plays on day $d$.

**Valid schedule:** $x_1 = 1, x_2 = 0, x_3 = 1$ -- the pair plays on Days 1 and 3 (2 games, satisfies all constraints, no consecutive-day play).

**Infeasible schedule:** $x_1 = 1, x_2 = 1, x_3 = 1$ -- 3 games violates the upper bound of 2 games for this pair.

In the full problem, you will have 6 pairs and 10 days. The variable structure scales accordingly.

---

# Timeline (Weeks 9-16)

| Week     | Phase              | Deliverable                                                      |
|----------|--------------------|------------------------------------------------------------------|
| Week 9   | Phase 1            | Baseline formulation                                             |
| Week 10  | Phase 2            | Rest optimization                                                |
| Week 11  | Feedback and review | Instructor feedback on Phases 1-2; prepare for AI evaluation     |
| Week 12  | Phase 3            | AI replication and evaluation; Phase 4 modification proposal due |
| Week 13  | Phase 4a           | Structural modification: formulate and solve extended model      |
| Week 14  | Phase 4b           | AI stress test and comparative analysis                          |
| Week 15  | Final reflection   | Synthesis                                                        |

---

# Phase 1: Baseline formulation (25 points)

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
- After obtaining the integer solution, solve the LP relaxation (change Solver to allow continuous variables) and compare the relaxation bound to the integer optimal value. Report the integrality gap.

> 🔍 **Checkpoint - verify before running Solver:**
> - How many binary decision variables does your model have?
> - What is the theoretical maximum number of games? The minimum?
> - Does your constraint count match the number of structural requirements listed above?

## Submission requirements

- Excel file (.xlsx)
- Written explanation (approximately 1 page) addressing:
  - Decision variable definitions.
  - Objective function.
  - Complete constraint structure.
  - Identification and interpretation of binding constraints.
  - LP relaxation bound and integrality gap interpretation.

- Brief reflection (2-3 sentences): What surprised you about the relationship between constraints and the feasible region?

### Phase 1 rubric (25 points)

- Formulation correctness: 12
- Solver implementation and configuration: 8
- Clarity and technical precision: 5

---

# Phase 2: Schedule quality and constraint interaction (45 points)

All Phase 1 constraints remain in force.

## Objective

Minimize total rest violations.

A rest violation occurs when a team plays on consecutive days.

## Modeling expectations

- Introduce additional binary variables to represent rest violations if necessary.
- Properly link rest variables to game variables using logically correct linear constraints.
- Preserve all previously defined constraints without weakening them.
- Prove or disprove: zero rest violations are achievable under the pairwise and capacity constraints. Provide a structured argument that references specific constraint interactions (e.g., capacity limits on August 3 and 7, pairwise lower bounds, daily game limits).

Students should explicitly consider:

- Whether capacity limits on August 3 and August 7 induce unavoidable clustering.
- Whether pairwise lower bounds force scheduling density.
- How daily limits and pairwise requirements jointly constrain feasible spacing.

Superficial rest-counting approaches without correct logical linkage will receive reduced credit.

> 🔍 **Checkpoint - verify before running Solver:**
> - Is zero rest violations feasible? Write your argument before solving.
> - How many new variables did you introduce? Are they correctly linked to the game variables?
> - Did you preserve all Phase 1 constraints without modification?

## Submission requirements

- Updated Excel file.
- Written explanation (1-2 pages) addressing:
  - Mathematical modeling of rest violations.
  - Feasibility of zero violations.
  - Identification of structurally binding constraints.
  - Interaction between daily capacity and pairwise bounds.
  - Observations regarding Solver behavior.

- Brief reflection (2-3 sentences): Which constraint interaction was hardest to model correctly? Why?

### Phase 2 rubric (45 points)

- Correct modeling of rest violations: 18
- Preservation of prior constraints: 10
- Depth of structural analysis: 12
- Clarity and organization: 5

---

# Phase 3: AI replication and diagnostic evaluation (50 points)

Students will prompt a publicly available AI system to formulate the Phase 2 model.

Your prompt must include the complete problem description, all constraints, and the objective function. A vague prompt (e.g., “make a sports schedule in Excel”) will not yield a meaningful comparison and will receive reduced credit for the analytical portion.

## Required steps

1. Include the exact prompt used.
2. Implement the AI’s formulation exactly as generated.
3. Attempt to solve the AI model before making any corrections.

Do not modify the AI model prior to diagnostic analysis.

> 🔍 **Checkpoint - before beginning your analysis:**
> - Does your prompt include the full problem description and all constraints?
> - Did you implement the AI’s formulation exactly as generated, without corrections?
> - Did you attempt to solve it in Solver before analyzing?

## Analytical requirements (approximately 2 pages)

Students must evaluate:

- Appropriateness of decision variables.
- Completeness of constraint structure.
- Presence of redundant or unnecessary constraints.
- Logical errors in constraint construction.
- Feasibility or infeasibility in Solver.
- Compliance with Solver’s 200-variable limit.

Use the following comparison framework to structure your analysis:

| Dimension                          | Your Model (Phase 2) | AI-Generated Model | Assessment |
|------------------------------------|----------------------|--------------------|-----------:|
| Decision variable definitions      |                      |                    |            |
| Number of decision variables       |                      |                    |            |
| Constraint count                   |                      |                    |            |
| Constraint correctness (list errors) |                    |                    |            |
| Objective function                 |                      |                    |            |
| Solver feasibility                 |                      |                    |            |
| 200-variable limit compliance      |                      |                    |            |

Where applicable, reference specific constraint expressions and Solver output.

Statements such as “the AI model was incomplete” without supporting evidence will receive minimal credit.

- Brief reflection (2-3 sentences): What did the AI get right that you expected it to get wrong, or vice versa?

### Phase 3 rubric (50 points)

- Accurate implementation of AI formulation: 5
- Identification of structural deficiencies: 25
- Comparative reasoning between human and AI models: 15
- Clarity, specificity, and supporting evidence: 5

---

# Phase 4: Structural modification and AI stress test (60 points)

Students will introduce one substantive structural modification to the model.

## Structural modification

Propose and justify your own structural modification. The following are examples of modifications that qualify, but you are encouraged to design one that reflects a realistic scheduling concern:

- Rolling window constraint (e.g., no 3 games within any 4 consecutive days).
- Min-max fairness objective.
- Weighted multi-objective formulation.
- Asymmetric team availability constraints.
- Equity constraints on total idle days.

Merely changing numerical parameter values does not qualify as a structural modification.

**Proposal requirement:** Submit a 1-paragraph proposal describing your chosen modification by the end of Week 12. The instructor will confirm that it qualifies before you proceed with implementation.

## Required steps

1. Modify and solve your extended model.
2. Prompt AI to formulate the modified version.
3. Implement the AI formulation.
4. Compare structural robustness and Solver behavior.

> 🔍 **Checkpoint - before your comparative analysis:**
> - Has your modification proposal been approved by the instructor?
> - How does your modification change the feasible region compared to Phase 2?
> - Can you quantify the change in objective value?

## Analytical requirements (approximately 2 pages)

Students must explain:

- The structural modification introduced.
- Why the modification increases modeling complexity.
- How Solver behavior changes relative to earlier phases.
- Points at which AI reasoning weakens or remains robust.
- Any subtle formulation inconsistencies in the AI model.
- Quantitative marginal impact: How does the objective value change? Does the feasible region shrink, and by how much?

A high-quality analysis distinguishes between cosmetic differences and genuine structural weaknesses.

- Brief reflection (2-3 sentences): How did your structural modification change the difficulty of the problem?

### Phase 4 rubric (60 points)

- Quality and rigor of structural modification: 20
- Correct extended formulation: 15
- AI stress-test evaluation: 20
- Depth of analytical insight: 5

---

# Final reflection (20 points)

Maximum length: 1 page.

This reflection should synthesize your per-phase observations into broader insights. Revisit your brief reflections from Phases 1-4 and address:

1. Under what conditions does an optimization model become structurally fragile?
2. Which types of constraints most significantly increase modeling complexity?
3. In what contexts is AI assistance appropriate in optimization modeling, and where is independent formulation preferable?
4. What did you learn about the relationship between formulation detail and Solver behavior?

Your responses must reference specific experiences from the project. General statements without connection to your modeling work will receive reduced credit.

### Final reflection rubric (20 points)

- Conceptual insight: 10
- Integration of per-phase observations: 5
- Clarity and coherence: 5

---

# Grading summary

| Component        | Points  |
|------------------|---------|
| Phase 1          | 25      |
| Phase 2          | 45      |
| Phase 3          | 50      |
| Phase 4          | 60      |
| Final reflection | 20      |
| **Total**        | **200** |

---

# Evaluation standards

This project assesses:

- Formulation accuracy.
- Logical consistency.
- Solver competence.
- Structural reasoning.
- Critical evaluation of AI-generated optimization models.

There is no requirement that AI must fail.  
There is an expectation that students can explain how structural complexity alters feasibility, optimality, and model robustness.
