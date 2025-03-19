# Practical1
### Will a Customer Accept the Coupon?

**Context**

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

**Overview**

The goal of this project is to use what you know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

**Data**

This data comes to us from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50).

====================================================================

**Data Description**

The columns are as follows:

destination: 	 3 unique values [object]
unique values: ['No Urgent Place' 'Home' 'Work']

++++++++++++++++++++++++++++++++++++++++++++++

passanger: 	 4 unique values [object]
unique values: ['Alone' 'Friend(s)' 'Kid(s)' 'Partner']

++++++++++++++++++++++++++++++++++++++++++++++

weather: 	 3 unique values [object]
unique values: ['Sunny' 'Rainy' 'Snowy']

++++++++++++++++++++++++++++++++++++++++++++++

temperature: 	 3 unique values [int64]
unique values: [55 80 30]

++++++++++++++++++++++++++++++++++++++++++++++

time: 	 5 unique values [object]
unique values: ['2PM' '10AM' '6PM' '7AM' '10PM']

++++++++++++++++++++++++++++++++++++++++++++++

coupon: 	 5 unique values [object]
unique values: ['Restaurant(<20)' 'Coffee House' 'Carry out & Take away' 'Bar'
 'Restaurant(20-50)']

++++++++++++++++++++++++++++++++++++++++++++++

expiration: 	 2 unique values [object]
unique values: ['1d' '2h']

++++++++++++++++++++++++++++++++++++++++++++++

gender: 	 2 unique values [object]
unique values: ['Female' 'Male']

++++++++++++++++++++++++++++++++++++++++++++++

age: 	 8 unique values [object]
unique values: ['21' '46' '26' '31' '41' '50plus' '36' 'below21']

++++++++++++++++++++++++++++++++++++++++++++++

maritalStatus: 	 5 unique values [object]
unique values: ['Unmarried partner' 'Single' 'Married partner' 'Divorced' 'Widowed']

++++++++++++++++++++++++++++++++++++++++++++++

has_children: 	 2 unique values [int64]
unique values: [1 0]

++++++++++++++++++++++++++++++++++++++++++++++

education: 	 6 unique values [object]
unique values: ['Some college - no degree' 'Bachelors degree' 'Associates degree'
 'High School Graduate' 'Graduate degree (Masters or Doctorate)'
 'Some High School']

++++++++++++++++++++++++++++++++++++++++++++++

occupation: 	 25 unique values [object]
unique values: ['Unemployed' 'Architecture & Engineering' 'Student'
 'Education&Training&Library' 'Healthcare Support'
 'Healthcare Practitioners & Technical' 'Sales & Related' 'Management'
 'Arts Design Entertainment Sports & Media' 'Computer & Mathematical'
 'Life Physical Social Science' 'Personal Care & Service'
 'Community & Social Services' 'Office & Administrative Support'
 'Construction & Extraction' 'Legal' 'Retired'
 'Installation Maintenance & Repair' 'Transportation & Material Moving'
 'Business & Financial' 'Protective Service'
 'Food Preparation & Serving Related' 'Production Occupations'
 'Building & Grounds Cleaning & Maintenance' 'Farming Fishing & Forestry']

++++++++++++++++++++++++++++++++++++++++++++++

income: 	 9 unique values [object]
unique values: ['$37500 - $49999' '$62500 - $74999' '$12500 - $24999' '$75000 - $87499'
 '$50000 - $62499' '$25000 - $37499' '$100000 or More' '$87500 - $99999'
 'Less than $12500']

++++++++++++++++++++++++++++++++++++++++++++++

car: 	 5 unique values [object]
unique values: [nan 'Scooter and motorcycle' 'crossover' 'Mazda5' 'do not drive'
 'Car that is too old to install Onstar :D']

++++++++++++++++++++++++++++++++++++++++++++++

Bar: 	 5 unique values [object]
unique values: ['never' 'less1' '1~3' 'gt8' nan '4~8']

++++++++++++++++++++++++++++++++++++++++++++++

CoffeeHouse: 	 5 unique values [object]
unique values: ['never' 'less1' '4~8' '1~3' 'gt8' nan]

++++++++++++++++++++++++++++++++++++++++++++++

CarryAway: 	 5 unique values [object]
unique values: [nan '4~8' '1~3' 'gt8' 'less1' 'never']

++++++++++++++++++++++++++++++++++++++++++++++

RestaurantLessThan20: 	 5 unique values [object]
unique values: ['4~8' '1~3' 'less1' 'gt8' nan 'never']

++++++++++++++++++++++++++++++++++++++++++++++

Restaurant20To50: 	 5 unique values [object]
unique values: ['1~3' 'less1' 'never' 'gt8' '4~8' nan]

++++++++++++++++++++++++++++++++++++++++++++++

toCoupon_GEQ5min: 	 1 unique values [int64]
unique values: [1]

++++++++++++++++++++++++++++++++++++++++++++++

toCoupon_GEQ15min: 	 2 unique values [int64]
unique values: [0 1]

++++++++++++++++++++++++++++++++++++++++++++++

toCoupon_GEQ25min: 	 2 unique values [int64]
unique values: [0 1]

++++++++++++++++++++++++++++++++++++++++++++++

direction_same: 	 2 unique values [int64]
unique values: [0 1]

++++++++++++++++++++++++++++++++++++++++++++++

direction_opp: 	 2 unique values [int64]
unique values: [1 0]

++++++++++++++++++++++++++++++++++++++++++++++

Y: 	 2 unique values [int64]
unique values: [1 0]

====================================================================


nnnnnnn

====================================================================

**By: Somaye Jafari**
