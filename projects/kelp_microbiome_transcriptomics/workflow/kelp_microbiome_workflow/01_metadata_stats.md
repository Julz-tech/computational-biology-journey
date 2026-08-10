# Choice of plots
* Determined by **type of variable** and **questions we're asking**
* Questions to ask:
	* How many variables are involved?
	* What type of variables are they? (continuous or categorical)
	* What question do we want to answer?
		* Distribution
		* Comparison
		* Relationship
		* Composition
	

| Question                                                      | Variables Involved           | Standard plot                     | Example from this project                                                                                        |
| ------------------------------------------------------------- | ---------------------------- | --------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Distribution of one continuous variable                       | 1 continuous                 | Histogram (or density plot)       | Shape of initial_length_bl overall (how initial_length_bl is distributed among the kelp regardless of treatment) |
| Compare one continuous variable across categories             | 1 continuous + 1 categorical | Box plot (or violin plot)         | Blade length by treatment group                                                                                  |
| Relationship between two continuous variables                 | 2 continuous                 | Scatter plot                      | Blade length vs. growth rate                                                                                     |
| Relationship between two continuous variables, split by group | 2 continuous + 1 categorical | Scatter plot with hue=/col=       | Blade length vs. growth rate, colored by temperature                                                             |
| Counts/frequency of categoriesv                               | 1 categorical                | Bar plot                          | Number of kelp per treatment group                                                                               |
| Change over time                                              | 1 continuous + time          | Line plot                         | Blade length across t1→t2→t3→t4 for the same individuals                                                         |
| Composition / proportion of a whole                           | categorical parts of a whole | Stacked bar or pie (rarely ideal) | Proportion died vs. survived per treatment                                                                       |
## Reading a multi-color scatter plot
* Has 5 dimensions of info:
	* x position
	* y position
	* Color
	* Shape
	* Regression line
* Need to go through the layers in order
* We will use this example:
![[Pasted image 20260806095505.png]]
* **Step 1: Name every visual channel and what it represents**
	* x axis = initial blade length (continuous)
	* y axis = t1 to t2 growth rate (continuous)
	* Color = temperature (10/14/18°C)
	* Marker shape = surface (● natural, ✕ disrupted)
	* Black line = a fitted trend, not raw data
	* Therefore, the plot answers questions at multiple levels:
		* By temperature alone
		* By surface alone
		* By temperature and surface combined
	* **Phrase:** This plot has initial blade length on the x axis, growth rate at t1 and t2 on the y axis and displays both temperature as color and surface as shapes
* **Step 2: Read the overall trend first, ignoring every group**
	* Look at the trend line only
	* This answers - Is there any relationship?
	* Here, the line rises from left to right, indicating positive association
	* **Phrase:** At a glance, there appears to be a positive association between initial blade length and growth rate at t1 and t2
* **Step 3: Understand what the gray band means**
	* The shaded region is a confidence band around the regression line's estimate
	* It reflects uncertainty in where the true average line sits, not the spread of the individual data points around the line
	* The band seems to widen at the edges (low and high blade lengths) reflects that there are fewer data points there, hence the line position is less certain in these regions
	* **Phrase:** The shaded band reflects uncertainty in the fitted trend within the edges since we have fewer data points but is more confident in the middle due to more data points
* **Step 4: Assess linearity visually, don't just declare it**
	* Does the line stay "close" to the data points for the entire length of the x-axis, or does it only fit well in the middle and drift away from the dots at the ends?
		* If a single straight line looks like a decent fit _everywhere_ (left side, middle, right side) → roughly linear
		- If the data points clearly hug the bottom, then swoop upward steeply, then flatten out at the top (like a rainbow or an "S" shape) → not linear, because no single straight line could hug that shape from end to end
		![[Pasted image 20260806114412.png]]
	* **Phrase:** The relationship appears approximately linear across the observed range, with no obvious curvature
* **Step 5: Bring in ONE encoding at a time - color first**
	* scan the whole x-axis and ask whether the color groups maintain a consistent vertical offset from each other across the _entire_ range, not just at one spot
	* **Question**: 
		* Do blue (10°C), orange (14°C), and green (18°C) points consistently occupy the same _vertical bands_ above/below each other? 
		* This tells us whether temperature shifts growth rate _independent of_ blade length
		* If the answer stays the same as you slide all the way across, that's a real, consistent group difference
		* If the answer flips partway through (green is below blue on the left, but above blue on the right), that's not a consistent effect (this indicates an **interaction**) 
	* **Phrase:** Holding blade length roughly constant, growth rate at 10°C tends to sit lower than growth rates at 14 and 18°C for natural surface kelp, while growth rate at 18°C tends to sit lower than at 14°C and 10°C for disrupted kelp 
