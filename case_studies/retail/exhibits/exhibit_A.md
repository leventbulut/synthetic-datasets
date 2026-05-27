# Exhibit A — Internal Memo

---

**EVERGREEN RETAIL GROUP**
**OFFICE OF THE CHIEF MERCHANDISING OFFICER**

---

**TO:** Catherine Yoo (CEO); Robert Tanaka (CFO); David Park (VP, Customer Analytics)
**FROM:** Marcus Webb, Chief Merchandising Officer
**CC:** Sandra Kim (Director, Diversity & Inclusion); Anika Vasquez (Senior Data Engineer)
**DATE:** January 28
**RE:** VIP Program Overlap Analysis — Preliminary Findings

---

## Summary

At Catherine's request, my team has completed a preliminary cross-reference of the current VIP customer list (maintained by regional store managers) against the top customer lifetime value rankings generated from the consolidated CRM dataset. The results are concerning.

---

## The Overlap Problem

Our VIP program currently identifies **47,000 customers** across all four store formats. These customers receive our highest-tier personalization: early access to seasonal collections, dedicated concierge support, in-store event invitations, and handwritten correspondence from department leads. The program costs **$4.2 million annually** to operate — approximately **$89 per VIP customer per year**.

When we ranked all 800,000 customers in the CRM by `customer_lifetime_value` and isolated the top 47,000 by data-driven CLV, the overlap with the manager-curated VIP list was as follows:

| Category | Count | Share |
|---|---|---|
| On **both** lists (manager-selected AND top CLV) | 18,800 | 40.0% |
| On VIP list only (manager-selected, NOT top CLV) | 28,200 | 60.0% |
| Top CLV only (NOT on VIP list) | 28,200 | 60.0% |

**Only 40% of the names match.**

This means approximately 28,200 customers — representing some of the highest predicted lifetime values in our database — are receiving no VIP-level attention whatsoever. Simultaneously, we are spending VIP-level resources on 28,200 customers whose data-driven CLV does not place them in the top tier.

---

## Where the Discrepancies Concentrate

The mismatch is not evenly distributed across store formats:

| Store Format | VIP List Count | Overlap with Top CLV | Overlap Rate |
|---|---|---|---|
| Luxury | 8,400 | 5,880 | 70.0% |
| Premium | 14,100 | 7,050 | 50.0% |
| Standard | 16,000 | 4,480 | 28.0% |
| Discount | 8,500 | 1,390 | 16.4% |

The pattern is clear: managers at Luxury and Premium stores are reasonably good at identifying high-CLV customers through personal relationships. Managers at Standard and Discount formats are selecting VIPs based on criteria that do not correlate well with long-term value — likely visibility, friendliness, and frequency of in-person visits rather than total spend, category breadth, or online purchase behavior.

---

## Financial Implications

A back-of-envelope calculation:

- **Current VIP spend:** $4.2M / year on 47,000 customers
- **Estimated CLV of correctly identified VIPs (18,800):** Concentrated in the upper quartile of the CLV distribution
- **Estimated CLV of misidentified VIPs (28,200):** Broadly distributed, many in the middle of the CLV range
- **Missed high-CLV customers (28,200):** Receiving standard-tier service despite data indicating they are among our most valuable

If the average CLV differential between correctly and incorrectly identified VIPs is even half the spread we're seeing in the data, the misallocation could represent **$8–12 million in unrealized annual value** through suboptimal personalization targeting.

---

## My Honest Assessment

I want to be transparent: these numbers challenge a program I've championed for years. The VIP list was built on the principle that store managers — the people who interact with customers face-to-face every day — are best positioned to identify our most valuable relationships. I still believe there is truth in that principle. A data model cannot capture the loyalty that comes from a manager remembering a customer's anniversary or holding a return item for a regular.

But 40% overlap is indefensible. We are spending $4.2 million on a program that is, by the data's account, misallocating 60% of its resources.

I am requesting that David Park's analytics team develop a data-driven segmentation model to **supplement** — not replace — the manager-curated list. The goal should be a hybrid system that preserves the relational intelligence of our store teams while correcting the systematic blind spots that the data has revealed.

---

## Recommended Next Steps

1. **Data Audit:** Before we trust the CLV rankings, we need to understand the quality of the underlying data. Anika has flagged missing values, entry errors, and extreme outliers in the consolidated CRM. David's team should complete a full audit before any model is operationalized.

2. **Segmentation Model:** Build a classification model that assigns every customer to Budget, Moderate, Premium, or VIP based on behavioral and transactional data. Compare the model's VIP assignments to both the manager list and the CLV rankings.

3. **CLV Regression:** Develop a predictive model for customer lifetime value. Use the predictions to establish a data-driven threshold for VIP qualification — a minimum expected value that justifies the $89/customer investment.

4. **Ethical Review:** Sandra Kim has raised concerns about income and store-type variables in the model. I share her concern. We should discuss this at the next Customer Experience Committee meeting.

---

Marcus Webb
Chief Merchandising Officer
Evergreen Retail Group

---

*This exhibit is a fictional internal communication prepared for case discussion. All statistics referenced are directionally consistent with the case dataset available at `datasets/retail/synthetic_retail_20250901.csv`. Students should verify cited figures against the raw data.*
