Vilfredo Pareto (1848–1923) was an Italian economist, sociologist, and philosopher best known for his foundational contributions to the field of microeconomics and the development of the Pareto Principle.

In 1896, while studying wealth distribution in Italy, Pareto observed a curious mathematical pattern: approximately 80% of the land in Italy was owned by only 20% of the population. The observation that a minority of inputs often creates a majority of outputs, became the basis for what is now widely known as the "80/20 rule", and it applies to a surprising number of metrics. It's important to note, although it's sometimes called a "rule", in actual fact it's more of a guideline, and the numbers don't have to be exact.

In my field of software development, the 80/20 rule pops up reasonably regularly: Microsoft once famously noted that fixing the top 20% of the most-reported software bugs eliminated 80% of the errors and crashes in Windows. Additionally, a 2019 study observed that 80% of user engagement comes from just 20% of an app's features.

In a charity shop I recently picked up the book *4-hour Work Week* by Tim Ferriss. Although it's from the distant past of 2007 (well, distant past in technology terms), I figured that for £2, maybe I could gain some insight and at least get me down to a 40-hour work week. Ferriss brings up the Pareto principle again and asks the question: "which 20% of your clients bring you the most revenue?"

I wanted to see if the 80/20 rule held water at Ticketlab, so I put it to the test. It turns out that getting from a vague hunch to actionable data is surprisingly straightforward with some help from our AI overlords.

The process was structured thus:

*   **Define your key metric:** For Ticketlab, booking fees make us money, but that differs depending on size of event and how frequently the organiser hosts events. I gave Cursor the "calculate fees" formula we use on Ticketlab as the basis for our client ranking.
*   **Extract and Rank:** Cursor running against my codebase knows my database structure, so I was able to get it to create a SQL query that pulled all 472 active organisers, and ranked them by net fees for the past 12 months.
*   **Build the Curve:** I didn't actually need to plot this out, as the table had a cumulative earnings column, but it could be a fun exercise if you want to use up some of that graph paper you've got knocking about the place. With the event organisers ranked in order of earnings from booking fees, I just needed to look down the table to find where the fees first crossed the 80% threshold. It turns our that Ticketlab's 80/20 rule is actually 80/27, with 80% of revenue coming from 27% of clients. 
*   **Behavioural Segmentation:** Instead of just listing top clients, I segmented the top 125 clients by behaviour and category: looking for high-frequency slots, higher ticket prices, and regular promoters versus the occasional "big hitter", and seeing what kind of events they host. 
*   **Stress-Test the ICP:** I held our existing Ideal Customer Profile (which leaned heavily on music venues and festivals) against the data. It was a useful exercise; although our assumptions were mostly right, but they needed a bit of tweaking to match the reality of our top performers.
*   **Define Strategy:** I split the output into two lanes: protecting the absolute top tier (ranks 1–3) and aggressively seeking to reproduce the profile of ranks 4–40 as our primary acquisition target.
*   **Account for the "Why":** I noted a few caveats—these are estimates, not the final word from the Stripe ledger, and some category tags are heuristic—but the direction is clear.
*   **Schedule the Review:** I’ve set a reminder to re-run this every six months. The results could change seasonally, or other initiatives could tip the scales.

From these results we know what's working well, and our growth strategy is clear: focus on keeping hold of our best clients and lean into what works best for them to help us grow. We can also use those successes as social proof and keyword targeting in our next camnpaigns. For us that means catering for more community cinema, film nights, gigs and theatre.

Have you tried this technique? Have you found a particular metric that flips your understanding of your "vital few" on its head? Have a play with your own data and let me know what patterns you uncover.