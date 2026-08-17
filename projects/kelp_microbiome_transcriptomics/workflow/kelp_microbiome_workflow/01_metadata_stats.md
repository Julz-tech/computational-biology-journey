# Question 1: Does initial morphological characteristics predict subsequent growth rate, and does this relationship differ among treatments? We follow data analysis steps outlined above
### The Data
* Data = initial blade length and growth rate (continuous)
* Predictor (X): initial blade length 
* Response (Y): growth rate
* We analyze each time interval separately (how did growth change at each phase?):
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
* Treatment is then added to check whether these line graphs have different slopes 
##### Step 1: Check shape of distribution of initial blade length across the kelp (How the data behaves)
* **Chart used:** histogram - we're checking a single variable distribution
* Purpose: sorts each kelp into difference bins according to blade length
* **x axis** = bins of initial blade length (size ranges e.g., 0-2 cm)
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


##### Treatment comparisons - does our variable (initial blade length) differ across treatments?
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

##### Step 2: Verify relationship - Does initial blade length predict t1-t2 growth rate, and does that relationship differ among treatments? (Statistical learning)
* We use data from above to make inferences
* Here, we use **supervised learning** since we have **input (Initial blade length)** and **output or target (growth rate)**, that is **already measured**. The goal is to learn the relationship between the two so that we can predict growth rate for new kelp from initial blade length
	* We use the above data and its shape to give us a model which we will use to infer the relationship
	* Since **growth rate (our target) is continuous**, we use **regression models**:
		* **Linear Regression**
			* Predicts outcome using one predictor
			* Here, we're predicting growth rate from initial length (one predictor)
		* **Multiple Linear Regression**
			* Predicts outcome using two or more predictors 
			* This will be used later when we add more variables to predict growth rate
###### Objective I - Temperature x Surface
* **Required:** Kelp with both initial blade length and a t1-t2 growth rate measurement = 134/171 kelp:

| Treatment       | Count |
| --------------- | ----- |
| kelp_wild10nat  | 30    |
| kelp_wild18nat  | 30    |
| kelp_wild18disr | 29    |
| kelp_wild10disr | 15    |
| kelp_wild14disr | 15    |
| kelp_wild14nat  | 15    |

* **Plot used:** **Scatter plot** with **colors for treatments** and **regression line** laid over
* **Purpose:** The scatter plot shows us the **relationship between two continuous variables** (initial_blade_length and growth_rate_t1t2), split by treatment (categorical), hence the colors - **Is there a relationship?**
* The regression line laid over gives a **quick visual summary of the raw relationship**, same as the median, Q1 and Q3 lines in a box plot, so that we can see the trend at a glance
* **Visual Impressions (association is not proof of cause, i.e., no statistical validation yet):**
	* This plot shows initial blade length on the x-axis and growth rate (t1 to t2) on the y-axis. Color shows temperature, and shape shows surface type (natural vs. disrupted)
	* **Conclusions from the plot:**
		* Overall, bigger kelp at the start tend to have faster growth rates
		* The relationship looks roughly linear - a single straight line fits the data reasonably well across the whole range, without an obvious curve
		* The gray shaded band shows **how confident we are in the trend line's position**. It is narrower in the middle (more data points there) and wider at the edges (fewer data points, so less certainty about exactly where the line sits)
		* **Comparing temperatures:** for natural-surface kelp, growth rate is lowest at 10°C and higher at 14°C and 18°C. For disrupted-surface kelp, the opposite happens; growth rate is highest at 10°C and drops at 18°C
		* **Comparing surface:** At 10°C, disrupted kelp  grow slightly faster than natural kelp. But at 14°C and 18°C, this flips, with natural kelp growing faster than disrupted kelp, indicating surface effect isn't fixed but dependent on temperature
		* Two natural surface kelp stand out with unusually high growth rates (around 2.0–2.25 cm/day), with one at 10°C and another at 18°C
	* This plot suggests **initial blade length has an overall positive relationship with growth rate**, and that **this relationship may depend on temperature and surface**
	* We can test this properly using a **multiple linear regression model that lets the effect of blade length, temperature, and surface (and their interactions) all be estimated at once, while accounting for kelp being grouped within tanks** (a mixed-effects model)
	![[Pasted image 20260806093509.png]]

* We have established initial blade length affects growth and that the relationship differs among treatments
* To determine **if the relationship between initial blade length and growth rate truly differs between the treatments**, we can draw two separate plots - one for natural surface and another for disrupted surface kelp:
	![[Pasted image 20260811114414.png]]
