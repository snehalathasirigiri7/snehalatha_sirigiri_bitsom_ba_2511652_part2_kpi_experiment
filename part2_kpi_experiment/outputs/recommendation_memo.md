# Recommendation Memo
## Campaign Experiment — Onboarding & Activation Decision
**To:** Product Leadership  
**From:** Snehalatha Sirigiri, Business Analyst  
**Date:** June 2025  
**Re:** Launch Decision — New Onboarding Campaign (Treatment)

---

## Executive Summary

The new onboarding and activation campaign (Treatment) produced a statistically significant improvement in the company's North Star Metric — Paid Conversion Rate — achieving a **+120.75% relative lift** over the existing experience. The result clears the statistical significance bar at 99.9% confidence. However, two guardrail metrics — Support Ticket Rate and Average Revenue per Converted User — show patterns that require attention before unrestricted full rollout.

**Recommendation:** Proceed with a **phased rollout**, starting with the Mobile and Desktop user base where conversion lift is clearest, while simultaneously addressing the support ticket surge and investigating the revenue-per-conversion dip over the next 30–45 days.

---

## North Star Metric

**Selected Metric:** Paid Conversion Rate  
(Proportion of users who transition from trial or free tier to a paid subscription within 30 days)

**Why this is the North Star:**
- It directly captures the primary business value the experiment is designed to influence
- All other funnel metrics (landing page visits, trial starts, onboarding completions) are intermediary steps toward this outcome
- Revenue growth at the company level is mathematically a function of conversion rate multiplied by user volume
- Leadership's decision question is precisely about whether more users are willing to pay — this metric answers that directly

**Risks of optimizing this metric blindly:**
- Conversion rate can be inflated by over-incentivizing sign-ups (discounts, free trials) that attract low-lifetime-value users who later churn or request refunds
- A short-window conversion rate may not reflect 90-day or annual retention
- High conversion paired with high support tickets suggests friction in the post-conversion experience, which can erode LTV even as conversion numbers rise

---

## KPI Tree Summary

The KPI tree for this experiment is organized across three primary driver categories:

**Driver 1 — Activation Funnel Quality**
Sub-drivers: Landing Page Visit Rate, Trial Start Rate, Onboarding Completion Rate. The Treatment group outperformed Control on all three, indicating the new campaign successfully moved users deeper into the activation funnel.

**Driver 2 — User Engagement Depth**
Sub-drivers: Average Engagement Score (30d), Days to Convert, Session Frequency. Treatment users showed a +10.34% higher average engagement score and converted 2.46 days faster, suggesting the campaign is capturing more genuinely interested users.

**Driver 3 — Revenue Quality & Retention**
Sub-drivers: ARPU, Revenue per Converted User, Refund Rate. ARPU showed marginal improvement (+$2.13), but revenue per converted user was significantly lower in Treatment ($770 vs $1,630 in Control). This warrants investigation into whether the Treatment is attracting lower-value plan tiers.

**Guardrail Metrics Monitored:** Refund Rate, Support Ticket Rate, Revenue per Converted User consistency, Segment-level conversion parity.

---

## Experiment Result Summary

| Metric | Control | Treatment | Change |
|---|---|---|---|
| Sample Size | 693 | 715 | +22 users |
| Landing Page Visit Rate | 63.64% | 72.59% | +8.95pp |
| Trial Start Rate | 25.11% | 29.09% | +3.98pp |
| Onboarding Completion Rate | 15.58% | 21.26% | +5.68pp |
| **Paid Conversion Rate (NSM)** | **3.18%** | **6.99%** | **+3.82pp (+121%)** |
| Avg Revenue per User | $51.75 | $53.88 | +$2.13 |
| Avg Revenue per Converted User | $1,630 | $770 | -$860 |
| Refund Rate | 0.00% | 0.42% | +0.42pp |
| Support Ticket Rate | 14.72% | 24.76% | +10.04pp |
| Avg Engagement Score | 57.03 | 62.93 | +5.90 |
| Avg Days to Convert | 8.86 | 6.40 | -2.46 days |

---

## Hypothesis Test Interpretation

A two-sample independent t-test was performed on Paid Conversion Rate with a one-tailed alternative hypothesis (Treatment > Control) at significance level alpha = 0.05.

- **t-statistic:** -3.2618 (magnitude: 3.26)
- **p-value (one-tailed):** 0.000567
- **Decision:** Reject H0

