# Install PuLP and add library packages


```python
pip install pulp
```

    Requirement already satisfied: pulp in /Users/albertlee/opt/anaconda3/lib/python3.9/site-packages (2.9.0)
    Note: you may need to restart the kernel to use updated packages.



```python
import pandas as pd
from pulp import *
```

# Add Dataframe from Excel File with Diet Foods


```python
df = pd.read_excel("Assignment_1_Diet.xlsx")
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Foods</th>
      <th>Price_Per_Serving</th>
      <th>Serving_Size</th>
      <th>Calories</th>
      <th>Cholesterol_mg</th>
      <th>Total_Fat_g</th>
      <th>Sodium_mg</th>
      <th>Carbohydrates_g</th>
      <th>Dietary_Fiber_g</th>
      <th>Protein_g</th>
      <th>Vit_D_mcg</th>
      <th>Vit_A_mcg</th>
      <th>Vit_C_mcg</th>
      <th>Calcium_mg</th>
      <th>Iron_mg</th>
      <th>Potassium_mg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tofu</td>
      <td>0.78</td>
      <td>1/2 Block of Tofu</td>
      <td>190.0</td>
      <td>0</td>
      <td>12.0</td>
      <td>9.0</td>
      <td>2.8</td>
      <td>2.3</td>
      <td>22.8</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>642.5</td>
      <td>4.8</td>
      <td>295.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>White Rice</td>
      <td>0.29</td>
      <td>1 Cup</td>
      <td>205.0</td>
      <td>0</td>
      <td>0.4</td>
      <td>0.0</td>
      <td>45.0</td>
      <td>0.6</td>
      <td>4.3</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>16.0</td>
      <td>1.9</td>
      <td>55.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mango</td>
      <td>0.83</td>
      <td>1 Mango</td>
      <td>202.0</td>
      <td>0</td>
      <td>1.3</td>
      <td>3.4</td>
      <td>50.0</td>
      <td>5.4</td>
      <td>2.8</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>37.0</td>
      <td>0.5</td>
      <td>564.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Low Sodium Soy Sauce</td>
      <td>0.22</td>
      <td>1 Tbsp</td>
      <td>8.1</td>
      <td>0</td>
      <td>0.0</td>
      <td>511.0</td>
      <td>0.8</td>
      <td>0.1</td>
      <td>1.3</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>4.3</td>
      <td>0.2</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Avacado</td>
      <td>0.42</td>
      <td>1 Avacado</td>
      <td>322.0</td>
      <td>0</td>
      <td>29.0</td>
      <td>14.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>24.0</td>
      <td>1.1</td>
      <td>974.9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Edamame</td>
      <td>0.62</td>
      <td>1/2 Cup</td>
      <td>94.0</td>
      <td>0</td>
      <td>4.0</td>
      <td>4.7</td>
      <td>6.9</td>
      <td>4.0</td>
      <td>9.2</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>49.0</td>
      <td>1.8</td>
      <td>337.9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Canned Corn</td>
      <td>0.57</td>
      <td>1 Can</td>
      <td>177.0</td>
      <td>0</td>
      <td>3.2</td>
      <td>540.0</td>
      <td>38.0</td>
      <td>5.3</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9</td>
      <td>0.7</td>
      <td>348.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Hard Boiled Egg</td>
      <td>0.80</td>
      <td>2 Hard Boiled Eggs</td>
      <td>156.0</td>
      <td>374</td>
      <td>10.6</td>
      <td>124.0</td>
      <td>1.1</td>
      <td>0.0</td>
      <td>12.6</td>
      <td>2.2</td>
      <td>0</td>
      <td>0</td>
      <td>50.0</td>
      <td>1.2</td>
      <td>126.0</td>
    </tr>
  </tbody>
</table>
</div>



# Use PuLP to create the linear programming optimization


```python
# Create the 'prob' variable to contain the problem data
prob = LpProblem("Simple Diet Problem",LpMinimize)
```

    /Users/albertlee/opt/anaconda3/lib/python3.9/site-packages/pulp/pulp.py:1298: UserWarning: Spaces are not permitted in the name. Converted to '_'
      warnings.warn("Spaces are not permitted in the name. Converted to '_'")



```python
# Creates a list of the Ingredients
food_items = list(df['Foods'])
```


```python
print("The food items to consdier, are\n"+"-"*100)
for f in food_items:
    print(f,end=', ')
