# vertigo-cengiz

Task 1
Method & General Approach

I approached Task 1 by simulating the game’s player base using a cohort model.
I assumed that each variant receives 20,000 installs per day and that users remain active according to the provided retention checkpoints.

To estimate daily activity, I first converted the retention checkpoints (D1, D3, D7, D14) into a full daily retention curve. I assumed Day 0 retention is 100% and interpolated retention values between checkpoints. For longer horizons (beyond Day 14), I used an exponential decay tail to avoid unrealistic flat retention.

For each day, I calculated DAU by summing the active users coming from all previous install cohorts. After obtaining DAU, I computed revenue as the sum of ad revenue and IAP revenue.

Ad revenue was calculated using impressions per DAU and eCPM, while IAP revenue required an ARPPU assumption. Since ARPPU was not provided, I reported break-even ARPPU values to show under which conditions each variant would outperform the other.

Task 1-a — DAU after Day 15

To answer this question, I simulated daily active users for both variants over 15 days.

I calculated DAU on each day by summing the contribution of all past cohorts, where each cohort’s activity depends on its retention at that specific age. This effectively models how users accumulate in the game over time.

The comparison is driven mostly by early retention because Day-15 DAU is dominated by recent cohorts (ages 0–14). Therefore, the variant with stronger early retention produces higher DAU at this horizon.

I also plotted DAU over time to visualize how the player base grows for both variants

Task 1-b — Total Money by Day 15

I extended the DAU simulation to compute revenue from Day 1 to Day 15.

For each day:

Ad revenue = DAU × impressions per user × eCPM / 1000

IAP revenue = DAU × purchase rate × ARPPU

I then summed daily revenue to obtain cumulative revenue by Day 15.

Because ARPPU was not given, I calculated a break-even ARPPU value. This threshold indicates the ARPPU level at which both variants would generate equal total revenue.

This allowed me to compare variants without relying on a single arbitrary monetization assumption.

Task 1-c — Total Money by Day 30

To evaluate longer-term performance, I repeated the same analysis for a 30-day horizon.

Since retention data was only provided up to Day 14, I assumed an exponential decay after Day 14. I derived the decay rate from the slope between Day 7 and Day 14 retention values. This approach keeps the curve realistic and avoids assuming users suddenly stop leaving the game.

I then calculated cumulative revenue from Day 1 to Day 30 and again reported the break-even ARPPU.

This longer horizon increases the importance of late-stage retention because older cohorts contribute more significantly to total revenue.

Task 1-d — 10-Day Sale Event

In this scenario, I modeled a temporary sale starting on Day 15 that increases the purchase rate by 1 percentage point for 10 days (Day 15–24).

The sale does not affect retention or DAU, so only IAP revenue changes. I updated the purchase rate only during the event window and recomputed cumulative revenue by Day 30.

The result mainly shifts the break-even ARPPU because IAP revenue becomes more important during the event period, but the long-term player behavior remains unchanged.

Break-even ARPPU ≈ 1.99

Task 1-e — New Permanent User Source

In this scenario, starting from Day 20, installs come from two sources:

12,000 users/day from the original source

8,000 users/day from a new source

The new users follow a different retention curve defined by the provided exponential formulas. I calculated DAU by summing the activity of both sources simultaneously for each cohort.

Unlike the sale event, this change increases the number of active players every day. As a result, both ad revenue and IAP revenue grow continuously because the player base itself becomes larger.

I then computed total revenue by Day 30 under this mixed acquisition model.

Task 1-f — Final Decision

When comparing the two possible improvements, I would prioritize integrating the permanent new user source rather than running the temporary sale event.

The sale only increases purchase conversion for a limited period and creates a short-term revenue spike. Once the event ends, revenue returns to its previous level.

The new user source, however, increases the number of active players entering the game every day. Because both ad revenue and IAP revenue scale with the active user base, the effect compounds over time and continues beyond the 30-day horizon.

Therefore, the permanent acquisition source provides sustainable growth, while the sale provides only temporary monetization uplift.



TASK 2

### Data quality checks
- I started by validating the dataset: overall coverage (row/user counts and date ranges)

### Overall trends (DAU, revenue, sessions)
I analyzed daily DAU and revenue (total, IAP, ads) to understand overall game health and volatility. I also tracked session behavior over time (sessions per user-day, session duration, and duration per session) to see whether engagement grows or declines as the product matures.

### Cohort retention (D1/D3/D7)
I built install cohorts using install_date and measured retention as the share of users who were active (total_session_count > 0) on day-since-install 1, 3, and 7. This highlights whether the game is primarily losing players immediately (onboarding issue) or later (mid-game retention issue).

### First-day engagement features
To support segmentation, I created per-user first-day (D0) engagement features such as total sessions, total session duration, and match activity (starts/ends, win/loss counts). These features help explain differences in retention and monetization later in the lifecycle.

### User segmentation (based on first-day sessions)
I segmented users into Low/Mid/High engagement groups based on first-day session counts using NTILE(3). This creates simple, interpretable segments that I can compare on retention and revenue outcomes.

### Segment outcomes (retention and revenue)
After defining first-day engagement segments, I compared their D7 retention and 7-day ARPU. This shows whether early engagement is predictive of longer-term value and helps identify which cohorts to prioritize (e.g., onboarding improvements for Low segment or UA targeting for High segment).

### Monetization diagnostics
I tracked payer rate, ARPU, and ARPPU over time to understand whether revenue changes are driven by more payers, higher spend per payer, or ads. I also separated ARPU into ad ARPU and IAP ARPU to see which monetization stream is dominant.

### Platform and country insights
I analyzed revenue concentration by platform and country to identify the highest-value markets. This helps prioritize localization, UA targeting, and product optimization efforts (e.g., focusing on markets with high payer_rate or high ARPU).
