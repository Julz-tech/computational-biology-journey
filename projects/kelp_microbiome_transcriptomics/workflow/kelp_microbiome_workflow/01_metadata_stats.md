## Question 1: Do initial morphological characteristics predict subsequent growth rate, and does this relationship differ among treatments? (continuous data hence regression analysis)
* Predictor (X): initial growth at t1
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

##### Step 1: Check shape of distribution of initial size across the kelp
* **Chart used:** histogram
* Purpose: sorts each kelp into difference bins according to size
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


##### Step 2: Treatment comparisons
* ***Chart used:** Box plot
* Purpose: visualizes percentiles (refer to percentiles above)
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