# Kestrel Living: Who Checks the AI's Numbers?

## An AI answer validation framework built by Pod Lyra for the 10Alytics Hackathon (Data Analytics track)

AI analytics answers sound confident even when wrong, and Kestrel Living has no reliable way to catch errors or privacy breaches before managers act. We audited the company's AI assistant, built a checker that recomputes its answers, and redesigned the Data Analyst role around validation, governance and interpretation.

## What we found
We re-computed all 15 answers in the AI log against Kestrel Living's official metric definitions and business rules.

| Verdict | Answers |
|------------|---------|
| Correct | 4 |
| Correct, with caveat | 2 |
| Misleading | 2 |
| Wrong | 5 |
| Non-compliant (privacy or consent) | 2 |

- Profit overstated by £13.3M. AI-012 reported £22,965,866.60. That is revenue. True profit is £9,616,347.60. The AI's confidence was 94%.
- Consent ignored. AI-011 recommended emailing the top 10 spenders, but only 3 of them have given marketing consent. AI-015 offered customer names and emails.
- Confidence scores are not evidence. Correct answers averaged 93, wrong answers 92.6.
- Data preparation matters. The correct answers only match after removing 45 duplicate order lines, excluding two internal test accounts, and fixing mixed dates and channel labels.

## How the solution works
1. Governed data layer: completed orders only, test accounts excluded, duplicates removed, dates and labels standardised.
2. Recompute: every AI claim is recalculated from the official definitions (Power BI measures, SQL queries and Excel formulas).
3. Verdict: PASS or FAIL, with the evidence and the difference shown.
4. Route: each verdict maps to a named human checkpoint (Analyst, Senior Analyst, Finance Director or Data Protection Lead).
5. Scales beyond the 15: a new AI claim is added as one row in a claims table and checked instantly. We tested it with a new claim (AI-016), and it was flagged straight away.

- Privacy by design: names and emails are removed before the data is loaded, so the model only uses Customer_ID.

## Screenshots: Power BI report

<img width="931" height="524" alt="1" src="https://github.com/user-attachments/assets/df19f819-a753-40df-938c-8064de2642a6" />
Page 1: every AI claim is recomputed and marked PASS or FAIL.
<img width="930" height="527" alt="2" src="https://github.com/user-attachments/assets/e88b7749-ba1f-4c6d-8523-910c0325d17b" />
Page 2: revenue bridge. Discounts, not returns, are the bigger gap between gross and net revenue.
<img width="931" height="526" alt="3" src="https://github.com/user-attachments/assets/1db562a1-1b42-415f-b358-a1aa737aa9b6" />
Page 3: consent gate. Only 3 of the top 10 spenders can be contacted.
<img width="932" height="526" alt="4" src="https://github.com/user-attachments/assets/5651b231-c96c-478c-9637-ec30e4a1ccf8" />
Page 4: category view. Lowest profit is not the same as poor performance.

## Project Deliverables

| Deliverable | File |
|------------|---------|
| AI Exposure Scorecard, Control Rules, Rules of Engagement | https://github.com/hussaindarboe63-creator/Kestrel_Living/blob/main/Kestrel_Living_AI_Validation_Workbook.xlsx |
| AI Validation Report | https://github.com/hussaindarboe63-creator/Kestrel_Living/blob/main/Kestrel_Living_AI_Validation_Report.docx |
| Role & Workflow Pack (before/after workflow, future role, reskilling plan, AI rules) | https://github.com/hussaindarboe63-creator/Kestrel_Living/blob/main/Kestrel_Living_Role_and_Workflow_Pack.docx |
| Working solution | https://github.com/hussaindarboe63-creator/Kestrel_Living/blob/main/Hackathon.pbix, SQL queries, DAX measures |
| Presentation Slides | https://github.com/hussaindarboe63-creator/Kestrel_Living/blob/main/Kestrel_Living_AI_Insights.pptx |
| Note on AI tools used | https://github.com/hussaindarboe63-creator/Kestrel_Living/blob/main/Kestrel_Living_AI_Tools_Note.docx |

## Technology Stack

### Data Analysis
- Microsoft Excel (live formulas)
- SQL

### Dashboard
- Power BI (Power Query and DAX)

### Documentation
- Microsoft PowerPoint and Word

### AI Tools Used
- Claude helped explore the data, draft the validation logic and write documents. Results were checked in Excel and Power BI. See the AI tools note for details.

## Business Impact

- About 39% of analyst hours can be automated or assisted. About 65% of that time returns as validation, governance and interpretation work, so the analyst role becomes more important, not less.
- Wrong, misleading and non-compliant answers are caught before managers act on them.
- High-impact figures and personal-data requests always go to a named human.

## Limitations
The data covers one year (2025), so trends and causation cannot be established.
Duplicate removal is a documented judgement that should be confirmed with the data owner.
Scorecard time estimates are planning assumptions, not measured benchmarks.
The checker has specific rules for the 15 logged questions plus general red-flag rules. A new type of question needs a registered metric check, otherwise it is routed to an analyst.
All case-study data is fictional.

## Next steps
Pilot the checker on live BI data.
Start 10% weekly sampling of released answers.
Keep the 15 validated answers as a regression test set whenever the AI model or prompt changes.

## Team
Pod Lyra
- A team of data analytics learners working with Excel, SQL and Power BI.
