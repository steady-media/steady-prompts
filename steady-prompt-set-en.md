# Steady prompt set

Version 0.2, 5 October 2026. For test users of the Steady connector.

## What this is

Twelve questions about your membership numbers, written out as prompts. A prompt is the text you give an AI assistant such as Claude or ChatGPT. These prompts tell the assistant how to read your Steady numbers correctly. Without them, it will often give you the dashboard total where you wanted the number of people who pay.

The assistant only reads your numbers. It changes nothing in Steady.

## Before you start

Connect your publication to your assistant with the Steady connector. You find it in your Steady backend under Integrations, AI assistants: https://steady.page/de/backend/publications/default/integrations/ai_assistants

## Three ways to use this file

1. **Quick try.** Copy one prompt from Part B into a new chat. Start with "Where do I start?".
2. **With the whole file.** Attach this file to a new chat and write: "Follow the standing rules in this file and run question 1."
3. **Set up once.** Create a project in Claude or ChatGPT. Paste Part A into the project's instructions. Check that the Steady connector is switched on in that project. From then on, the short question is enough: "How's it going?"

The third way gives the best answers.

## All twelve questions

| No. | Question | When |
| --- | --- | --- |
| 1 | Where do I start? | The first time you use Steady with an AI assistant. |
| 2 | How's it going? | Once a month, as your regular check. |
| 3 | Fewer joining or more leaving? | When your paying members or your revenue stop growing. |
| 4 | When do I lose members? | Before the months in which many memberships renew. |
| 5 | Where will I be in a year? | When you want a target, or need to plan. |
| 6 | What did the campaign bring? | After a membership call, a campaign or a special offer. |
| 7 | Do they stay? | When you want to know if new members renew after their first year. |
| 8 | Is that a lot or a little? | When you want to know how your numbers compare. |
| 9 | Should I change my price? | Before you raise a price or end a discount. |
| 10 | The numbers for pros | When an accountant, a bank or a board asks for metrics. |
| 11 | The dashboard | When you want all the charts on one page, for a meeting or a yearly review. |
| 12 | The full analysis | Once a year, or before a big decision. It takes several minutes and many calls. |

## Part A: Standing rules

Paste this once into the instructions of a project. Every answer in that project then follows these rules.

```text
You help a media maker understand the membership numbers of their publication on Steady. They are a journalist, podcaster or newsletter writer, not a business analyst. Read the numbers through the Steady connector. Change nothing in Steady.

DATA RULES
1. Paying members come first. The total in the Steady dashboard also counts guests (people who read through someone else's membership and pay nothing themselves) and members who came through a bundle. Take paying members, guests and external members from total_by_type in get_key_statistics. Say "paying members", never just "members". Explain the difference to the dashboard number once.
2. The time series count all member types together. To separate paying members from guests, pull daily data for members and for revenue over the same days. On a day on which revenue rose, some joins are paying: divide the new monthly revenue by 5 euros and round. Count that many, but never more than the joins of that day and never fewer than one. A single join worth 50 euros or more a month is one package. A day with joins and no new revenue counts as guests. Use the same rule for cancellations and lost revenue. For the number of paying members on an earlier date, count back from today's number. Say once that this split is an estimate.
3. Monthly and yearly values for "new" and "lost" are net: a person who joins and leaves in the same month disappears from them. For new members and cancellations, add up daily values. Use monthly and yearly values for totals only.
4. Ask for at most 365 days of daily data in one call. Never ask for dates before the publication was created. A call with period=all returns yearly values and the creation date in period.start. A comparison with a year ago needs two calls per series.
5. Leave the current month out of every comparison, because it is not finished. Judge the last completed month.
6. The churn rate from get_churn_rate counts all member types, so it is too low for paying members. If you need the churn rate of paying members, compute it with rule 2.
7. Amounts arrive in cents. Show euros.
8. Do every calculation in code, not in your head. If two numbers contradict each other, say so in one sentence and report it with submit_feedback.
9. Say what the data cannot show: who the members are, why they leave, where they come from. Do not guess.
10. Free readers are in free_members in get_key_statistics. They signed up without paying and are not part of the dashboard total. The numbers for the last 30 days there reach into the current month.
11. Use as few calls as the question needs. Call get_churn_rate and get_trial_members only when the question is about the churn rate or about trial memberships.

HOW TO ANSWER
- First sentence: the answer, with a number and a comparison. Compare with the same month a year ago. If the publication is younger than that, compare with the month before.
- Give the direction in plain words: up, down or level.
- Then one graphic that shows this sentence.
- Then three short parts with these headings: What happened? Why? What can I do this week? Under "Why?", say what the numbers show about the cause, such as fewer new members or more cancellations. If they show no cause, say so. Under the last heading, name one action, with a number.
- End with "I can't see this in your data: ..." and one question to ask next.
- One screen of text at most.

LANGUAGE
- Answer in the language the person writes in. In German use "Du" and gender with a colon (Leser:innen).
- Write like a careful reporter: short sentences, subject, verb, number. No metaphors. No business jargon such as lever, funnel, driver, KPI, insight, user base.
- Use the correct term and explain it the first time. Examples: "churn rate (the share of paying members whose membership ended in a month)", "monthly revenue (what all memberships together bring in per month)". After that, use the term.
- With fewer than 100 paying members, talk about people before percentages: "4 of your 40 paying members".
- Say "media makers", never "creators".
- Do not praise or scold a number. Give the number and what you compare it with.

GRAPHICS
- Title: the finding as a full sentence with its number. Subtitle: what is measured, the unit, the period.
- One accent colour, #EC7B68, for the thing the title is about. Everything else grey. No legend: label lines and bars directly. Horizontal gridlines only. Bars start at zero.
- Change over time: columns for up to 13 periods, a line for more. New members against cancellations: columns up and down from one zero line. A share: 100 dots. Fewer than 30 people: one dot per person. No pie charts.
- Under the graphic, small: "Source: Steady, as of [date]", and a note if guests are included.
- If you cannot draw in this app, write a table of five rows at most. Keep the title, the subtitle and the source line.
```

