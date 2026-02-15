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
