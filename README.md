# FinTech-Fraud-Detection-and-Risk-Analytics
# Case Study by Priyanka Chaudhari
# ─────────────────────────────────────────────────────────────
# Live Website: https://priyankac.qzz.io/case-studies.html
# ─────────────────────────────────────────────────────────────


## PROJECT OVERVIEW

A mid-size FinTech payment processor was experiencing a rise in fraudulent
transactions with no systematic detection or risk-scoring framework in place.
Fraud losses were growing quarter-over-quarter and the Risk & Compliance team
lacked the analytical infrastructure to identify high-risk merchants, flag
suspicious customers, or quantify financial exposure by segment.

This project delivers an end-to-end fraud analytics solution — from raw
transaction data through SQL-based risk analysis to an executive Power BI
dashboard — enabling data-driven fraud control decisions.

## BUSINESS OBJECTIVES

1. Identify and quantify fraud exposure by merchant, category, geography,
   and time of day.
2. Produce a merchant risk scorecard (HIGH / MEDIUM / LOW) to guide
   rule-engine development.
3. Deliver monthly trend visibility to track fraud rate movement over time.
4. Profile high-risk customers for Customer Due Diligence (CDD) review queue.
5. Provide actionable rule recommendations to reduce fraud exposure by 40-50%.


## PROBLEM STATEMENT

Current State:
  - No centralised fraud detection framework existed.
  - Risk team reviewed transactions manually — slow, inconsistent, non-scalable.
  - No merchant-level or customer-level risk scoring.
  - No trend tracking; leadership could not see fraud rate movement month-to-month.
  - Estimated annual fraud loss: $300K–$500K with no quantified breakdown.

Desired State:
  - SQL-based analytical framework with 8+ risk queries and a merchant risk view.
  - Executive Excel workbook: KPI summary, category analysis, amount buckets,
    monthly trend.
  - Interactive Power BI dashboard with drill-through by merchant, region, and time.
  - Documented recommendations for rule-engine implementation.


## TECHNOLOGIES & SKILLS USED

  - SQL
  - Power BI
  - BRD / FRD (Business & Functional Requirements Documentation)
  - RTM (Requirements Traceability Matrix)
  - FinTech Domain Knowledge
  - UAT (User Acceptance Testing)
  - Agile Methodology


## KEY OUTCOMES

  - 18.2%   fraud rate identified (9x the industry average)
  - $1.63M  total fraud exposure quantified
  - 3 rules addressing 88% of total exposure identified
  - 40–50%  estimated exposure reduction through rule implementation


## SCOPE

In Scope:
  - Analysis of 5,000 transactions: Jan–Dec 2024
  - Fraud analysis by merchant category, state, hour-of-day, amount bucket,
    and customer
  - Merchant risk scorecard view (SQL CREATE VIEW)
  - Excel workbook: 4-tab pivot analysis with embedded charts
  - Power BI dashboard: 3 pages with interactive slicers
  - Fraud rule recommendations with estimated impact

Out of Scope:
  - Real-time transaction processing or live data feeds
  - Machine learning model development (Phase 2)
  - Integration with production payment systems
  - PCI-DSS compliance certification


## STAKEHOLDERS

  Role                       | Responsibility
  ─────────────────────────────────────────────────────────────────────
  Head of Risk & Compliance  | Project Sponsor; approve scope & deliverables
  Fraud Analytics Lead       | Use scorecard for rule-engine specifications
  Finance Director           | Review P&L fraud exposure reporting
  Product Manager            | Consume requirements for alert features
  Engineering Lead           | Implement rule-engine from recommendations
  Legal & Compliance         | Ensure FINRA / AML alignment


## FUNCTIONAL REQUIREMENTS SUMMARY

Data Layer (FR-01):
  Transaction schema includes 12 fields: transaction_id, customer_id,
  transaction_date, transaction_time, merchant_name, merchant_category,
  transaction_amount, state, hour_of_day, is_fraud, fraud_reason, status.
  Data validation rules enforce: positive amounts, binary fraud flags (0/1),
  valid hour integers (0-23), approved status values, and valid date formats.

