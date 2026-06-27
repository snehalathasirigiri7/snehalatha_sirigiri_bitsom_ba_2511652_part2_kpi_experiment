# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

**Analyst:** Snehalatha Sirigiri  
**Submission Type:** GitHub Repository  
**Repository Name:** `snehalatha_sirigiri_part2_kpi_experiment`

---

## Business Context

A subscription-based digital product company ran a controlled experiment to evaluate a new onboarding and activation campaign. Users were randomly split into two groups:

- **Control Group:** Experienced the existing onboarding flow
- **Treatment Group:** Experienced the newly designed onboarding and activation campaign

Leadership needs a data-backed answer to one question: should the new campaign be launched to all users?

**Key stakeholders affected:** Product team, Marketing, Customer Success, and Revenue leadership.  
**Primary risk to monitor:** Supporting metrics such as refund rate and support ticket rate must not deteriorate while conversion improves.

---

## Dataset Description

**File:** `data/campaign_experiment_data.xlsx`  
**Total Records:** 1,408 users  
**Columns (16 total):**

| Column | Type | Description |
|---|---|---|
| user_id | String | Unique user identifier |
| signup_date | Date | Date user signed up |
| experiment_group | String | Control or Treatment |
| region | String | North, South, East, West |
| device_type | String | Mobile, Desktop, Tablet |
| traffic_source | String | Organic, Paid Search, Social, Referral, Email |
| plan_type | String | Free, Basic, Premium |
| visited_landing_page | Binary | 1 = visited, 0 = did not |
| started_trial | Binary | 1 = trial started |
| completed_onboarding | Binary | 1 = onboarding completed |
| converted_to_paid | Binary | 1 = converted to paid (North Star) |
| revenue_30d | Float | Revenue generated in 30 days |
| support_tickets_30d | Integer | Support tickets raised |
| refund_requested | Binary | 1 = refund requested |
| days_to_convert | Float | Days elapsed before conversion (null if no conversion) |
| engagement_score | Float | Engagement score in 30 days (0–100) |

---

## North Star Metric

**Selected: Paid Conversion Rate**

The paid conversion rate measures the proportion of users who transition from a free or trial state to a paying subscription within 30 days of signing up. This metric was chosen as the North Star because:

1. It directly captures whether the campaign achieves its commercial goal
2. All funnel steps (landing page visits, trial starts, onboarding completions) are drivers toward this outcome
3. Revenue growth is a linear function of conversion volume multiplied by revenue per user
4. This is the single metric that most directly answers leadership's decision question

**What could go wrong if optimized blindly:** High conversion rate could co-occur with low-value plan selection, high refund rates, and elevated support burden — all of which erode long-term business value despite short-term conversion gains. This is why guardrail metrics must be evaluated in parallel.

---

## KPI Tree Summary

The KPI tree (located at `outputs/kpi_tree.png`) organizes success metrics into three levels:

**North Star:** Paid Conversion Rate

**Primary Drivers:**
1. Activation Funnel Quality → Landing Page Visit Rate, Trial Start Rate, Onboarding Completion Rate
2. User Engagement Depth → Avg Engagement Score, Days to Convert, Session Frequency
3. Revenue Quality & Retention → ARPU, Revenue per Converted User, Refund Rate

**Guardrail Metrics:**
- Refund Rate (must remain below 2%)
- Support Ticket Rate (must not exceed 20% without investigation)
- Revenue per Converted User consistency (within ±15% of Control)
- Segment-level conversion parity (no regional or device subgroup should decline)

---

## Experiment Analysis Approach

### Data Cleaning Steps