## Part B: Six core questions

Each prompt also works alone, without Part A. Replace the text in [square brackets] with your own.

### 1. Where do I start?

**When:** The first time you use Steady with an AI assistant.

```text
Use the Steady connector to give me a first look at my publication, on one page.

Start with the one thing I probably do not know yet. Check this first: my Steady dashboard counts guests, who pay nothing, together with paying members. Tell me how many really pay today, and how many paid a year ago.

Then show four more findings. Each gets one sentence with a number, one small chart, and the question I should ask next:
- my monthly revenue over the last 13 completed months
- new paying members and cancellations in the last 12 completed months. Use daily data for this, because monthly values hide people who join and leave in the same month. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing.
- the calendar months in which most of my revenue started. Yearly memberships renew in the month they started, so these are my renewal months.
- my free readers, and how many of them started paying

Give no advice yet. End with the three questions that matter most for my numbers. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Use six calls to Steady at most.
```

**You get:** One page: one fact you may not know, four more findings with a chart each, and three questions to continue with.

**Ask next:** Whichever of the three questions interests you most.

### 2. How's it going?

**When:** Once a month, as your regular check.

```text
Use the Steady connector and tell me how my publication is doing.

I want to know three things: how many members really pay (my dashboard total also counts guests, who pay nothing), what I earn per month, and how both compare with the month before and with the same month a year ago. Leave out the current month, because it is not finished. Stay with these three things; other findings belong to the other questions.

Answer in this order: one sentence with the number; one chart of my monthly revenue over the last 13 completed months; what happened; why; one thing I can do this week. Then tell me what my data cannot show, and which question I should ask next. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** Paying members, monthly revenue, the direction, and one thing to do.

**Ask next:** "Fewer joining or more leaving?" if the numbers fall or stand still.

### 3. Fewer joining or more leaving?

**When:** When your paying members or your revenue stop growing.

```text
Use the Steady connector. My paying members or my revenue are not growing. Find out which of two things changed: do fewer people join, or do more people cancel?

Use daily data for members and for revenue, because monthly values hide people who join and leave in the same month. Ask for one year of daily data per call. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Compare the last 12 completed months with the 12 months before. If I have 100 or more paying members, also show it month by month.

Start with one sentence that names the side that changed, with both numbers for both periods. Draw one chart: new paying members up, cancellations down. Then name one thing I can do this week. Tell me what my data cannot show. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** Which of the two sides changed, with the numbers for this year and the year before.

**Ask next:** "When do I lose members?" if more people cancel. "What did the campaign bring?" if fewer join.

### 4. When do I lose members?

**When:** Before the months in which many memberships renew.

```text
Use the Steady connector. In which months do most of my paying members cancel, and which dates in the next 12 months matter for my revenue?

Use daily data for members and for revenue over my whole history, one year per call. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Add up the cancellations by calendar month over the last 24 completed months. For each month with many cancellations, check if a lot of revenue started in the same calendar month of an earlier year. Yearly memberships renew in the month they started, and that is when people cancel.

Also look for one membership or package that alone brings 10 percent or more of my monthly revenue. Tell me when it started and when it will probably renew.

Start with one sentence. Draw twelve columns, January to December, and a time line of the dates ahead. Then name one thing I can do four weeks before the next date. Tell me what my data cannot show. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** The months with many cancellations, the reason if the data shows one, and the dates ahead.

**Ask next:** "Where will I be in a year?"

### 5. Where will I be in a year?

**When:** When you want a target, or need to plan.

```text
Use the Steady connector. If nothing changes, how many paying members will I have in a year?

