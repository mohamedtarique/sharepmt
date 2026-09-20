1. Are you actively considering a job change? What's prompting it?

I'm not looking to leave — I'm looking to move in a specific direction, and I'm being selective about it.

My work so far has been building the data layer end to end: API integration, extraction, cleaning, structuring and the reporting built on top. I've taken that about as far as it goes within a corporate-registry dataset. What I want next is to apply the same engineering discipline to portfolio data — holdings, exposures, performance and attribution — where the output goes directly to Investment Directors and clients, and the analytical content is as demanding as the build.

This role sits exactly at that intersection, which is why I'm in this conversation.

2. What interests you most about this role?

Breadth of data. The team spans Systematics, Fixed Income, Equities and Multi Asset. Most data roles give you one dataset and one shape of problem — here the variety across customised mandates, model portfolios, time-series and point-in-time views is where I learn fastest, and where reusable tooling pays off most.

Proximity to the client. Today I work on a product-based project where priorities reach me through Product and Sales reports — I solve problems at one remove from the person who has them. This role puts me alongside Investment Directors, Specialists and Portfolio Managers, and closer to the client requirement itself. I'd rather hear the problem first-hand, scope it properly, and build the right thing once.

The reporting line. I read up on [Associate Director's name] before applying — [one specific, verifiable accomplishment]. Pairing his depth on the investment side with what I bring on data and automation is a genuinely strong learning structure for me.

3. Automating a manual reporting / data processing task

Headline: I rebuilt our UK corporate filings workflow from a fully manual process — roughly [__] minutes of analyst touch time per company and a worst-case six-month data lag — into an automated pipeline with a 24-hour detection window.

Python
3.1 Automated data pull from the UK registry (API)

Challenge

Analysts manually checked every company in our database for new filings — most had none, so the majority of effort produced no output.
Checks ran on a cycle; a company filing just after a check wouldn't be picked up for another six months.
Stale data drove recurring client tickets.

Approach

Connected to the Companies House API via Python and ran it against our full company list.
Moved from a monthly manual query to a scheduled daily run connected directly to the database.

Business impact

New filings surfaced within 24 hours of appearing in the registry.
Analyst time redirected to companies that actually had updates — processing volume up [__]%.
Freed capacity for ad-hoc requests and new initiatives.
Client tickets on new filings down [__]%.
3.2 Data extraction from filings

Challenge

Manual copy-paste from filing PDFs into Excel — averaging ~10 minutes per filing.
Filings with 200+ shareholders were effectively unprocessable.
Power Query extraction produced inconsistent output.

Approach

Built a Python extraction pipeline using PyPDF2, Tesseract and PaddleOCR.
Added routing logic to handle native-text, scanned/non-OCR and handwritten filings.
Output delivered as a clean Excel file, ready for downstream processing.

Business impact

Extraction time cut from ~10 minutes to [__] minutes — a [__]% reduction.
Removed the shareholder-count ceiling entirely.
UK dataset coverage increased by [__]%, including filings we previously couldn't capture at all.
3.3 File conversion utility

Challenge

Analysts raised individual Adobe Acrobat licences for short-term conversion needs; licences lapsed after 90 days of inactivity, forcing repeat requests.
Online conversion tools were blocked for security and data-compliance reasons.

Approach

Built a Python converter that auto-detects the input file type and delivers the user's chosen output format.
Covers all major filing types, including multi-page TIFF.

Business impact

Adopted as the team standard for file conversion.
Licensing spend reduced by [__]%, removing a recurring administrative request cycle.
VBA
3.4 Cap table preparation (dynamic data processing)

Challenge

10–15 minutes per company spent on data cleaning and cap table construction.
No standard method across the team, causing inconsistency and timeliness issues.

Approach

Built VBA scripts to clean the extract and construct the cap table automatically.
Generates the pivot, segregates individual vs. institutional investors, runs the calculations, and auto-recalculates when an analyst makes a manual edit.

Business impact

Cleaning time cut from 10–15 minutes to ~5 minutes.
Manual calculation errors effectively eliminated.
Uniform output structure across all analysts — the control improvement that made the next stage possible.
End-to-end automation
3.5 Detection → extraction → cleaning → direct upload

Challenge

Even with structured data, analysts re-keyed it into the front end by hand — ~10 minutes per record of clicking and pasting.

Approach

Chained the components into a single flow: API detection → trigger → Jira ticket → automated extraction to Excel → VBA cleaning and segregation → direct upload to front end.
Prototype built with Power Apps, Power Automate and Lists; currently in development with the Engineering team.

Business impact

Targets full elimination of the ~10-minute manual upload per record.
Analyst role shifts from doing the work to reviewing the output.
End-to-end: [__]% of manual touch time removed across the workflow.
Other projects
3.6 AI / Copilot initiatives
Agent orchestration: multi-agent setup that researches data the way an analyst would, with tasks assigned across agents — currently in test with selected analysts.
AI optimisation: identified friction in how the division used AI for data cleaning and built a scalable solution (Python script + vision model + LLM routing) that selects the right resource per use case — reducing run time, improving output reliability, and handling complex cases on lighter models. Pending rollout.
3.7 Jira KPI reporting
Automated a weekly KPI report to each analyst, enabling individuals to plan and track their own delivery rather than discovering gaps at period end.
3.8 Jurisdictional coverage
Valuations and cap table processes across the UK, Ireland, Poland, Spain and Germany — covering the EMEA region and all deal types.
4. How would you analyse the performance of an investment portfolio?

Four steps: frame the question, measure return, decompose it into drivers, then test whether the return justified the risk — each viewed both point-in-time and as a time series.

Step 1 — Frame it. Confirm the benchmark, mandate constraints, period, currency and hedging policy, and gross vs. net of fees. Also whether returns are time-weighted (judges the manager) or money-weighted (reflects the client's actual experience).

Step 2 — Measure. Absolute return, benchmark return and excess return, then rolling 1m / 3m / 12m / 3y plus calendar years — to see whether performance is persistent or driven by one or two episodes.

Step 3 — Decompose. The question isn't did we outperform but why:

Portfolio type	Attribution lensEquity	Brinson: allocation, selection, interaction; then top/bottom contributors by contribution, so position size is reflected
Systematic	Factor attribution — value, momentum, quality, low vol, size, plus residual. Key question: did return come from intended factors or unintended exposures? (MSCI Barra)
Fixed income	Carry/income, duration, curve positioning, spread/credit, sector and rating allocation, selection, FX — grouped by key-rate duration and ratings buckets

Step 4 — Risk.

Dimension	MetricsAbsolute risk	Volatility, downside deviation, max drawdown and recovery, VaR
Relative risk	Tracking error (ex-ante vs. realised), active share, beta
Risk-adjusted	Information Ratio (primary for active mandates), Sharpe, Sortino
Consistency	Hit rate, up/down capture, rolling IR
Exposure	Factor exposure vs. target, sector/country/issuer concentration, liquidity
FI-specific	Duration and DTS vs. benchmark, spread duration, YTW, credit quality mix

Step 5 — Isolate the drivers. Look for contribution disproportionate to weight or risk budget — a position consuming 30% of tracking error but contributing 5% of return is a finding regardless of whether the period was positive. Cross-check three ways: ex-ante vs. ex-post risk, intended vs. unintended exposure, and rolling contribution to confirm whether a driver was persistent or a single event.

And practically: I'd want this as a repeatable, auditable process rather than a one-off — a consolidated pipeline pulling holdings, risk and performance data with reconciliation controls built in, feeding standard Power BI outputs and client-ready templates. Consistent across mandates, scalable as mandate count grows, and every client-facing number traceable to source.
