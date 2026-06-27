# Hypothesis Test Notes
## Campaign Experiment — Onboarding & Activation Analysis
**Analyst:** Snehalatha Sirigiri

---

## 1. Metric Selected for Hypothesis Testing

**Metric:** Paid Conversion Rate (proportion of users who converted to paid within 30 days)

**Why this metric was chosen:**
Paid Conversion Rate is the North Star Metric for this experiment. The core business objective is to determine whether the new onboarding campaign converts more users from free/trial status to paid subscriptions. Testing any intermediate metric (like trial start rate or landing page visits) would not directly answer the decision question that leadership needs answered. Revenue per converted user is also important, but conversion volume is the primary lever before optimization of revenue per user becomes relevant.

---

## 2. Hypotheses

### Null Hypothesis (H0)
The paid conversion rate of the Treatment group is equal to or lower than the paid conversion rate of the Control group.

> H0: p_treatment ≤ p_control

### Alternate Hypothesis (H1)
The paid conversion rate of the Treatment group is strictly greater than the paid conversion rate of the Control group.

> H1: p_treatment > p_control

---

## 3. Test Characteristics

| Parameter | Value |
|---|---|
| Test type | Two-sample independent t-test |
| Directionality | One-tailed (right-sided) |
| Significance level (alpha) | 0.05 |
| Confidence level | 95% |

**Rationale for one-tailed test:**
Leadership is specifically asking whether the Treatment improves conversion. A two-tailed test would also flag cases where Treatment performs worse, but the business decision is directional: the new campaign either earns a rollout or it does not. A one-tailed test gives us higher statistical power for detecting the specific improvement we care about.

**Rationale for t-test vs. z-test:**
Sample sizes (693 and 715) are large enough that the t-test approximates the z-test closely. The t-test is preferred as it does not assume known population variance and is robust when group sizes are unequal.

---

## 4. Test Inputs

| Input | Control | Treatment |
|---|---|---|
| Total users in group | 693 | 715 |
| Users who converted to paid | 22 | 50 |
| Conversion rate | 3.18% | 6.99% |
| Observed difference | — | +3.82 percentage points |
| Relative lift | — | +120.75% |

---

## 5. Test Output

| Statistic | Value |
|---|---|
| t-statistic | -3.2618 |
| p-value (two-tailed) | 0.001133 |
| p-value (one-tailed) | 0.000567 |
| Decision threshold (alpha) | 0.05 |
| Critical value (one-tailed, alpha=0.05) | 1.645 |

**Note on t-statistic sign:** The t-statistic is negative because the calculation was ordered as `t-test(Control, Treatment)`. The magnitude (3.2618) is what matters; the Treatment group has a higher mean, confirming the direction of the effect.

---

## 6. Decision Rule

- **If p-value (one-tailed) < 0.05:** Reject H0. Sufficient statistical evidence that Treatment improves conversion.
- **If p-value (one-tailed) >= 0.05:** Fail to reject H0. Insufficient evidence of improvement.

---

## 7. Interpretation

**Result: REJECT H0**

The one-tailed p-value of 0.000567 is far below the significance threshold of 0.05. There is statistically significant evidence that the new onboarding campaign (Treatment) increases the paid conversion rate compared to the existing experience (Control).

The Treatment group achieved a conversion rate of **6.99%** versus **3.18%** for Control — a relative lift of **+120.75%**. This magnitude of improvement is both statistically significant and practically meaningful for the business.

**However**, the hypothesis test result alone does not determine the recommendation. Guardrail metrics must also be evaluated before a launch decision is made (see recommendation memo).

---

## 8. Additional Tests Performed

### Engagement Score (t-test)
- Control mean: 57.03 | Treatment mean: 62.93
- t-statistic: -7.9445 | p-value: < 0.0001
- Result: Statistically significant positive improvement in engagement

### Revenue per User (t-test)
- Control ARPU: $51.75 | Treatment ARPU: $53.88
- t-statistic: -0.1060 | p-value: 0.916
- Result: No statistically significant difference in per-user revenue (ARPU driven primarily by non-converted users with $0 revenue)

---

## 9. Limitations

- The binary conversion metric is analyzed as a continuous variable in the t-test; a proportions z-test would be a valid alternative and would yield similar conclusions at these sample sizes.
- The experiment ran for a defined window; seasonal effects cannot be fully ruled out.
- Randomization balance was reasonable (693 vs 715) but not perfectly equal; this is accounted for by the independent-samples approach.