* **Step 6: Bring in the second encoding - shape**
	* Isolate shape only, ignoring color
	* Do circles (natural) sit consistently above/below x's (disrupted)?
	* **Phrase:** Natural surface kelp tend to sit above disrupted kelp at similar x values (natural surface kelp tend to have a higher growth rate)
* **Step 7: Combine both encodings**
	* Look at color and shape _together_
	* e.g., "green x's" (18°C disrupted) versus "green dots" (18°C natural) specifically, versus "blue x's" (10°C disrupted) versus "blue dots" (10°C natural)
	* This is where we actually see whether the surface effect _depends on_ temperature 
	* **Phrase:** At 10°C, natural surface kelp appears to have a lower growth rate, compared to disrupted kelp. This pattern, however isn't consistent across temperatures, with natural surface kelp appearing to have a higher growth rate than disrupted kelp at higher temperatures (14 and 18°C)
* **Step 8: Outliers - flag but don't let them drive the story**
	* Note extreme points (e.g., the two points near 2.0-2.25 cm/day growth) explicitly
	* Describe them as individual observations, not as evidence of a group-level pattern
	* **Phrase:** Two individual growth rates, near 2.0-2.25 cm/day, stand out as unusually high, both in natural surface kelp, at 10 and 18°C
* **Step 9: State the scope and limits explicitly**
	* Close every visual read with an honest scope statement 
	* **Phrases:**
		* This is a visual/descriptive pattern only; it has not yet been statistically tested
		* This plot suggests there is an overall linear positive relationship between initial blade length and growth rate at t1 and t2, which is also temperature and surface dependent and can be evaluated by a 
		* Correlation visible here does not establish which variable is driving the other
	

# Statistical tests/models and how to pick one
* **The right test is determined by:**
	1.  what type each variable is
	2. What question shape is being asked
* **Step 1: Classify the outcome (dependent variable)**
	* For **continuous variables** like growth rate, **regression-based tests** are used
	* For **categorical variables** like survival, we can use **logistic regression or chi square tests**
	* For count e.g., number of events, we use **Poisson-type models**
* **Step 2: Classify predictors**
	* **Continuous predictor** e.g., blade length → **correlation** or **regression**
	* **Categorical predictor** e.g., temperature groups, surface → **group-comparison tests** (t-test, ANOVA) 
	* **Mix of both, plus interactions** → this is where you land, and it's why you've been using `smf.ols` formulas rather than a "named" test