Take the last six completed months from daily data: the average number of new paying members per month, and the share of paying members who cancel per month. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Carry both forward for twelve months. Call the result a projection, not a forecast: it is a calculation and knows nothing about campaigns, price changes or seasons. Give a range. Also tell me the number at which as many people join as leave.

My target is [number] paying members in twelve months. Tell me how many new paying members I need per month for that, and how many more that is than today. If I gave no number, ask me for one.

Start with one sentence. Draw one line: the past solid, the projection dashed. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** A projection for twelve months, and how many new paying members a month your target needs.

**Ask next:** "How's it going?" again in a month, to check the number.

### 6. What did the campaign bring?

**When:** After a membership call, a campaign or a special offer.

```text
Use the Steady connector. I ran [a campaign / a membership call / an offer] from [date] to [date]. What did it bring?

Use daily data for members and for revenue from 14 days before the start to 14 days after the end. Count new paying members per day. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Compare the campaign days with the usual number per day. If I offer trial memberships, show how many trials started and how many became paying members. Trials that have not ended yet cannot have converted, so say which numbers are still open. Also show how many free readers signed up.

Start with one sentence: how many more paying members joined than in a normal period of the same length. Draw new paying members per day, with the campaign days marked. Tell me what my data cannot show, for example if these members will stay. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** What the campaign added above a normal period.

**Ask next:** "Where will I be in a year?"

## Part C: Six more questions

These are newer and less tried than Part B. Questions 7 and 8 reach the limits of the data today: the prompts say so and show the nearest thing.

### 7. Do they stay?

**When:** When you want to know if new members renew after their first year.

```text
Use the Steady connector. I want to know if my new paying members stay: of 100 who started, how many still pay after a year?

First check if the connector has a tool that follows members by the month in which they started. If it has: tell me, of 100 paying members who started in a month, how many still paid after 3, 12 and 13 months, for members who pay yearly and for members who pay monthly. Use only start months that are at least 13 months old. Compare the 12 newest of these months with the 12 before.

If the connector has no such tool: say so in two sentences and do not estimate a number. Show me this as the nearest thing: in which calendar months most of my revenue started, and in which most was lost, over my whole history. Yearly memberships renew in the month they started.

Start with one sentence. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** Today: an honest "not yet visible", plus your renewal months. Later, once Steady delivers the data: how many of 100 stay.

**Ask next:** "When do I lose members?"

### 8. Is that a lot or a little?

**When:** When you want to know how your numbers compare.

```text
Use the Steady connector. I want to know if my numbers are normal.

First check if the connector has a tool with comparison values from similar Steady publications. If it has: place my numbers next to those of publications of my size, and tell me on which number I am furthest behind.

If it has no such tool: say in one sentence that a comparison with other publications does not exist yet. Do not quote figures from other companies or from studies, because they are not comparable. Compare me with myself: for these five numbers, give the last 12 completed months and the 12 months before, and name the one that got worse the most:
- new paying members per month
- cancellations by paying members per month
- monthly revenue
- revenue per paying member
- the share of members who pay once a year (today only)

Use daily data for new members and cancellations, one year per call. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing.

Start with one sentence. Draw one chart with the five numbers. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** Today: a comparison with your own last year. Later: a comparison with similar publications.

**Ask next:** The question that fits your weakest number.

### 9. Should I change my price?

**When:** Before you raise a price or end a discount.

```text
Use the Steady connector. I am thinking about raising my price by [percent]. Do not recommend a price. Show me what I need for my decision.

Compute the threshold: if the price rises by p percent, at most 1 − 1 ÷ (1 + p) of the affected members may cancel before I earn less than today. At 20 percent that is about 17 of 100. If I named no percentage, compute it for 10, 20 and 50 percent.

Put next to it how many of 100 paying members cancel in a normal month. Take that from daily data for the last 12 completed months. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing.

Show my monthly revenue today, and after the increase if nobody cancels. The connector does not show my plans and prices, and it cannot show what an earlier price change did; say that.

Start with one sentence. Draw two bars for the revenue, and one dot per paying member with the threshold marked. Tell me what my data cannot show: how many would leave because of an increase. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon. Keep the answer to one screen.
```

**You get:** How many members may cancel before a higher price brings in less. No price recommendation.

**Ask next:** "Where will I be in a year?"

### 10. The numbers for pros

**When:** When an accountant, a bank or a board asks for metrics.

```text
Use the Steady connector and give me a table of metrics that I can pass on to an accountant, a bank or a board.

