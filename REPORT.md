#**R1**

"Does the booking cancellation rate differ between repeated guests and first-time guests by enough to justify giving membership benefits 
to regular customers and special offers to new customers?"

*Answer*

Yes. Repeated guests have a cancellation rate of 7.64%, while new guests have a cancellation rate of 28.30%. This is a difference of about 
20.66 percentage points, suggesting that customer retention and loyalty programs may help reduce cancellations and improve revenue stability.

**R2  — The Data**

*Data Source : Kaggle*
The dataset used in this project is the Hotel Booking Demand Dataset, which is a publicly available dataset for research and educational purposes.

*Dataset Size*

The dataset contains 87,396 rows and 32 columns after removing duplicate records.

*What One Row Represents*

Each row represents one hotel booking made by a customer.

*Potential Grouping Variables*

The dataset contains several categorical variables that can be used for grouping and comparison:

- hotel (City Hotel, Resort Hotel)
- meal (BB, HB, FB, SC, Undefined)
- market_segment (Online TA, Offline TA/TO, Corporate, Complementary, etc.)
- distribution_channel
- deposit_type
- customer_type
- is_repeated_guest
- reserved_room_type
- assigned_room_type
- country

For this analysis, the primary grouping variable selected is:
- is_repeated_guest (New Guest vs Repeated Guest)
  - 0 = New Guest
  - 1 = Repeated Guest

*Outcome Variable which is numerical*
- is_canceled
  - 0 = Booking Not Cancelled
  - 1 = Booking Cancelled

*Quality Audit*

- The `children` column contains 4 missing values.
- The `country` column contains 452 missing values.
- The `agent` column contains 12,193 missing values.
- The `company` column contains 82,137 missing values (more than 93% missing values).
- The `meal` column contains an "Undefined" category, which may indicate incomplete information.
- No duplicate records were found after data cleaning.

*Suspicious Values*

1. Presence of negative "adr" value
# One record contains a negative "adr" value (-6.38),
# which is not realistic because room prices cannot be negative.

# 2. Company column has a huge number of missing values
# The company column contains 82,137 missing values,
# indicating that most bookings were not associated with a company
# or the information was not recorded.

# 3. Presence of outliers in adr
# The "adr" column shows possible outliers because the maximum value
# (5400) is much higher than the average value (106.34).
# This indicates the presence of extreme booking prices.

#**R3**
##*1. 95% Confidence Interval*

# The computed 95% confidence interval for the difference
# in cancellation rates is:

# [-0.2160 , -0.1971]

# This indicates that the true difference in cancellation
# rates between repeated guests and new guests is likely
# to lie between -21.60% and -19.71%.

##*Absolute and Relative Difference*

# Absolute Difference = -0.2065

# The negative sign indicates that repeated guests have
# a lower cancellation rate than new guests.

# Relative Difference:
# The cancellation rate of repeated guests is lower
# relative to the baseline group (new guests).

# Therefore, repeated guests are less likely to cancel
# their bookings compared to first-time guests.

#**R4 – Ruling Out Alternative Explanations**

# 1. Chance
#
# The naive difference in cancellation rates between
# repeated guests and new guests was -20.65 percentage points.
#
# 95% Confidence Interval:
# [-21.60%, -19.71%]
#
# Since the confidence interval does not include zero,
# the observed difference is unlikely to be due to random chance.


# 2. Confounding
#
# Lead time was identified as a plausible confounding variable
# because it may influence cancellation behavior and differs
# between repeated and non-repeated guests.
#
# After controlling for lead time (lead_time > 200 days):
#
# New Guests Cancellation Rate = 40.46%
# Repeated Guests Cancellation Rate = 37.14%
#
# Controlled Difference = -3.32 percentage points
#
# Compared to the naive estimate (-20.65 percentage points),
# the effect became much smaller after controlling for lead time.
#
# This suggests that lead time explains a substantial part
# of the observed difference in cancellation rates.


# 3. Artefact
#
# The dataset does not contain detailed information about
# the booking data collection process.
#
# Therefore, it is not possible to fully verify whether
# measurement procedures or data collection methods differed
# between repeated and non-repeated guests.
#
# However, the same target variable (is_canceled) was used
# for both groups, reducing the likelihood of measurement bias.


# Comparison of Estimates
#
# Naive Estimate      = -20.65 percentage points
# Controlled Estimate = -3.32 percentage points
#
# The controlled estimate is much smaller than the naive estimate,
# indicating that lead time acts as an important confounding factor.

#**R5**

# R5 – Sensitivity Analysis

# To verify that the conclusion does not depend on a single
# arbitrary choice, the controlled estimate was recomputed
# under multiple reasonable alternatives.

# Alternative 1:
# Lead-time bands: [0-30, 31-90, 91-180, 180+] 

# Alternative 2:
# Lead-time bands: [0-60, 61-120, 121-240, 240+]

# Alternative 3:
# Hotel type was used as an alternative confounding variable.

# Alternative 4 (optional):
# Lead-time outliers were excluded using the IQR method.

# Across these alternative specifications, repeated guests
# consistently showed lower cancellation rates than new guests.

# Therefore, the main conclusion is stable and does not depend
# on a single modeling choice.

# If the magnitude of the effect changes across alternatives,
# the direction and amount of drift should be reported.

#**R6**
# all the mentioned points which are written the above.

#**R7 – One Memorable Number**

# 7.64%

# The cancellation rate among repeated guests is only 7.64%.
# This indicates that customers who choose to stay at the hotel
# again are less likely to cancel their bookings, reflecting
# stronger customer loyalty and satisfaction.
