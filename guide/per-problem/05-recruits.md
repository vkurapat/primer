> Seed spec — §17 of the Primer authoring guide. To author this tutorial, read the index `../../CLAUDE.md`, the shared rules in `../authoring.md` + `../exercise-list.md`, and this file.

### 05 — Recruits  *(Position 1, Easy predictive)*

- **Type:** example
- **Renderings:** chapter ✓ · tutorial ✓ · class exercise — (an earlier class exercise was built and then retired in July 2026; per current policy, problems with a built chapter and tutorial do not get one)
- **"Imagine":** You are in charge of ordering uniforms for next year's Marine Corps bootcamp recruits.
- **Dataset:** `recruits` (`primer.tutorials`) — a 50-row teaching cut of NHANES, 40 male and 10 female young adults aged 18–27, columns `height`, `sex`, `age`. Built by `data-raw/recruits.R`; documented in `R/recruits.R`. The 40/10 split is deliberate so the two group means have visibly different standard errors — a feature the Temperance section asks students to notice and explain.
- **Outcome:** `height` (continuous, cm)
- **Treatment / Key covariate:** `sex` (Male/Female)
- **Quantity of Interest (QoI):** What is the average height of male and female USMC recruits?
- **Model:** Linear regression, one categorical predictor
- **Causal / Predictive:** Predictive
- **Student project:** `recruits`
- **Data prep:** none in the tutorial — the `recruits` tibble is already filtered and sliced. Setup chunk uses `recruits` directly (no intermediate `x`).
- **Final model:** `linear_reg() |> set_engine("lm") |> fit(height ~ sex, data = recruits)` → `fit_recruits`
- **DGM (Courage):** Show the fitted DGM and its expected value as two separate displayed equations, DGM first, in both the chapter's and the tutorial's Courage section (the tutorial shows them again in its Summary):
  1. **Fitted DGM, with ε included:** $\text{height} = 165.9 + 8.9 \cdot \text{sexMale} + \epsilon, \quad \epsilon \sim N(0, 41.0)$. Here 41.0 is the estimated error *variance* (residual SD ≈ 6.4 cm). Say in the prose that both the coefficients and the error variance have been replaced by their estimates, and label *this* equation "our fitted data generating mechanism."
  2. **Expected value, with ε = 0:** $\widehat{\text{height}} = 165.9 + 8.9 \cdot \text{sexMale}$. Introduce it as what you get by setting ε to its expected value of zero, because most questions want a single number rather than a distribution. The hat marks an estimated expected value, not the mechanism: the randomness is set aside, not deleted.

  Don't use the older form that showed only the hatted equation with "residuals drawn from N(0, 41.0)" as a side note. It made the expected value look like the DGM. See `dgm.md` §18.1 (and §18.3 for the parallel in non-linear families).
- **Preceptor Table:** Unit (Young Adult) | Outcome (Height cm) | Covariate (Sex)
- **Population Table:** Source | Unit/Time (Young Adult, Year) | Outcome (Height cm) | Covariate (Sex)
- **Paired question (chapter only):** What is the average causal effect of sex on a recruit's height? The implied manipulation is biologically absurd --- you cannot toggle a recruit's sex --- so the chapter explicitly names the absurdity and uses it to make the predictive/causal distinction visible (per §1.2's *paired-question-required-even-when-absurd* rule).
- **Paired Preceptor Table (chapter only):** Unit (Young Adult) | Potential Outcomes (Height if Female, Height if Male) | Treatment (Sex). The two potential-outcome columns are filled with truth, with the unobservable counterfactual rendered with diagonal hatching (same convention as any causal Preceptor Table).
- **QoI-variety candidates (chapter Temperance):** the average is one question; a campaign-quality answer for the Quartermaster also wants (a) the *maximum* (the tallest recruit you need to fit), (b) the 10th and 90th *percentiles* (how many extra-small and extra-large uniforms to order), and (c) the *distribution of a sample statistic* (e.g. the height of the tallest recruit out of a specific batch of three) which requires simulation from the DGM. The chapter sketches how to get each from the same fitted DGM; the simulation step gets a paragraph but not full mechanics.

---

