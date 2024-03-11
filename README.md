DESIGN ANALYSIS AND ALGORITHM 

Introduction:
Calorie optimization is crucial for promoting a healthy lifestyle, and leveraging algorithmic techniques is essential for designing efficient solutions. This analysis explores various algorithmic approaches for designing a Calorie Optimizer, focusing primarily on the Greedy approach and comparing its efficacy with Backtracking and Brute Force strategies. The aim is to provide insights into the strengths and weaknesses of each approach to aid in selecting the most suitable algorithmic technique for the Calorie Optimizer problem.

Problem Statement:
The rising concern of obesity and associated health issues necessitates effective weight management solutions. Existing tools often lack personalization and fail to consider diverse nutritional requirements. This project addresses this gap by presenting a Calorie Optimizer with a Greedy approach, aiming to provide a user-friendly and tailored solution for effective weight management.

Design Approach:
The Calorie Optimizer utilizes the Greedy approach to create a personalized meal plan efficiently. By iteratively adding foods with the highest nutritional value relative to their calorie content, the Greedy Knapsack algorithm ensures an optimal distribution of proteins, carbohydrates, and fiber, facilitating effective weight management. This approach balances computational efficiency with providing users a personalized and practical nutritional plan.

Algorithm Design Techniques Used:

Greedy Approach:
The Greedy approach makes locally optimal choices throughout the optimization process, working within predefined calorie limits and giving precedence to foods with exceptional nutritional density.
It navigates potential meal plans efficiently, delivering personalized and effective solutions tailored to individual caloric optimization needs.
Calorie Optimization with Greedy Approach:

Algorithm Steps:

Read Food Data: Read food data from a CSV file, storing food names and calorie information.
Extract Calories: Convert a string into a numerical calorie value.
Greedy Calorie Optimizer: Takes food options, a calorie limit, and selected food names, filters, and sorts selected foods based on calories, and iterates through sorted options, adding foods to the plan if they fit within the remaining calories.
Example Usage: Demonstrates usage by reading food data, taking user input for limits and selected foods, and printing the optimized meal plan using the Greedy Calorie Optimizer.
Time Complexity for Greedy Approach:

Best Case: O(n log n)
Average Case: O(n log n)
Worst Case: O(n^2)
Tools Used:

Anaconda Navigator
Jupyter Notebook
Python
Pandas Library
CSV File from Kaggle
Result:
The algorithm effectively utilizes a Greedy approach to optimize personalized daily meal plans, demonstrating efficiency and adaptability. The practical example showcases its user-friendly application, making it a valuable tool for generating optimized meal plans based on individual preferences and constraints.

Conclusion:
The example usage of the algorithm demonstrates its practical application, allowing users to input their personalized daily calorie limit and selected food names. The output provides an optimized meal plan, showcasing the algorithm's ability to adapt to different user preferences and constraints. Future improvements could include incorporating additional nutritional factors or optimizing for specific dietary preferences.

DATASET : https://www.kaggle.com/datasets/vaishnavivenkatesan/food-and-their-calories

CODE 


import pandas as pd

def read_food_data_from_csv(csv_file_path):
    df = pd.read_csv(csv_file_path)
    food_options = [(row['Food'], row['Calories']) for index, row in df.iterrows()]
    return food_options

def extract_calories(calories_str):
    return int(calories_str.split(' ')[0])

def greedy_calorie_optimizer(food_options, personalized_calorie_limit, selected_food_names):
    selected_food_names = [name.strip() for name in selected_food_names]
    selected_food_options = [food for food in food_options if food[0] in selected_food_names]
    sorted_food_options = sorted(selected_food_options, key=lambda x: extract_calories(x[1]), reverse=True)

    meal_plan = []
    remaining_calories = personalized_calorie_limit

    for food, calories_str in sorted_food_options:
        calories = extract_calories(calories_str)
        if remaining_calories >= calories:
            meal_plan.append((food, calories))
            remaining_calories -= calories

    return meal_plan

# Example usage:
csv_file_path = "/Users/dhivya/Downloads/Food and Calories - Sheet1.csv"
food_options_from_csv = read_food_data_from_csv(csv_file_path)

# Set your personalized daily calorie limit
personalized_calorie_limit = int(input("Enter your personalized daily calorie limit: "))

# Get the selected food names from the user
selected_food_names = input("Enter your selected food names (comma-separated): ").split(',')

# Get the optimized meal plan
optimized_meal_plan = greedy_calorie_optimizer(food_options_from_csv, personalized_calorie_limit, selected_food_names)
print("Optimized Meal Plan:", optimized_meal_plan)