The probability of observing this conversion rate difference by chance alone (if H0 were true) is 0.057%. This is overwhelming statistical evidence of a genuine improvement. The experiment is correctly powered and the result is reliable.

---

## Guardrail Metric Analysis

### 1. Refund Rate
- Control: 0.00% | Treatment: 0.42%
- **Assessment:** The refund rate in Treatment is small in absolute terms (3 users out of 715), but the appearance of refunds where Control had none is a signal. It suggests some converted users in Treatment may have experienced unmet expectations post-conversion. Monitor closely over the next billing cycle. Does not block launch at this level.

### 2. Support Ticket Rate
- Control: 14.72% | Treatment: 24.76%
- **Assessment:** This is the most significant guardrail finding. A 10-percentage-point increase in support ticket rate — nearly a 68% relative rise — indicates that the new onboarding experience is creating confusion or unresolved issues for a meaningful portion of users. Before full rollout, the product and support teams should investigate the top ticket categories in the Treatment group. This does not invalidate the conversion lift, but it represents an operational risk and a potential churn signal.

### 3. Avg Revenue per Converted User (Revenue Quality)
- Control: $1,630 | Treatment: $770
- **Assessment:** Revenue per converted user is significantly lower in Treatment. Two hypotheses: (a) Treatment is attracting users who select lower-priced plan tiers (Basic/Free → Basic rather than Premium), or (b) shorter days-to-convert correlates with lower initial plan commitment. Segment analysis by plan type should be conducted before full rollout.

### 4. Segment-Level Conversion Parity
- No major region shows a decline in Treatment vs Control.
- Mobile users show strong conversion lift in Treatment.
- Email-sourced users showed relatively weaker lift — may be worth separate analysis before email channel rollout.

---

## Segment-Level Insights

**By Device Type:**
- Mobile users form the largest segment (864 users) and Treatment showed consistent improvement in this group.
- Desktop also showed positive response to Treatment.
- Tablet (112 users) is a small segment; results less conclusive.

**By Region:**
- All four regions (North, South, East, West) showed positive conversion trends in Treatment over Control.
- No region showed a regression — conversion parity holds across geographies.

**By Traffic Source:**
- Organic and Social traffic sources showed strong conversion improvement in Treatment.
- Email-sourced users showed smaller lift, which may indicate the new onboarding design performs better for users arriving through discovery channels vs. direct email outreach.

**By Plan Type:**
- The shift toward lower ARPC in Treatment may reflect higher Free-to-Basic conversions vs. Free-to-Premium.
- Premium plan conversion rate in Treatment vs Control is worth isolating in a follow-up analysis.

---

## Final Recommendation

**Decision: Phased Rollout — Launch to Mobile and Desktop users in all regions, with 30-day guardrail monitoring before full activation**

The statistical evidence for conversion improvement is strong and consistent across all regions and primary device types. The North Star Metric achieved a 120.75% relative lift with p < 0.001.

However, the following conditions must be addressed in parallel with rollout:

1. **Support Ticket Investigation:** The Customer Success and Product teams should pull ticket content from Treatment users and classify the root causes within two weeks of rollout.
2. **Revenue Quality Monitoring:** Track plan distribution (Free/Basic/Premium) among newly converted Treatment users weekly to confirm whether ARPC recovers as the campaign stabilizes.
3. **Refund Rate Threshold:** Set an automated alert if refund rate in the rolled-out population exceeds 1.5% at any weekly checkpoint.
4. **Email Segment:** Continue testing before extending the new experience to email-sourced traffic; results there are less certain.

---

## Risks and Limitations

- The experiment window and dates do not account for potential seasonal patterns in sign-up behavior.
- Users in the Treatment group were not tracked beyond 30 days; long-term retention and churn rates are unknown.
- The revenue-per-converted-user drop could indicate plan-tier mix shift or discounting behavior not captured in the dataset.
- Small absolute refund counts (3 users) make the refund rate estimate statistically noisy; it should be re-evaluated at scale.
- The 8 duplicate user_id rows were excluded from primary analysis; their origin should be investigated to rule out tracking issues.

---

## Recommended Next Steps

1. Launch to Mobile + Desktop segments across all regions (immediate)
2. Set up weekly monitoring dashboard for support ticket rate, refund rate, and ARPC
3. Run follow-up analysis on 90-day retention for Treatment converters vs Control converters
4. Investigate email segment performance with a targeted sub-experiment
5. Escalate support ticket root cause findings to Product by Day 14 of rollout
6. Re-evaluate full rollout decision at Day 45 based on guardrail monitoring data
