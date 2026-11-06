---

id: litvis

narrative\-schemas:

- \.\./\.\./lectures/narrative\-schemas/proposal\.yml

---

@import “\.\./\.\./lectures/css/datavis\.less”

# Project Proposal

\{&#40;whoami\|\} \{\|whoami&#41;\}

\{&#40;task\|\}

You should complete this datavis project proposal by **Sunday 8th November, 5pm UK time** ensuring you have committed and pushed it to GitHub\. Successful submissions by that time will be awarded up to **5 marks** towards your coursework assessment total\.

\{\|task&#41;\}

\{&#40;questions\|\}

- How do Formula 1 drivers perform relative to their teammates, and which drivers consistently outperform them? I want to compare points earned in eligible races, race head\-to\-head results and qualifying performance across seasons\.
- How does a driver’s performance relative to their teammates change over their career? I want to examine trends by age and experience, and identify possible periods of improvement, peak performance and decline\.
- How do different performance measures change our assessment of Formula 1 drivers? I want to explore whether rankings based on race results, qualifying and consistency agree, and how the rankings change when users adjust their relative importance\.

\{\|questions&#41;\}

\{&#40;datasources\|\}

I will use the publicly accessible [Jolpica\-F1 API](https://api.jolpi.ca/ergast/f1/) and its [documentation](https://github.com/jolpica/jolpica-f1), which provide structured historical race results, qualifying results, points, driver information and constructors\. I will focus on completed seasons from 1996 to 2025\. The records can be filtered, joined and aggregated into driver–teammate comparisons using basic data shaping\. For race\-based metrics, I will include a race only when **both teammates complete it**; if either retires, the race will be excluded for both\. I will also exclude sprint results\. Qualifying comparisons will use sessions with valid results for both teammates\. These are public sporting records and present no privacy concerns\.

\{\|datasources&#41;\}

\{&#40;justification\|\}

I chose Formula 1 because championship position and total points depend heavily on the car, so they do not necessarily show how well an individual driver performed\. Comparing teammates reduces some of the machinery difference, while combining race and qualifying metrics reveals different aspects of performance\. Interactive visualisations would let users compare drivers, explore career trends and test how their conclusions change with different measures, which would be difficult to understand from tables alone\. Jolpica provides relevant, publicly available and consistently structured data requiring relatively minor cleaning for these views\. I will make clear that teammate strength, changing points systems and excluding retirements still limit the conclusions that can be drawn\.

\{\|justification&#41;\}