* **Step 1: What is being displayed:** This scatter plot, like the one above, has initial blade length on the x axis and growth rate on the y, with different colors representing different temperatures for each surface and a regression line to visualize the trend
* **Natural Surface Kelp**
	* **Step 2: Overall trend**
		* There's a **positive association between initial blade length and growth rate** (larger kelp at t1 tend to have faster t1→t2 growth) 
		* This positive direction **holds at all three temperatures**
		* **What differs** between temperatures is the **overall growth-rate level**, which is described in Step 5
	* **Step 3: Band around regression lines**
		* The bands all appear wider on the ends where there are less values, than the middle, reflecting some uncertainty in the regression line 
	* **Step 4: Assess linearity**
		* For **all three temperatures**, the relationship appears roughly linear 
		* A straight line fits reasonably well across the range, without an obvious curve
		* A few individual points sit noticeably above or below their group's line
		* These are worth noting separately as outliers, but they don't change the overall linear shape of the trend
	* **Step 5: Temperature encoding
		* **Overall trend:** 14°C highest throughout; 10°C starts lowest, closes the gap with 18°C by large blade lengths.
		* At small initial blade lengths, 10°C kelp have a noticeably lower growth rate than 14°C or 18°C kelp
		* However, the 10°C line rises more steeply than the others, and by the largest blade lengths, 10°C growth rates approach and possibly exceed 18°C
		* 14°C consistently shows the highest growth rate across the whole range
* **Disrupted Surface Kelp**
	* All same points except step 5
	* **Step 5: Temperature encoding
		* **Overall trend:** 14°C starts lower than 10°C but overtakes it to become highest; 18°C starts lowest and rises to approach 10°C; 10°C is the least steep
		* At small initial blade lengths, 18°C kelp have a noticeably lower growth rate than 10°C and 14°C kelp. However, 18°C line rises more steeply, approaching 10°C
		* Growth rate at 14°C consistently rises, starting lower than 10°C but overtaking 10°C to have the highest growth rate 
* If initial blade length predicted growth rate exactly the same way, regardless of temperature or surface, all regression lines would have the same slope
* However, this is not the same, meaning temperature and surface have an influence over this relationship
* Therefore, the way growth rate ranks across temperatures looks different between natural and disrupted surface kelp
* For example, 10°C has lower growth rate in natural surface but a little higher growth rate under disrupted surface
* This visual pattern is consistent with surface treatment changing how temperature affects growth (**an interaction**), but it hasn't been statistically tested yet 

####### **Conclusions until this point**
* We have the same number of kelp in t2 as what we started with at t1:

| Temperature | Natural | Disrupted |
| ----------- | ------- | --------- |
| 10          | 30      | 15        |
| 14          | 15      | 15        |
| 18          | 30      |           |
* Larger kelp tend to have higher t1-t2 growth rates across temperatures
* There is an interaction between treatment and the relationship between growth rate and initial blade length