```

    So, the food items to consdier, are
    ----------------------------------------------------------------------------------------------------
    Tofu, White Rice, Mango, Low Sodium Soy Sauce, Avacado, Edamame, Canned Corn, Hard Boiled Egg, 


```python
costs = dict(zip(food_items,df['Price_Per_Serving']))
```


```python
costs
```




    {'Tofu': 0.78,
     'White Rice': 0.29,
     'Mango': 0.83,
     'Low Sodium Soy Sauce': 0.22,
     'Avacado': 0.42,
     'Edamame': 0.62,
     'Canned Corn': 0.57,
     'Hard Boiled Egg': 0.8}



# Create dictionary for nutritional facts for food items


```python
calories = dict(zip(food_items,df['Calories']))
```


```python
cholesterol = dict(zip(food_items,df['Cholesterol_mg']))
```


```python
fat = dict(zip(food_items,df['Total_Fat_g']))
```


```python
sodium = dict(zip(food_items,df['Sodium_mg']))
```


```python
carbohydrates = dict(zip(food_items,df['Carbohydrates_g']))
```


```python
fiber = dict(zip(food_items,df['Dietary_Fiber_g']))
```


```python
protein = dict(zip(food_items,df['Protein_g']))
```


```python
Vitamin_D = dict(zip(food_items,df['Vit_D_mcg']))
```


```python
Vitamin_A = dict(zip(food_items,df['Vit_A_mcg']))
```


```python
Vitamin_C = dict(zip(food_items,df['Vit_C_mcg']))
```


```python
calcium = dict(zip(food_items,df['Calcium_mg']))
```


```python
iron = dict(zip(food_items,df['Iron_mg']))
```


```python
potassium = dict(zip(food_items,df['Potassium_mg']))
```


```python
# A dictionary called 'food_vars' is created to contain the referenced Variables
food_vars = LpVariable.dicts("Food",food_items,0,cat='Continuous')
```


```python
food_vars
```




    {'Tofu': Food_Tofu,
     'White Rice': Food_White_Rice,
     'Mango': Food_Mango,
     'Low Sodium Soy Sauce': Food_Low_Sodium_Soy_Sauce,
     'Avacado': Food_Avacado,
     'Edamame': Food_Edamame,
     'Canned Corn': Food_Canned_Corn,
     'Hard Boiled Egg': Food_Hard_Boiled_Egg}




```python
prob += lpSum([costs[i]*food_vars[i] for i in food_items]), "Total Cost of the balanced diet"
```

# Adding Assignment Constraints


```python
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
```


```python
# The problem data is written to an .lp file
prob.writeLP("SimpleDietProblem.lp")
```




    [Food_Avacado,
     Food_Canned_Corn,
     Food_Edamame,
     Food_Hard_Boiled_Egg,
     Food_Low_Sodium_Soy_Sauce,
     Food_Mango,
     Food_Tofu,
     Food_White_Rice]




```python
# The problem is solved using PuLP's choice of Solver
prob.solve()
```

    Welcome to the CBC MILP Solver 
    Version: 2.10.3 
    Build Date: Dec 15 2019 
    
    command line - /Users/albertlee/opt/anaconda3/lib/python3.9/site-packages/pulp/solverdir/cbc/osx/64/cbc /var/folders/cz/l5s8bjb52v555tv67llq0j1c0000gn/T/cd46f2fbdb3e44d2a3330ce5aae17c8c-pulp.mps -timeMode elapsed -branch -printingOptions all -solution /var/folders/cz/l5s8bjb52v555tv67llq0j1c0000gn/T/cd46f2fbdb3e44d2a3330ce5aae17c8c-pulp.sol (default strategy 1)
    At line 2 NAME          MODEL
    At line 3 ROWS
    At line 19 COLUMNS
    At line 124 RHS
    At line 139 BOUNDS
    At line 140 ENDATA
    Problem MODEL has 14 rows, 8 columns and 96 elements
    Coin0008I MODEL read with 0 errors
    Option for timeMode changed from cpu to elapsed
    Presolve 10 (-4) rows, 8 (0) columns and 79 (-17) elements
    0  Obj 7.2727273 Primal inf 8.2461017 (4)
    2  Obj 9.5827213
    Optimal - objective value 9.5827213
    After Postsolve, objective 9.5827213, infeasibilities - dual 0 (0), primal 0 (0)
    Optimal objective 9.582721282 - 2 iterations time 0.002, Presolve 0.00
    Option for printingOptions changed from normal to all
    Total time (CPU seconds):       0.00   (Wallclock seconds):       0.00
    





    1



# Checking whether the solution is "Optimal", "Infeasible", or "Unbound"


```python
# The status of the solution is printed to the screen
print("Status:", LpStatus[prob.status])
```

    Status: Optimal


# What foods are for a balanced diet (least cost)


```python
print("Therefore, the optimal (least cost) balanced diet consists of\n"+"-"*110)
for v in prob.variables():
    if v.varValue>0:
        print(v.name, "=", v.varValue)
```

    Therefore, the optimal (least cost) balanced diet consists of
    --------------------------------------------------------------------------------------------------------------
    Food_Avacado = 3.2840226
    Food_Hard_Boiled_Egg = 9.0909091
    Food_Tofu = 1.1932109



```python
print("The total cost of this balanced diet daily is: ${}".format(round(value(prob.objective),2)))
```

    The total cost of this balanced diet daily is: $9.58



```python
print("The total cost of this balanced diet for a 7-day week is: ${}".format(round(value(prob.objective),2)*7))
```

    The total cost of this balanced diet for a 7-day week is: $67.06



```python

```
