# Blue Ridge Summer League

## Formulation, Structural Analysis, and AI Evaluation in Optimization Modeling  

This project integrates formulation, implementation, structural analysis, and critical evaluation of AI-assisted modeling within a unified scheduling problem.

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

# Timeline (Weeks 9–16)

| Week | Phase | Deliverable |
|------|-------|-------------|
| Week 9 | Phase 1 | Baseline formulation |
| Week 10 | Phase 2 | Rest optimization |
| Week 12 | Phase 3 | AI replication and evaluation |
| Weeks 13–14 | Phase 4 | Structural modification and AI stress test |
| Week 15 | Final reflection | Synthesis |

<!-- In-class sessions during Weeks 11 and 15 will include structured discussion of common modeling errors and Solver diagnostics. -->

---

# Phase 1: Baseline formulation (30 points)

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

## Submission requirements

- Excel file (.xlsx)
- Written explanation (approximately 1 page) addressing:
  - Decision variable definitions.
  - Objective function.
  - Complete constraint structure.
  - Identification and interpretation of binding constraints.

### Phase 1 rubric (30 points)

Formulation correctness – 15  
Solver implementation and configuration – 10  
Clarity and technical precision – 5  

---

# Phase 2: Schedule quality and constraint interaction (40 points)

All Phase 1 constraints remain in force.

## Objective

Minimize total rest violations.

A rest violation occurs when a team plays on consecutive days.

## Modeling expectations

- Introduce additional binary variables to represent rest violations if necessary.
- Properly link rest variables to game variables using logically correct linear constraints.
- Preserve all previously defined constraints without weakening them.
- Analyze whether zero rest violations are feasible under the pairwise and capacity constraints.

Students should explicitly consider:

- Whether capacity limits on August 3 and August 7 induce unavoidable clustering.
- Whether pairwise lower bounds force scheduling density.
- How daily limits and pairwise requirements jointly constrain feasible spacing.

Superficial rest-counting approaches without correct logical linkage will receive reduced credit.

## Submission requirements

- Updated Excel file.
- Written explanation (1–2 pages) addressing:
  - Mathematical modeling of rest violations.
  - Feasibility of zero violations.
  - Identification of structurally binding constraints.
  - Interaction between daily capacity and pairwise bounds.
  - Observations regarding Solver behavior.

### Phase 2 rubric (40 points)

Correct modeling of rest violations – 15  
Preservation of prior constraints – 10  
Depth of structural analysis – 10  
Clarity and organization – 5  

---

# Phase 3: AI replication and diagnostic evaluation (50 points)

Students will prompt a publicly available AI system to formulate the Phase 2 model.

## Required steps

1. Include the exact prompt used.
2. Implement the AI’s formulation exactly as generated.
3. Attempt to solve the AI model before making any corrections.

Do not modify the AI model prior to diagnostic analysis.

## Analytical requirements (approximately 2 pages)

Students must evaluate:

- Appropriateness of decision variables.
- Completeness of constraint structure.
- Presence of redundant or unnecessary constraints.
- Logical errors in constraint construction.
- Feasibility or infeasibility in Solver.
- Compliance with Solver’s 200-variable limit.

Where applicable, reference specific constraint expressions and Solver output.

Statements such as “the AI model was incomplete” without supporting evidence will receive minimal credit.

### Phase 3 rubric (50 points)

Accurate implementation of AI formulation – 10  
Identification of structural deficiencies – 20  
Comparative reasoning between human and AI models – 15  
Clarity, specificity, and supporting evidence – 5  

---

# Phase 4: Structural modification and AI stress test (60 points)

Students will introduce one substantive structural modification to the model.

## Acceptable examples

- Rolling window constraint (e.g., no 3 games within any 4 consecutive days).
- Min–max fairness objective.
- Weighted multi-objective formulation.
- Asymmetric team availability constraints.
- Equity constraints on total idle days.

Merely changing numerical parameter values does not qualify as a structural modification.

## Required steps

1. Modify and solve your extended model.
2. Prompt AI to formulate the modified version.
3. Implement the AI formulation.
4. Compare structural robustness and Solver behavior.

## Analytical requirements (approximately 2 pages)

Students must explain:

- The structural modification introduced.
- Why the modification increases modeling complexity.
- How Solver behavior changes relative to earlier phases.
- Points at which AI reasoning weakens or remains robust.
- Any subtle formulation inconsistencies in the AI model.

A high-quality analysis distinguishes between cosmetic differences and genuine structural weaknesses.

### Phase 4 rubric (60 points)

Quality and rigor of structural modification – 20  
Correct extended formulation – 15  
AI stress-test evaluation – 20  
Depth of analytical insight – 5  

---

# Final reflection (20 points)

Maximum length: 1 page.

Students must address:

1. Under what conditions does an optimization model become structurally fragile?
2. Which types of constraints most significantly increase modeling complexity?
3. In what contexts is AI assistance appropriate in optimization modeling, and where is independent formulation preferable?
4. What did you learn about the relationship between formulation detail and Solver behavior?

General statements without reference to the project experience will receive reduced credit.

### Final reflection rubric (20 points)

Conceptual insight – 15  
Clarity and coherence – 5  

---

# Grading summary

| Component | Points |
|-----------|--------|
| Phase 1 | 30 |
| Phase 2 | 40 |
| Phase 3 | 50 |
| Phase 4 | 60 |
| Final reflection | 20 |
| **Total** | **200** |

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