####### **Statistical validations**
* We now check if our above conclusions are statistically supported
* **Question 1:** Is initial blade length associated with t1→t2 growth rate?
	* H₀ = Initial blade length is not associated with t1→t2 growth rate
	* H₁ = Initial blade length is associated with t1→t2 growth rate
	* **Model:** Does the size of a kelp at t1 help explain how fast it grew from t1 to t2?
		![[Pasted image 20260811124829.png]]
		* The key line is: initial_length_bl     0.0392    0.005    8.442    0.000    0.030    0.048
		* **Slope**
			* 0.0392 is the slope - tells us the direction and size of the relationship between initial blade length and growth rate
				* This means, for ever additional 1cm of initial blade length, the predicted t1-t2 growth rate increases by ~0.0392cm/day (positive relationship)
		* **Y intercept**
			* The y intercept value is 0.2238
			* This is the predicted growth rate when initial_length_bl = 0
				* If initial length = 0 cm, then predicted growth rate = 0.2238 cm/day
			* However, none of the kelp has initial length = 0 cm
			* Therefore only necessary for defining the regression line
		* The model therefore has this equation (Y ≈ β0 + β1 X)
			* growth_rate = 0.2238 + (0.0392 × initial_blade_length)
			* If we plug in different lengths, we will get higher growth rates for larger lengths
			* Therefore, we have proven that: **Larger kelp tended to grow faster during t1→t2**
		* **R²**
			* Shows how much variation in growth rate is explained by initial blade length
			* R² = 0.351
			* Therefore, 35.1% of the variation in growth rate can be accounted for by initial blade length
			* Meaning, 64.9% of the variation in growth rate is unexplained at this point
		* **p value**
			* How likely the results are if the null hypothesis is true
			* P>|t| = 0.000
			* H₀: There is no linear relationship between initial blade length and t1→t2 growth rate
			* H1: There is a linear relationship between initial blade length and t1→t2 growth rate
			* p value < 0.05 so we reject the null hypothesis
			* **Conclusion:** There is strong statistical evidence that initial blade length is associated with t1→t2 growth rate
		* **95% confidence interval**
			* We have 2 percentages: 0.025 and 0.975 ([0.025  0.975])
			* This gives us 95%
			* At this interval, for the slope, we have [0.030, 0.048]
			* The estimated slope is 0.0392
			* The plausible range according to the model is:
				* 0.030 ───────── 0.0392 ───────── 0.048
			* This therefore means the value estimated for the slope is 0.0392 with a 95% confidence interval of approximately **0.030 to 0.048**
			* This entire interval is above zero, hence supporting the conclusion that the relationship is positive
		* **F statistic**
			* F-statistic = 71.26
			* Prob (F-statistic) = 4.88e-14
			* The F-statistic compares variation explained by the model with variation left unexplained by the model
				* Is the variation explained by the model larger compared to the variation the model fails to explain?
				* =variation explained/variation remaining
				* The calculation uses **mean squares**, which account for degrees of freedom
				* Large f statistic means the model explains substantially more variation than we'd expect relative to the unexplained variation
		* **No. Observations**
			* This is the number of kelp that had values for initial_length_bl and growth_rate_t1t2 (134)
		* **Omnibus, Jarque-Bera, Skew, Kurtosis, Durbin-Watson**
			* **Diagnostics** that help us determine whether the assumptions behind OLS regression are reasonable
			* Residual = actual value - predicted value
			* Example:
				* Actual growth = 1.2 cm/day
				* Predicted      = 1.0 cm/day
				* Residual       = +0.2 cm/day
			* Omnibus = 1.048
				* Assumption: residuals are approximately **normally distributed**
				* Do the residuals show evidence of substantial non-normality?
				* H₀: residuals are approximately normally distributed
				* Since Omnibus p = 0.592,  We do not have evidence of substantial non-normality from this test
				* Not proof of perfect normality
			* Omnibus p = 0.592
			* Jarque-Bera p = 0.583
				* Another test of residual normality
				* We don't have evidence that the residuals substantially deviate from normality according to the Jarque–Bera test
				* Not proof of perfect normality
			* Skew = -0.108
				![[Pasted image 20260812113556.png|499]]
				* Residual skewness = -0.108 which is closer to 0, meaning the residuals are approximately symmetrical, with a very slight tendency toward a left tail
			* Kurtosis = 2.617
				* Describes the shape of the tails and concentration of the distribution
				* A normal distribution has a kurtosis of approximately 3
				* 2.617 is close to 3 so there's no obvious extreme-tail problem here
		* **Durbin-Watson**
			* Detects serial correlation
			* 2 → little autocorrelation
			* < 2 → positive autocorrelation
			* 2 → negative autocorrelation
			* We have 1.283 = some positive correlation
		* **Overall Conclusion from the model**
			* There is strong statistical evidence of a positive association between initial blade length and t1→t2 growth rate. 
			* The estimated increase is approximately **0.039 cm/day in growth rate for every 1 cm increase in initial blade length** (95% CI: 0.030–0.048, p < 0.001)
			* Initial blade length alone explained approximately **35% of the variation** in t1→t2 growth rate
  * **Question 2:** Does the effect of temperature on t1→t2 growth rate depend on surface treatment, after accounting for initial blade length?
		  * **Temperature effect:** Does growth differ with temperature?
		  * **Surface effect:** Does growth differ between natural and disrupted surfaces?
		  * **Temperature × surface interaction:** Does the effect of surface depend on temperature?
		  * Initial blade length is associated with t1-t2 growth rate across temperatures, with a surface interaction 
		  * H₀ = There is no temperature × surface interaction on t1→t2 growth rate
		  * H₁ = The effect of temperature on growth rate **depends on surface treatment**
	  * **Model:** size + treatments - Do treatments explain additional variation?
		  * Here, we have categorical predictors and a reference group
		  * **Assumption:** The effect of initial blade length on growth rate is the same across all temperature/surface combinations
		  * growth_rate_t1t2 ~ initial_length_bl
                     + temperature
                     + surface
                     + temperature × surface
		![[Pasted image 20260812211404.png|665]]
	  * **Reference group** = 10°C + disrupted
	  * **Categorical predictors:**
		  * treat_temp:
			  * 10, 14, 18
		  * treat_surface:
			  * `disr, nat`
	  * **R²** = 0.441
		  * The model explains approximately **44.1% of the observed variation** in t1→t2 growth rate using initial blade length, temperature, surface, and their temperature × surface interaction
		  * R² never decreases when we add more predictors to a model
		  * Even if the added predictor is useless, it will increase, giving a false impression  of the explained variation
	* **Adjusted R²** = 0.415
		* Penalizes the model for adding more predictors
		* This means, after accounting for the number of predictors in the model, the model explains about **41.5%** of the variation
	  * **F statistic** = 16.72
		  * Does the model as a whole explain significantly more variation than a model with no predictors?
		  * p = 3.78 × 10⁻¹⁴
		  * There is **very strong evidence that the model as a whole is useful for explaining growth-rate variation**
	  * **Initial blade length slope** = 0.0338
		  * For every additional 1 cm of initial blade length, the predicted t1→t2 growth rate increases by approximately 0.0338 cm/day, **holding temperature and surface treatment constant**
		  * This association is positive because 0.0338 > 0
	  * **Initial blade length p value** = 0.000
		  * There is strong statistical evidence that initial blade length is positively associated with t1→t2 growth rate **after accounting for temperature and surface treatment**
	  * **Y intercept** = 0.3474
		  * The model therefore has the equation: growth_rate = 0.3474 + (0.0338 × initial_blade_length) for the **reference treatment (10°C + disrupted)**
		* This means when **temperature is 10°C** and **surface treatment is disrupted**, the predicted growth rate **when initial blade length is 0 cm** is 0.3474 cm/day
	  * **The coefficient at 14°C (temperature effect at 14°C)** = 0.1552
		  * This means, at the reference surface treatment (**disrupted**) and at a given initial blade length, the predicted growth rate at 14°C is **0.1552 cm/day higher than at 10°C**
	  * **The coefficient at 18°C (temperature effect at 18°C)** = -0.1821
		  * This means, at the reference surface treatment (**disrupted**) and at a given initial blade length, the predicted growth rate at 18°C is **0.1821 cm/day lower than at 10°C**
	  * **The coefficient for natural surface (natural surface effect)** = -0.1233
		  * This means, at 10°C, natural-surface kelp have an estimated growth rate **0.1233 cm/day lower than disrupted-surface kelp**, for a given initial blade length
	  * **Interactions (temperature × surface interaction):**
		  * How much the effect of natural vs disrupted surface changes when we move from the reference temperature to the given temperature
		  * 14°C × natural = +0.2249
			  * The growth rate difference between natural and disrupted surfaces is estimated to be **0.2249 cm/day higher at 14°C than at 10°C**
		  * 18°C × natural = +0.2883
			  * The growth rate difference between natural and disrupted surfaces is estimated to be **0.2883 cm/day higher at 18°C than at 10°C**
	  * **Overall equation for the model:** growth rate = 0.3474 + (0.0338 × initial size) + temperature effect + surface effect + (temperature × surface interaction)
	  * **Equations for each category:**
		  * **10°C + disrupted:**
			  * There are no temperature/surface adjustments
			  * growth = 0.3474 + (0.0338 × size)
		  * **14°C + disrupted:**
			  * growth = 0.3474 + (0.0338 × size) + 0.1552 
		  * **18°C + disrupted:**
			  * growth = 0.3474 + (0.0338 × size) - 0.1821
		* **10°C + natural:**
			* growth = 0.3474 + (0.0338 × size) - 0.1233
		*  **14°C + natural:**
			* growth = 0.3474 + (0.0338 × size) + 0.1552 - 0.1233 + 0.2249
		* **18°C + natural:**
			* growth = 0.3474 + (0.0338 × size) - 0.1233 - 0.1233 + 0.2883
	* **Equations summary:**
		* 10 disr:  growth = 0.3474 + 0.0338 × size
		* 14 disr:  growth = 0.5026 + 0.0338 × size
		* 18 disr:  growth = 0.1653 + 0.0338 × size
		* 10 nat:   growth = 0.2241 + 0.0338 × size
		* 14 nat:   growth = 0.6042 + 0.0338 × size
		* 18 nat:   growth = 0.3303 + 0.0338 × size
	* **N/B:** slope is constant (0.0338) because this model assumes **the relationship between initial size and growth rate is the same across treatments**
		* The plot may show different lines vertically, but this model assumes they are essentially **parallel**
	* **Overall conclusion:** 
		* Initial blade length was positively associated with t1–t2 growth rate (β = 0.0338 cm/day per cm, p < 0.001), after accounting for temperature, surface treatment, and their interaction
		* The model explained 44.1% of the variation in t1→t2 growth rate (R² = 0.441)
		* **Adjusted R² = 0.415:** After accounting for the number of predictors in the model, the adjusted proportion of explained variation is 41.5%
		* There was evidence of a temperature × surface interaction at 18°C (β = 0.2883, p = 0.048), relative to the 10°C reference condition
		* There was no strong statistical evidence of a temperature × surface interaction at 14°C relative to 10°C (β = 0.2249, p = 0.189)
