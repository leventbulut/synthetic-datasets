# Exhibit A — Internal Email

---

**FROM:** Diane Kowalski, Chief Marketing Officer
**TO:** Derek Holt (CEO); Simone Weiss (CFO); Maya Chen (VP, Customer Strategy)
**CC:** Jordan Blake (Director, Customer Retention); Priya Sharma (Lead Data Engineer)
**DATE:** October 4, 2024
**SUBJECT:** Customer Attrition — What I'm Seeing and What Worries Me

---

Team,

I want to flag something before Monday's planning session. I've been reviewing the consolidated CRM data that Priya's team delivered last month, and the picture isn't good. I'm calling it internally the "quiet exodus" because what's striking is the *absence* of signal — no spike in complaints, no viral social media incidents, no product recalls. Just a steady, silent bleed.

**Here's what the data shows:**

We now have a unified view of 600,000 customer records across 29 data fields. The churn risk classifications — which, I should note, were inherited from three different legacy systems with three different scoring methodologies — break down as follows:

| Churn Risk Level | Customers | Share of Base |
|---|---|---|
| High (2) | 250,251 | 41.7% |
| Medium (1) | 142,134 | 23.7% |
| Low (0) | 207,615 | 34.6% |

Read that again: **41.7% of our customer base is flagged as high churn risk.** Even if the legacy classifications are only directionally correct, that is an extraordinary number heading into our most important selling season.

**The lifetime value question:**

The average customer lifetime value in this dataset is $904, but the median is $816 — which tells me we have a long tail of high-value customers pulling the average up. The standard deviation is $401. That spread is enormous. It means we have customers worth $1,300+ sitting next to customers who may never recoup their acquisition cost. If we're losing disproportionately from the high end, the revenue impact is far worse than topline churn rates suggest.

**What's happening in the loyalty tiers:**

| Tier | Customers |
|---|---|
| Silver | 152,200 |
| Gold | 142,587 |
| Bronze | 127,479 |
| Platinum | 103,239 |
| Diamond | 74,495 |

Diamond — our highest-value, most engaged segment — is also our smallest at ~74.5K members. I don't yet have a cross-tabulation of churn risk by loyalty tier (Maya, can your team prioritize this?), but if the exodus is hitting Diamond and Platinum disproportionately, we have a much bigger problem than the aggregate numbers suggest.

**My concern about the data itself:**

I want to be honest: I don't fully trust these numbers yet. Priya has warned us that the three-system consolidation may have introduced inconsistencies. The total dataset has about 17,998 missing values — that's roughly 0.10% of all data cells, which sounds small, but I don't know where those gaps are concentrated. If critical fields like engagement metrics or satisfaction scores have systematic holes, any model we build on this foundation could be unreliable at best and misleading at worst.

**Satisfaction is a red flag:**

The average satisfaction score across the base is 5.50 on a 10-point scale. Five-point-five. That's not angry. That's not happy. That's *indifferent*. And in my experience, indifference is harder to fix than dissatisfaction. An unhappy customer will tell you what's wrong. An indifferent customer just opens a competitor's app.

**What I'm recommending:**

Before we allocate another dollar to acquisition, we need to understand retention. Maya's team should be resourced to build two things:

1. A **churn early-warning model** that can identify at-risk customers before Black Friday (classification against `churn_risk`)
2. A **CLV estimation model** that gives Simone's team defensible numbers for the acquisition budget (regression on `customer_lifetime_value`)

Both models need to be built on this dataset, which means we need to get serious about data quality *first*. I'd rather delay by a week and build on solid ground than rush and present the board with predictions we can't defend.

One more thing — and I'll bring this up on Monday — the demographic dimensions in this data make me nervous from a targeting perspective. I'll let Maya speak to the specifics, but we need to think carefully about how we use whatever the models tell us. Personalization is our brand promise. Profiling is a PR crisis.

Let's discuss Monday.

— Diane

---

*This exhibit is a fictional internal communication prepared for case discussion. All statistics referenced are drawn from the case dataset available at `datasets/marketing/synthetic_marketing_20250901.csv`. Students should verify cited figures against the raw data.*
