### AI's Interpretation and highlighting
1. Across the dataset, Sweetener D shows the sharpest net increase from first to last observation at 23.83%, followed by Staple A at 19.31%, Oil B at 17.45%, and Pulse C at 6.75%. [GREEN]
2. In the unfiltered dataset, Sweetener D has a mean price of 576.81 compared to a median of 167.75, making the mean more than 3.4 times higher than the median. [GREEN]
3. Once flagged outliers are removed (price_flag == 'ok'), the mean price of Sweetener D drops dramatically from 576.81 to 167.15—a decrease of 409.66 units—while its median barely moves from 167.75 to 167.50.[GREEN]
4. Similarly, removing flagged values brings Staple A's mean down from 160.89 to 111.39, whereas its median stays completely unchanged at 112.50. [GREEN]
5. By contrast, Oil B and Pulse C show identical means and medians before and after filtering (316.18 and 324.00 for Oil B; 205.91 and 206.00 for Pulse C), indicating that neither item had any rows flagged as outliers.[AMBER]
6. The massive upward skew in the raw means for Sweetener D and Staple A was likely caused by data-entry typos (such as misplaced decimal points) or temporary retail price gouging during peak holiday demand. [AMBER]
7. Because Sweetener D has the highest first-to-last percentage increase (23.83%), consumers spent more total money on Sweetener D than on any other staple in the basket. [RED]
8. Overall, reporting the median rather than the unfiltered mean prevents extreme price spikes from distorting the typical cost of Staple A and Sweetener D. [AMBER]
### Audit Table

| Claim | Colour | How you checked | Accepted or rejected |
| :--- | :--- | :--- | :--- |
| 1. Sweetener D rose 23.83%, Staple A 19.31%, Oil B 17.45%, Pulse C 6.75%. | Green | Matched against my `pct_change` output in `2_work.ipynb`. | Accepted |
| 2. Sweetener D raw mean (576.81) is >3.4x higher than median (167.75). | Green | Recomputed `576.81 / 167.75 = 3.44` in `2_work.ipynb`. | Accepted |
| 3. Filtering outliers drops Sweetener D mean by 409.66; median moves 0.25. | Green | Recomputed `576.81 - 167.15 = 409.66` and `167.75 - 167.50 = 0.25` in `2_work.ipynb`. | Accepted |
| 4. Filtering outliers reduces the mean of staple A down to 111.39 while median stays same at 112.5| Green|Matched against with outliers(default) vs nooutliers table| Accepted |
| 5.Oil B and Pulse C show identical means and median before and after filtering. | Amber | The second half of the sentence after the numbers is an explanation or a causal claim| Accepted |
| 6. Upward skew in the price means of Sweetener D and Staple A was likely caused by data entry typos or due to price gouging during peak holiday demand. | Amber | claim contains no recomputable variables and the term "likely" pushes it into an explanation | Rejected |
|7. Due to Sweetener D pct being highest, it means consumers spent the most on it. | RED | Consumer demand is a factor outside our dataframe. | Rejected |
|8. Reporting median rather than the unfiltered mean prevents extreme price spikes from distorting the cost of Staple A and Sweetener D. | Amber | contains no computable variables and is very clearly an explanation | Accepted |

### Confused Classmate Transcript
**AI (Confused Classmate):** Hey, thanks for helping me look over this Prices Desk data! Honestly though, I don't get why we're even bothering with the median when settling the neighbours' argument. The **mean** uses every single price in the spreadsheet, so isn't the mean *always* the most accurate, typical price? **But why** would we ever ignore data points by using the median instead?

**Me:** An outlier value may lead to inaccurate data representation

**AI (Confused Classmate):** Okay, an outlier value can distort things, I've heard that term before—**but why** does just one or two outlier prices ruin the mean if all the other normal prices are still in there? Shouldn't all the normal days outweigh one weird day? And why doesn't that same outlier ruin the median too?

**Me:** Not mathematically, if all prices are in 3 digits but one single row contains a large value in 4 digits like 9999, it will cause significant distortions, especially if there are just 95 entries.

**AI (Confused Classmate):** Oh, that 9999 example makes way more sense! Seeing how one 4-digit typo gets divided across only 95 rows explains why the mean shoots up into a price nobody ever actually paid. **But why** doesn't the **median** shoot up when that 9999 row is sitting in those 95 entries? Doesn't the median still have to count that row too?

**Me:** No the median will not shoot up, since median is calculated when data is arranged in ascending order it will make the center of that data remain stable

**AI (Confused Classmate):** Oh, I finally get it now! Because the median sorts all 95 prices in ascending order and simply picks the middle position (the 48th entry), that `9999` value just sits quietly at the very end of the list without changing which price is in the center. That makes complete sense why the mean isn't always the "typical" price when there are extreme spikes or typos!

### Reflection:
When explaining the gap between the raw and filtered mean for Sweetener D, I attributed it to a "likely massive outlier price," even though the spreadsheet only records numbers and cannot prove how extreme values occurred.
Second, under my E: section, l speculated about why the two neighbours were arguing based on general statistics habits, which goes outside what the price table can show. Finally, under C:, I claimed that any change in the median will directly alter the mean, which overgeneralizes a mathematical relationship that does not hold in every case. Adjusting these claims to stick strictly to the recorded prices and specific dataset values would make the note safer for Ms.Noor to publish.