1. **Missing values:** `device_type` (18 nulls) and `traffic_source` (24 nulls) were retained and labeled as 'Unknown' for segment analysis. `engagement_score` nulls (14) were excluded from averages. `days_to_convert` nulls (1,336) are expected — only the 72 users who converted have a value for this field.
2. **Duplicate user IDs:** 8 duplicate rows were identified. The first occurrence per user_id was retained for analysis.
3. **Binary column validation:** All binary fields (`visited_landing_page`, `started_trial`, `completed_onboarding`, `converted_to_paid`, `refund_requested`) were confirmed to contain only 0 or 1 values.
4. **Revenue outliers:** The maximum revenue observation was $8,610.72 (a single high-value user). This was retained as a legitimate premium subscription revenue figure, not an error.
5. **Group balance:** Control group had 693 users and Treatment had 715 — a minor imbalance of 22 users (~3.2%), which is acceptable for A/B analysis using independent-samples methods.

### Metrics Computed

All required metrics were computed for both Control and Treatment groups, including user count, all visit/trial/onboarding/conversion rates, ARPU, ARPC, refund rate, support ticket rate, average engagement score, and average days to convert. Full results are in `outputs/experiment_summary.xlsx`.

### Segment Analysis

Conversion rate, trial start rate, average engagement, and average revenue per user were segmented across:
- Region (North, South, East, West)
- Device Type (Mobile, Desktop, Tablet)
- Traffic Source (Organic, Paid Search, Social, Referral, Email)
- Plan Type (Free, Basic, Premium)

---

## Hypothesis Test Summary

**Test:** Two-sample independent t-test  
**Metric tested:** Paid Conversion Rate  
**Hypothesis direction:** One-tailed (Treatment > Control)  
**Significance level:** 0.05

| Statistic | Value |
|---|---|
| t-statistic | -3.2618 |
| p-value (two-tailed) | 0.001133 |
| p-value (one-tailed) | 0.000567 |
| Decision | Reject H0 |

The conversion rate difference is statistically significant at the 99.9% confidence level.

---

## Guardrail Metrics Considered

| Metric | Control | Treatment | Risk Level |
|---|---|---|---|
| Refund Rate | 0.00% | 0.42% | Low — Small absolute count, monitor at scale |
| Support Ticket Rate | 14.72% | 24.76% | High — Requires root cause investigation before full rollout |
| Revenue per Converted User | $1,630 | $770 | Medium — Investigate plan-tier distribution shift |
| Segment Parity | Baseline | No region declined | Low — All regions responded positively |

---

## Final Recommendation

**Phased Rollout — Launch to Mobile and Desktop segments in all regions, with 30-day guardrail monitoring period before activating full rollout.**

The North Star Metric shows a definitive +120.75% relative lift in conversion rate. The statistical evidence is strong. However, the 68% increase in support ticket rate and the 52.7% lower revenue per converted user create meaningful operational and revenue quality risks that must be resolved before unrestricted launch.

Detailed reasoning, risks, and next steps are in `outputs/recommendation_memo.md`.

---

## Assumptions and Limitations

- The 30-day revenue window may not reflect full subscription lifetime value; long-term churn analysis is outside this dataset's scope.
- The experiment window spans March–April 2025; seasonal effects are not accounted for.
- Randomization is assumed to have been applied correctly; this analysis does not independently validate the randomization mechanism.
- Revenue per converted user interpretation assumes the lower value reflects plan mix, not pricing anomalies.

---

## Repository Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx
│   └── hypothesis_test_notes.md
├── outputs/
│   ├── kpi_tree.png
│   ├── experiment_summary.xlsx
│   └── recommendation_memo.md
├── screenshots/
│   ├── summary_metrics.png
│   ├── hypothesis_test_output.png
│   └── kpi_tree_preview.png
└── README.md
```

---

## Screenshots Included

| Screenshot | Description |
|---|---|
| `screenshots/summary_metrics.png` | Control vs Treatment comparison table for all core metrics |
| `screenshots/hypothesis_test_output.png` | Full hypothesis test inputs, outputs, and decision |
| `screenshots/kpi_tree_preview.png` | KPI tree visual showing North Star, drivers, sub-drivers, and guardrails |
