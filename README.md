# MSDS460 - Assignment 1

Assignment 1: For this assignment, you need to construct a personalized diet using current recommended dietary allowances from the U.S. Food and Drug Administration, updated to account for recent research on sodium intake and health (Mente, O'Donnell, and Yusuf 2021). Interested in learning more about nutrition and healthy living? Check out Nutrients, an open-access journal, at its home page https://www.mdpi.com/journal/nutrientsLinks to an external site. .

The constraints for this linear programming problem, should consider seven components of nutrition and their daily values, as shown in the following table:

![image](https://github.com/user-attachments/assets/300fdebf-ea9f-43d8-b37e-c211c879d393)

Set this up as a standard linear programming problem with decision variables taking any non-negative values. In other words, partial servings are permitted.

Food choices selected for this assignment are ingredients needed for a vegetarian Poke Bowl. The table below shows the food item, nutritional facts, and $ per servings. The nutritional facts can be found in the Appendix in the write-up.

![image](https://github.com/user-attachments/assets/f79ef3ec-b064-4b0d-9df1-d5fbc4ca7053)

The yellow highlighted hard-boiled egg was initially not in the model and then later added to the model as my initial linear optimizational model result was infeasible because it was missing Vitamin D. By adding the hard boiled eggs, the model resulted in optimal.

Assignment 1 Linear PuLP Problem variable Python Code: 

prob = LpProblem("Simple Diet Problem",LpMinimize)

Constraints Python: 

# Calories
prob += lpSum([calories[f] * food_vars[f] for f in food_items]) >= 2000.0, "CalorieMinimum"
prob += lpSum([calories[f] * food_vars[f] for f in food_items]) <= 3000.0, "CalorieMaximum"

# Sodium
prob += lpSum([sodium[f] * food_vars[f] for f in food_items]) >= 500.0, "SodiumMinimum"
prob += lpSum([sodium[f] * food_vars[f] for f in food_items]) <= 5000.0, "SodiumMaximum"

# Protein
prob += lpSum([protein[f] * food_vars[f] for f in food_items]) >= 50.0, "ProteinMinimum"
prob += lpSum([protein[f] * food_vars[f] for f in food_items]) <= 175.0, "ProteinMaximum"

# Vitamin D
prob += lpSum([Vitamin_D[f] * food_vars[f] for f in food_items]) >= 20.0, "VitDMinimum"
prob += lpSum([Vitamin_D[f] * food_vars[f] for f in food_items]) <= 105.0, "VitDMaximum"

# Calcium
prob += lpSum([calcium[f] * food_vars[f] for f in food_items]) >= 1300.0, "CalciumMinimum"
prob += lpSum([calcium[f] * food_vars[f] for f in food_items]) <= 2500.0, "CalciumMaximum"

# Iron
prob += lpSum([iron[f] * food_vars[f] for f in food_items]) >= 18.0, "IronMinimum"
prob += lpSum([iron[f] * food_vars[f] for f in food_items]) <= 45.0, "IronMaximum"

# Potassium
prob += lpSum([potassium[f] * food_vars[f] for f in food_items]) >= 4700.0, "PotassiumnMinimum"
prob += lpSum([potassium[f] * food_vars[f] for f in food_items]) <= 5000.0, "PotassiumMaximum"

Solution:

Therefore, the optimal (least cost) balanced diet consists of
--------------------------------------------------------------------------------------------------------------
Food_Avacado = 3.2840226
Food_Hard_Boiled_Egg = 9.0909091
Food_Tofu = 1.1932109

The total cost of this balanced diet daily is: $9.58

The total cost of this balanced diet for a 7-day week is: $67.06