SQL Analysis (FR-SQL-01 to FR-SQL-09):
  FR-SQL-01 | KPI Overview        — Total txns, fraud count, rate %, exposure,
                                     and volume in a single summary row
  FR-SQL-02 | Category Analysis   — Fraud rate and exposure grouped by merchant
                                     category, ranked by fraud rate descending
  FR-SQL-03 | Time-of-Day         — Top 10 highest-risk hours ranked by fraud rate,
                                     including total txns and avg amount
  FR-SQL-04 | State Risk Ranking  — Fraud exposure and rate by US state
  FR-SQL-05 | Amount Buckets      — Fraud rate across 5 tiers: <$50, $50-200,
                                     $200-500, $500-1K, >$1K
  FR-SQL-06 | Customer Profiling  — Top 10 customers by fraud exposure for CDD queue
  FR-SQL-07 | Monthly Trend       — Fraud rate and monthly loss across all 12 months
  FR-SQL-08 | Fraud Reason        — Count and exposure by fraud_reason category
  FR-SQL-09 | Merchant Scorecard  — CREATE VIEW v_merchant_risk_scorecard classifying
                                     merchants HIGH (>40%), MEDIUM (>20%), LOW (<=20%)

## USER STORIES SUMMARY

EPIC 1 — Fraud Exposure Quantification

  US-01 | Fraud KPI Overview  [Priority: High | Sprint 1 | 3 pts]
    As a Risk Analyst, I want a single-view KPI summary of total transactions,
    fraud count, fraud rate %, and total exposure so that I can communicate
    fraud impact to leadership in one slide.
    Key criteria: returns 5 KPI fields in one row; fraud rate rounded to 2dp;
    results render in <5 seconds; values match Excel within 0.1%.

  US-02 | Merchant Category Risk Ranking  [Priority: High | Sprint 1 | 3 pts]
    As a Fraud Analyst, I want to rank merchant categories by fraud rate and
    exposure so that I can prioritise which categories need immediate controls.
    Key criteria: all distinct categories returned with 5 metrics; ordered by
    fraud_rate_pct desc; risk tiers applied: HIGH >40%, MEDIUM >20%, LOW <=20%;
    Excel chart matches SQL output.

  US-03 | Time-of-Day Fraud Pattern  [Priority: High | Sprint 1 | 2 pts]
    As a Risk Analyst, I want to identify which hours have the highest fraud
    rate so that I can define time-based transaction velocity rules.
    Key criteria: top 10 hours with fraud_rate_pct, total_txns, avg_amount;
    hours in 24-hr integer format; Power BI column chart included; hours >30%
    highlighted.

EPIC 2 — Risk Scoring

  US-04 | Merchant Risk Scorecard View  [Priority: High | Sprint 2 | 5 pts]
    As a Product Manager, I want a reusable merchant risk scorecard database
    view so that Engineering can query it directly when building the fraud rule
    engine.
    Key criteria: CREATE VIEW executes in SQLite and PostgreSQL without errors;
    returns 7 fields including risk_tier; no NULLs in risk_tier; supports
    downstream WHERE/ORDER BY filters; documented with inline SQL comments.

  US-05 | High-Risk Customer Queue  [Priority: Medium | Sprint 2 | 2 pts]
    As a Compliance Officer, I want a list of the top 10 customers by fraud
    exposure so that I can initiate Customer Due Diligence reviews in line with
    AML obligations.
    Key criteria: exactly 10 customers with 5 metrics; only is_fraud=1 records
    included; ordered by fraud_exposure desc; exportable to CSV.

EPIC 3 — Reporting & Dashboard

  US-06 | Monthly Fraud Trend Report  [Priority: Medium | Sprint 2 | 3 pts]
    As a Finance Director, I want monthly fraud rate and loss trends across the
    full year so that I can track the impact of controls implemented during the
    period.
    Key criteria: all 12 months of 2024 returned; no missing months; Excel
    column chart with month on X-axis; Power BI line chart reflects same trend.

  US-07 | Interactive Power BI Dashboard  [Priority: High | Sprint 3 | 8 pts]
    As a Risk Team Lead, I want an interactive dashboard filterable by merchant
    category, state, and date range so that I can investigate fraud patterns
    without writing SQL.
    Key criteria: 3-page dashboard; all slicers cross-filter all visuals on the
    same page; KPI cards update dynamically; accessible via shareable URL;
    mobile layout configured for Page 1.


## REQUIREMENTS TRACEABILITY (RTM SUMMARY)

  BRD Ref | Business Objective                           | Status
  ─────────────────────────────────────────────────────────────────
  BO-01   | Fraud exposure by merchant/category/geo/time | Complete
  BO-02   | Merchant risk scorecard                      | Complete
  BO-03   | Monthly trend visibility                     | Complete
  BO-04   | High-risk customer profiling for CDD         | Complete
  BO-05   | Rule recommendations + full BA docs suite    | Complete


## ABOUT THE AUTHOR

  Priyanka Chaudhari — Business Analyst
  Portfolio   : https://priyankac.qzz.io/index.html
  Resume      : https://priyankac.qzz.io/resume.html
  Case Studies: https://priyankac.qzz.io/case-studies.html