* **Question 3:** Does the relationship between initial size and growth rate change depending on temperature, surface, or the combination of temperature and surface?
	* H₀ = The relationship between initial blade length and t1→t2 growth rate does not differ among treatments
	  * H₁ = The relationship between initial blade length and t1→t2 growth rate differs among treatments
	* Model
		* Allows the **slope  to change depending on temperature and surface**:
			* initial_length × temperature
			* initial_length × surface
			* initial_length × temperature × surface
			* growth_rate_t1t2 ~ initial_length_bl * C(treat_temp) * C(treat_surface):
				* (initial length) + (temperature) + (surface) + (initial length × temperature) + (initial length × surface) + (temperature × surface) + (initial length × temperature × surface)
		![[Pasted image 20260815164544.png]]
	* **Reference group** = 10°C + disrupted
		  * **Categorical predictors:**
			  * treat_temp:
				  * 10, 14, 18
			  * treat_surface:
				  * `disr, nat`
		  * **R²** = 0.468
			  * The model explains approximately 46.8% of the variation in t1→t2 growth rate using initial blade length, temperature, surface, and their **two-way and three-way interactions**
				  * **Two-way interactions:**
					  * initial length × temperature
					  * initial length × surface
					  * temperature × surface
				  * **Three-way interaction:**
					  * initial length × temperature × surface
	* **Adjusted R²** = 0.420
		* After accounting for the number of predictors in the model, the adjusted R² indicates that approximately 42.0% of the variation in growth rate is explained by the model
	  * **F statistic** = 9.761
		  * p = 1.69 × 10^-12
		  * There is **very strong evidence that the model as a whole is useful for explaining growth-rate variation**
	  * **Initial blade length slope** = 0.0185
		  * At the **reference temperature and reference surface**, each additional 1 cm of initial blade length is associated with an estimated 0.0185 cm/day higher t1→t2 growth rate
		  * N/B: This slope is not for every treatment. It is the slope for the reference treatment only (10°C + disrupted surface)
	  * **Initial blade length p value** = 0.240
		  * This p-value asks whether the initial-length slope is different from zero for the reference treatment combination (10°C + disrupted surface)
		  * There is no statistical evidence that the initial-length slope differs from zero for the reference treatment combination (10°C + disrupted surface), β0 = 0.0185, p = 0.240
	  * **Y intercept** = 0.3474
		  * The model therefore has the equation: growth_rate = 0.3474 + (0.0338 × initial_blade_length) for the **reference treatment (10°C + disrupted)**
		* This means when **temperature is 10°C** and **surface treatment is disrupted**, the predicted growth rate **when initial blade length is 0 cm** is 0.3474 cm/day
	  * **The coefficient at 14°C (temperature effect at 14°C)** = 0.1552
		  * This means, at the reference surface treatment (**disrupted**) and at a given initial blade length, the predicted growth rate at 14°C is **0.1552 cm/day higher than at 10°C**
	  * **The coefficient at 18°C (temperature effect at 18°C)** = -0.1821
		  * This means, at the reference surface treatment (**disrupted**) and at a given initial blade length, the predicted growth rate at 18°C is **0.1821 cm/day lower than at 10°C**
	  * **The coefficient for natural surface (natural surface effect)** = -0.1233
		  * This means, at 10°C, natural-surface kelp have an estimated growth rate **0.1233 cm/day lower than disrupted-surface kelp**, for a given initial blade length
	  * **Interactions (temperature × surface interaction):**
		  * How much the effect of natural vs disrupted surface changes when we move from the reference temperature to the given temperature
		  * 14°C × natural = +0.2249
			  * The growth rate difference between natural and disrupted surfaces is estimated to be **0.2249 cm/day higher at 14°C than at 10°C**
		  * 18°C × natural = +0.2883
			  * The growth rate difference between natural and disrupted surfaces is estimated to be **0.2883 cm/day higher at 18°C than at 10°C**
	  * **Overall equation for the model:** growth rate = 0.3474 + (0.0338 × initial size) + temperature effect + surface effect + (temperature × surface interaction)