| Question                                                               | Outcome Type | Predictor Type           | Standard Test                                      |
| ---------------------------------------------------------------------- | ------------ | ------------------------ | -------------------------------------------------- |
| Do two groups differ in a continuous measure?                          | Continuous   | 1 categorical, 2 levels  | t-test                                             |
| Do 3+ groups differ in a continuous measure?                           | Continuous   | 1 categorical, 3+ levels | ANOVA                                              |
| Do two continuous variables move together?                             | Continuous   | Continuous               | Correlation (Pearson/Spearman)                     |
| Does a continuous predictor explain/predict a continuous outcome?      | Continuous   | Continuous               | Simple linear regression                           |
| Does the outcome depend on multiple predictors, possibly interacting?  | Continuous   | Mix, with interactions   | Multiple regression (what you're doing)            |
| Same as above, but individuals are grouped (tanks) and not independent | Continuous   | Mix, with interactions   | Mixed-effects regression (random effect for tank)  |
| Does a categorical outcome (survived/died) depend on predictors?       | Binary       | Any                      | Logistic regression                                |
| Are two categorical variables associated?                              | Categorical  | Categorical              | Chi-square test                                    |

# Question 1: Do initial morphological characteristics predict subsequent growth rate, and does this relationship differ among treatments? (continuous data hence regression analysis)
* Predictor (X): initial growth at t1 (continuous variable)
* Response (Y): growth rate
* If the line graph slopes upward, kelp that were initially larger tend to grow faster
* If the line graph slopes downward, kelp that were initially larger tend to grow slower
- Treatment is then added to check whether these line graphs have different slopes 
- We analyze each time interval separately (how did growth change at each phase?):
	* t1 - t2: growth before the heatwave
	* t2 - t3: growth during the heatwave period
	* t3 - t4: growth during recovery
* Initial morphological characteristics to look at:
	* length_bl_t1 = blade length
	* length_total_t1 = total length
	* weight_total_t1 = total weight
	* diam_bulb_t1 = bulb diameter
	* length_sthf_t1 = stipe/holdfast-related length
* Growth rate outcomes:
	* growth_rate_t1t2
	* growth_rate_t2t3
	* growth_rate_t3t4

#### Approach:
1. Test each initial metric individually
2. Multivariate approach combining all metrics

##### Step 1: Check shape of distribution of initial blade length across the kelp
* **Chart used:** histogram - we're checking a single variable distribution
* Purpose: sorts each kelp into difference bins according to blade length
* **x axis** = bins (size ranges e.g., 0-2 cm)
* Need to choose equal and sensible bin sizes to show representation well (not too large, not too small)
* **y axis** = count of how many kelp fall into a specific bin
* **Shape** = how the peaks are shaped
* Here, we have **bimodal distribution** (2 peaks instead of one smooth bell curve (**normal/unimodaldistribution**))
* Bimodal means we have two different groups combined into one column and each group has its own "typical size"
* We have one hump around 9-11 cm, a dip around 13-15 cm, a _second_ hump around 16-19 cm, then a gradual decline down to a nearly empty region around 32-35 cm, with a few outliers up near 37-38 cm
* This means we're combining 2 different starting sizes
* Most kelp seem to start at ~10cm with very few at ~36 cm (lots of variability in initial blade length)
* **Basic stats**:
	1. **Percentiles**
		* If we lined up data from smallest to largest, what value marks the point where x% of the data falls below it?
		* **Formula**: L = p/100(n+1)
			* P = the percentile we want
			* n = number of observations
			* L = position in the ordered dataset
		* **Example:**
			* We want P=75, and n=10 and our ordered data is 4, 5, 6, 7, 8, 10, 12, 13, 15, 18:
				* L = 75/100(10+1)
				* L = 8.25
				* So the 75th percentile is at **position 8.25**
				* Position 8.25 means we're **25% of the way between the 8th and 9th observations**
				* The 8th value is 13 and the 9th is 15:
					* 13+0.25(15−13) = 13.5
					* So the **75th percentile is 13.5 cm**
				* 75% of all observations fall at or below 13.5 cm
		* **25th percentile (Q1):** 25% of observations are below this value 
		- **50th percentile (median):** 50% are below this value
		- **75th percentile (Q3):** 75% are below this value
		- **90th percentile:** 90% are below this value
		- **From our data:**
			- 25th percentile = 11
				- 25% of the kelp fall at or below 11 cm
			- 75th percentile = 22
				- 75% of the kelp fall at or below 22 cm
			- median (50th percentile) = 16.2
				- 50% of the kelp fall at or below 16.2 cm
	2. **Other stat**s
		* min = 3.6 cm
		* max = 38.5 cm
		* mean = 16.52 cm (center of the data)
		* std = 7.23 cm. This indicates the amount of variation in kelp blade lengths around the mean (16.52 cm). The blade lengths typically vary by about 7.23 cm around the mean
		* The top 10 smallest values (3.6 - 5.8 cm) are associated with kelp that mostly died early (between t1 and t3, with none making it to t4), while the large ones survived to t4

![[Pasted image 20260805102551.png]]


##### Step 2: Treatment comparisons - does our variable (initial blade length) differ across treatments?
* **Chart used:** Box plot - compares a continuous variable across categories
* **Purpose**: visualizes percentiles (refer to percentiles above)
* **Limitation:** Only shows five 'landmarks' - min, max, Q1, median and Q3. Doesn't show a group's distribution, e.g., if it is bimodal, like a histogram does. This is instead captured by a violin plot
* Basic box plot:
		○  outlier
        |
       ---   ← max (excluding outliers)
        |
   ┌─────────┐  ← 75th percentile (top of box)
   │                       │
   │      -------      │  ← median / 50th percentile (line inside box. Not affected by outliers)
   │                       │
   └─────────┘  ← 25th percentile (bottom of box)
        |
       ---   ← min (excluding outliers)
        |
        ○  outlier
* The box itself (box height) is the interquartile range (IQR)
	* IQR is a measure of how spread out the middle 50% of the data is 
		* Can be tightly clustered or spread out
		* Larger box = greater variability among the middle 50% of observations
		* Smaller box = tight cluster around the median
	* IQR = Q3 - Q1
		* Q1​ = **25th percentile** (first quartile). This is the median of the **lower half** (when you split the data by 50% after organizing from smallest to largest (original median))
		- Q3​ = **75th percentile** (third quartile). This is the median of the **upper half**
		- Therefore, the central 50% of the data is represented by the interval Q3 and Q1
	- E.g., if we have IQR for our kelp as 7cm, it means the middle 50% of the kelp blade length spans 7cm
	- This doesn't mean each kelp differs from another by 7cm, rather it describes the width of the central portion of the distribution
- **The whiskers** (the thin lines sticking out top and bottom) extend to the most extreme data points that are  within 1.5 × IQR of the box edges
	- **1.5 × IQR is used to determine the boundaries beyond which observations are considered potential outliers**
	- **For example:**
		- IQR = Q3 - Q1
		- IQR = 13 - 6 = 7 cm
		- Boundary = 1.5 * IQR
		- Boundary = 1.5 * 7 = 10.5 cm
		- Lower fence = Q1 - 1.5(IQR)
		- Lower fence = 6 - 10.5 = -4.5 cm
		- Upper fence  = 13 + 10.5 = 23,5cm
		- Therefore:
			- Values **below −4.5 cm** are potential outliers
			- Values **above 23.5 cm** are also potential outliers
			- Values between those limits are not considered outliers 
	- Shows how far the **non-outlier observations** extend beyond Q1 and Q3
	- Long whiskers mean there is more spread in the lower and/or upper portions of the data
	- **NB:** **1.5 does not mean that anything beyond 1.5 IQR is definitely an outlier.** It means the observation is unusual enough that we should investigate it
	- For example, if a kelp blade is flagged as an outlier, we might ask:
		- Was it measured incorrectly?
		- Is there a recording error?
		- Is this genuinely an unusually large kelp blade?
		- Is the population naturally variable?
	- We **shouldn't automatically remove it** just because it falls beyond the whisker.
- **The dots (circles) beyond the whiskers** are flagged as **outliers** (points further than 1.5 × IQR from the box). These are the very large and very small values
* **x axis:** Various treatment groups 
* **y axis:** initial blade length

###### Plot 1
* Combines **all** 8 treatment groups from both objectives:
	* **Objective I**
		* 3 temperatures & 2 surfaces - sterilized (disrupted) and non-sterilized (intact/natural microbes): 
			- 10°C (ambient/control) = 5 intact tanks ( wild_nat) + 5 disrupted tanks (wild_disr) 
		    - 14°C (warm) = 5 intact tanks (wild_nat), 5 disrupted tanks (wild_disr) 
			- 18°C (hot) = 5 intact tanks (wild_nat), 5 disrupted tanks (wild_disr) 
		- Total of 30 tanks with 135 kelp individuals total
	* **Objective II**
		* 2 temperatures & 2 origins - wild and lab-grown (no microbial disruption)
		* 10°C (ambient/control) = 5 wild tanks (wild_nat) + 3 cultured tanks (cult_nat) 
		- 18°C (hot) = 5 wild tanks (wild_nat) + 3 cultured tanks (cult_nat) 
		- The wild kelp are shared between the 2 objectives
		- Total of 16 tanks with 96 kelp individuals total
- **kelp_wild14nat** has the highest median (~22 cm). It's both the largest-starting (highest initial blade length) 
- **kelp_wild18disr** has the lowest median (~15cm) among wild groups and by far the tallest box, meaning the middle 50% of its kelp span a huge range (roughly 9.5 to 21 cm) hence high variability around the median in initial blade length
- **kelp_wild10nat**, **kelp_wild10disr**, kelp_wild18nat **all** sit in a fairly similar middle range (medians ~17-19.5cm) with moderate box heights
- **kelp_wild14nat**, **kelp_wild10disr** and **kelp_wild18nat** both all outlier dots above their whiskers (very large individuals)
* Both cultured groups have **noticeably lower medians** (~11cm and ~10cm) than _every single wild group_ (which range roughly 15-22cm median)
* Cultured kelp started smaller than wild kelp across the board
* Both cultured groups also have short, tight boxes (small IQR), meaning **cultured kelp were fairly uniform in starting size**, unlike some of the wild groups (especially **kelp_wild18disr**, which was spread out)
* **kelp_cult10nat** has two three dots (**one low outlier (5.5)** and **two high outliers (16.0, 18.0)**) breaking its otherwise tight box.
* **kelp_cult18nat** has one high outlier (~37.5cm) that's dramatically bigger than the rest of its own group 
![[Pasted image 20260805124055.png]]

###### Plot 2
**Objective I (temperature x surface)**
* Initial blade length appears to differ by surface treatment in a way that is dependent on temperature:
	* At 14°C and 18°C, kelp with an intact (natural) microbiome started out somewhat larger on average than kelp with a disrupted microbiome, and this gap was more pronounced at 18°C
	* At 10°C, however, this pattern reversed slightly. Disrupted-surface kelp had a marginally higher median starting length than natural-surface kelp, and the two groups largely overlap
* The **gap between natural and disrupted grows** as temperature increases: 
	- At 10°C the two boxes almost overlap, but at 18°C the disrupted box has dropped much lower (median ~15cm) while natural stays elevated (median ~17.5cm)  
- Variability in starting length (both the spread of the middle 50% of individuals and the range of non-extreme values (whiskers)) is also temperature-dependent: 
	* Disrupted-surface kelp are more variable in blade length than natural-surface kelp at 14°C and 18°C
	* However, this pattern does not hold at 10°C, where natural-surface kelp show greater variability
- Outliers (unusually large individuals) were concentrated in the natural-surface groups at 14°C and 18°C, while disrupted-surface groups showed only a single outlier
	- Natural surface kelp have the most outliers - 14°C natural has two high outliers while 18°C has one
	- Disrupted surface only has one outlier at 10°C
![[Pasted image 20260805124113.png]]

###### Plot 3
**Objective II (temperature x origin)**
* **Initial blade length differed clearly by origin, and unlike in Objective I, this pattern was consistent across both temperatures:**
	* Wild kelp started out with a notably larger median blade length than cultured kelp at both 10°C and 18°C, and this gap widened modestly at the higher temperature 
		* At 10 °C, the wild median is ~17.2 cm while cultured median is ~11 cm 
		* At 18°C, the wild median is ~17.5 cm while cultured median is ~10 cm
	* Wild kelp start out with a larger median initial blade length compared to cultured kelp, which have much smaller initial blade length
* **Wild kelp were also more variable in starting size than cultured kelp at both temperatures:**
	* Both the spread of the middle 50% of individuals and the range of non-extreme values were consistently larger for wild kelp
	* Cultured kelp, by contrast, were tightly clustered around their median at both temperatures
	* Outliers were more common among cultured kelp:
		* At 10°C,  three individuals fell outside the typical range (one unusually small, two unusually large)
		* 1 outlier at 18°C
	* Wild kelp showed no outliers at 10°C and only a single large outlier at 18°C
![[Pasted image 20260805134900.png]]

##### Step 3: Verify relationship - Does initial blade length predict t1-t2 growth rate, and does that relationship differ among treatments?
###### Objective I
* **Required:** Kelp with both initial blade length and a t1-t2 growth rate measurement = 134/171 kelp:

| Treatment       | Count |
| --------------- | ----- |
| kelp_wild10nat  | 30    |
| kelp_wild18nat  | 30    |
| kelp_wild18disr | 29    |
| kelp_wild10disr | 15    |
| kelp_wild14disr | 15    |
| kelp_wild14nat  | 15    |

* **Plot used:** Scatter plot with colors for treatments and regression line laid over
* **Purpose:** The scatter plot shows us the relationship between two continuous variables (initial_blade_length and growth_rate_t1t2), split by treatment (categorical), hence the colors - **Is there a relationship?**
* The regression line laid over gives a quick visual summary of the raw relationship, same as the median, Q1 and Q3 lines in a box plot, so that we can see the trend at a glance
* **Visual Impressions (association not proof of cause, i.e., no statistical validation yet):**
	* This plot shows initial blade length on the x-axis and growth rate (t1 to t2) on the y-axis. Color shows temperature, and shape shows surface type (natural vs. disrupted)
	* Overall, bigger kelp at the start tend to have faster growth rates
	* The relationship looks roughly linear - a single straight line fits the data reasonably well across the whole range, without an obvious curve
	* The gray shaded band shows how confident we are in the trend line's position. It is narrower in the middle (more data points there) and wider at the edges (fewer data points, so less certainty about exactly where the line sits)
	* **Comparing temperatures:** for natural-surface kelp, growth rate is lowest at 10°C and higher at 14°C and 18°C. For disrupted-surface kelp, the opposite happens; growth rate is highest at 10°C and drops at 18°C
	* **Comparing surface:** At 10°C, disrupted kelp  grow slightly faster than natural kelp. But at 14°C and 18°C, this flips, with natural kelp growing faster than disrupted kelp, indicating surface effect isn't fixed but dependent on temperature
	* Two natural surface kelp stand out with unusually high growth rates (around 2.0–2.25 cm/day), with one at 10°C and another at 18°C
	* This plot suggests initial blade length has an overall positive relationship with growth rate, and that this relationship may depend on temperature and surface
	* We can test this properly using a **regression model that lets the effect of blade length, temperature, and surface (and their interactions) all be estimated at once, while accounting for kelp being grouped within tanks** (a mixed-effects model)
	![[Pasted image 20260806093509.png]]