One row per metric. Columns: the last completed month, the same month a year earlier, the average of the last 12 completed months, and one sentence that explains the metric. The metrics:
- monthly revenue (MRR) and MRR times 12 (ARR)
- paying members
- new paying members and cancellations per month
- the churn rate of paying members, and next to it the churn rate that Steady reports for all member types
- average length of a membership: 1 ÷ churn rate of paying members
- revenue per paying member (ARPU)
- lifetime value: ARPU times the average length of a membership
- quick ratio: new revenue ÷ lost revenue over 12 months
- the share of members who pay once a year

Use daily data for new members and cancellations, one year per call, because monthly values are net. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Leave out the current month. Label every row as "paying members" or "all member types" and never mix the two. New revenue includes upgrades and lost revenue includes downgrades, so say that these cannot be separated.

Start with one sentence on the most important change. End with three sentences on what matters most. Give no recommendation, because this table gets passed on.
```

**You get:** One table with the usual metrics of the subscription business, each explained in one sentence.

**Ask next:** "Show me the dashboard."

### 11. The dashboard

**When:** When you want all the charts on one page, for a meeting or a yearly review.

```text
Use the Steady connector and build a dashboard of my publication on one page. If this app can make an interactive page, use that.

Above the charts: the situation in one sentence, and the three numbers behind it. Then twelve charts at most, one per row:
1. the dashboard total, split into paying members and guests
2. monthly revenue, last 36 completed months
3. new paying members and cancellations per month, last 24 months
4. paying members over time
5. the churn rate per month, labelled "all member types"
6. new paying members by calendar month
7. cancellations by calendar month
8. new paying members by weekday
9. members who pay yearly against members who pay monthly
10. revenue per paying member, last 24 months
11. trial memberships and how many became paying members, only if I have trials
12. a projection for the next 12 months if nothing changes

Use daily data for members and for revenue, one year per call. Count paying members only. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Leave out the current month.

Every chart gets a title that states its finding as a sentence with a number, and a subtitle with what is measured, the unit and the period. One accent colour, everything else grey. No legends: label lines and bars directly. Horizontal gridlines only. Under every chart a small grey source line with the date.

In the chat, write five sentences: the five titles that matter most. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon.
```

**You get:** One page with up to twelve charts. Whoever reads only the titles knows the situation.

**Ask next:** "Give me the full analysis."

### 12. The full analysis

**When:** Once a year, or before a big decision. It takes several minutes and many calls.

```text
Use the Steady connector and analyse the whole history of my publication. This takes many calls. Work in four steps, and show me a short result after each step before you go on.

Step 1, pull the data: the numbers of today; yearly values; monthly values since the start; daily data for members and for revenue for every year, one year per call. Check that the daily values add up to the totals, and tell me where they do not.

Step 2, compute: paying members and guests for every day of the history. On a day with new revenue, divide the new monthly revenue by 5 euros and round: that many joins are paying, but never more than joined on that day and never fewer than one. Do the same for cancellations with the lost monthly revenue. Joins or cancellations on a day without such revenue are guests, who pay nothing. Then monthly revenue, new paying members and cancellations per month, the churn rate of paying members, revenue per paying member, and the dates on which I reached 100, 250, 500 and 1,000 paying members.

Step 3, look for patterns: calendar months and weekdays with many joins or many cancellations; single days with unusually many joins or one large payment, with their dates; what was left of each such peak three, six and twelve months later.

Step 4, project twelve months ahead: if nothing changes; with 20 percent more new paying members; with a churn rate one percentage point lower.

Then write a memo: the diagnosis in three sentences, each with a number; ten findings at most, sorted by importance, each with a number and a chart; the decisions I have to take, each with its effect in members and in euros, and a date. If this app can make files, add a spreadsheet with the data and the calculations. Tell me what the data cannot show. Explain every technical term the first time you use it. Write short, plain sentences, without metaphors or business jargon.
```

**You get:** A memo with a diagnosis, up to ten findings and the open decisions; where the app allows it, a spreadsheet.

**Ask next:** "How's it going?" every month, to see if the decisions work.

## If an answer looks wrong

Write to support@steadyhq.com. These four things help most:

- which question you asked, and the version at the top of this file
- which assistant you used (Claude or ChatGPT)
- what you expected, and what you got
- a screenshot of the answer

Three things to keep in mind:

- The split between paying members and guests over time is an estimate. Today's numbers are exact.
- The assistant cannot see who your members are, why they leave, or where they come from.
- Graphics depend on the assistant. If it cannot draw, it writes a small table.

## Changes

- 0.2, 5 October 2026: six more questions (Part C). An overview table. Every prompt now asks for plain sentences.
- 0.1, 2 October 2026: first version for test users.
