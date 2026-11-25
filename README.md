# CSC207-Group-Assignment

## Ideas:
### ANISHA:
Entities: Paper, SectionTag, SectionNote

\External API: OpenAlex API (or CrossRef API) for use case 1 for searching real academic papers by title, keyword, or DOI

#### 1. Search & Import Paper (API)
User story: As a researcher writing a paper, I want to search for academic articles by title, keyword, or DOI using an external literature API and save relevant results into my personal library, so that I do not have to manually type out bibliographic details.

\flow/details:
1. User enters a search query (title, keyword, or DOI) into the search bar.
2. System queries the external academic API (e.g., OpenAlex or CrossRef) and displays matching papers (title, authors, year, abstract).
3. User selects a paper and clicks Add to Library (or uses a manual-entry option if a paper is not indexed).
4. System creates a Paper entity, saves it to persistent storage, and confirms it has been added without duplicates.
##### 2. Tag & Annotate for Paper Sections
User Story: As a writer organizing my sources, I want to assign paper-section tags (such as Introduction, Related Work, Methods, or Discussion) and attach short notes or quotes to saved papers, so that I remember how and where I plan to cite each source in my draft.

\flow/details:
1. User selects a saved paper from their library.
2. User selects one or more section tags (predefined or custom) and enters a section-specific note (for ex. "Use this statistic for paragraph 2 of the Intro").
3. System updates the Paper entity with the SectionTag and note, persists the changes, and updates the paper's displayed tags in the UI.
#### 3. Filter & Search Library by Section
User Story: As a writer drafting a specific section of my paper, I want to filter my saved library by section tag, author, publication year, or keywords in my notes, so that I can quickly view only the sources relevant to the section I am currently writing.

\flow/details:
1. User selects one or more filter criteria (e.g., tag = Introduction, year >= 2020 or a keyword search).
2. System applies the selected filter rules to the saved library and returns the matching subset of papers.
3. User can clear or combine filters dynamically to switch focus between different sections of their paper.
#### 4. Generate Section Outline & Citations
User Story: As a researcher transitioning from reading to writing, I want to export a structured outline for a selected paper section (or my entire library) containing my notes and formatted citations (e.g., APA, IEEE, or BibTeX), so that I can directly integrate my organized literature into my manuscript.

\details/flow:
1. User selects a target scope (for ex. Introduction section only, or all sections) and chooses a citation format (APA, IEEE, or BibTeX).
2. System groups the matching papers by section, formats each reference according to the chosen style, and attaches the user's section notes underneath each citation.
3. User previews the generated outline and exports it to a local .md or a .txt file.



## EBUKA: Finance / Budgeting App

## General Purpose

The application is a personal finance management tool that helps users organize their finances, monitor spending, and make informed budgeting decisions.

Users can create monthly budgets, record and categorize income and expenses, set financial goals, and review spending patterns through summaries and visualizations.

## Core Use Cases

### Use Case #1: Create & Manage a Budget

**Main Flow:**
1. User creates a new empty budget.
2. User selects a period and an overall spending limit.
3. User creates spending categories (e.g., Food, Travel, Entertainment).
4. User assigns a spending limit specific to each category.
5. System saves the budget.
6. System displays all the limits.
7. User can view, edit, or delete the overall budget and/or its categories.

### Use Case #2: Record & Categorize Transactions

**Main Flow:**
1. User creates a new empty transaction.
2. User enters its amount, date, type (income/expense), and category.
3. System validates the transaction.
4. System saves the transaction.
5. System updates the user's financial summary and relevant budget totals.
6. User can view, edit, or delete existing transactions.

### Use Case #3: Analyze Spending Habits

**Main Flow:**
1. User selects a period to analyze.
2. System retrieves the transactions recorded during that period.
3. System calculates total income, total expenses, and remaining budget.
4. System breaks down expenses by category.
5. System displays the results through summaries and charts.

### Use Case #4: Set & Track Savings Goals

**Main Flow:**
1. User creates a new empty savings goal.
2. User gives it a title (e.g., "Save for GTA 6"), as well as a target amount and date.
3. User optionally enters an initial saved amount.
4. System saves the goal and calculates the remaining amount.
5. User updates their savings progress as time goes by.
6. System displays progress toward the target.
7. User can view, edit, or delete existing savings goals.

## Entities

- `Budget`
- `BudgetCategory`
- `Transaction`
- `TransactionType`
- `SavingsGoal`
- `SavingsContribution`

### Budget

```java
public class Budget {

    private String name;
    private LocalDate startDate;
    private LocalDate endDate;
    private double spendingLimit;
    private List<BudgetCategory> categories;

}
```

### BudgetCategory

```java
public class BudgetCategory {

    private String name;
    private double spendingLimit;

}
```

### Transaction

```java
public class Transaction {

    private double amount;
    private LocalDate date;
    private TransactionType type;
    private BudgetCategory category;

}
```

### TransactionType

```java
public enum TransactionType {
    INCOME,
    EXPENSE
}
```

### SavingsGoal

```java
public class SavingsGoal {

    private String title;
    private double targetAmount;
    private LocalDate targetDate;
    private List<SavingsContribution> contributions;

    public double getSavedAmount() {
        return contributions.stream()
                .mapToDouble(SavingsContribution::getAmount)
                .sum();
    }

    public double getRemainingAmount() {
        return Math.max(0, targetAmount - getSavedAmount());
    }

    public double getProgressPercentage() {
        if (targetAmount <= 0) {
            return 0;
        }

        return Math.min(100.0,
                (getSavedAmount() / targetAmount) * 100);
    }

}
```

### SavingsContribution

```java
public class SavingsContribution {

    private double amount;
    private LocalDate date;

}
```

## Pages

- **Dashboard:** Overview of total income, expenses, remaining budget, and goal progress.
- **Budgeting:** Create, edit, and delete budgets and spending categories.
- **Transactions:** Add, edit, delete, and filter transactions.
- **Visual Analytics:** Charts showing spending by category and over time.
- **Savings Goals:** Add, edit, delete, and filter financial goals.

## RICHARD: Recipe Creator and Nutrition Tracker

External API: USDA Food Data Central API (https://fdc.nal.usda.gov/api-guide/)

The application will focus on three main functionalities:
1. Recipe Creation: Create and edit recipes by selecting ingredients, specifying quantities, and providing preparation instructions.
2. Nutrition Calculation: Automatically retrieve nutritional information for ingredients and calculate the total nutritional value of recipes.
3. Nutrition Tracking: Log meals and monitor daily nutrition against customizable nutrition goals.

## Use Cases
Use Case 1 – Create a Recipe; User creates and saves a recipe containing ingredients and preparation instructions.\
User Story – Create and Manage Recipes, Search Ingredients and Calculate Nutrition

Main Flow:
1. User navigates to the daily nutrition tracker.
2. User selects a meal category (breakfast, lunch, dinner, or snack).
3. User chooses a saved recipe or searches for an individual food item.
4. User specifies the quantity or number of servings consumed.
5. Application retrieves the nutritional information if necessary and calculates the nutritional values based on the consumed quantity.
6. Application adds the food item to the selected meal category.
7. Application displays the updated totals alongside the user's daily nutritional goals.


Use Case 2 – Track Daily Nutrition; User logs a meal and views their accumulated daily nutritional intake.\
User Story – Track nutrition over time in order to monitor progress and maintain consistency

Main Flow:
1. User navigates to the daily nutrition tracker and selects a meal category (breakfast, lunch, dinner, or snack).
2. User chooses a saved recipe or searches for an individual food item.
3. User specifies the quantity or number of servings consumed.
4. Application retrieves the nutritional information if necessary and calculates the nutritional values based on the consumed quantity.
5. Application adds the food item to the selected meal category and updates the user's daily nutritional totals.
6. The application displays the updated totals alongside the user's daily nutritional goals.


Use Case 3 – Set and Monitor Nutritional Goals; user establishes nutritional targets and monitors their progress.\
User Story – I want to establish daily nutritional goals so that I can compare my actual food intake against my personal targets.

Main Flow:
1. User navigates to the nutritional goals section.
2. Application displays the current nutritional targets.
3. User enters their desired daily calorie, protein, carbohydrate, and fat goals and saves their goals.
4. Application compares the user's daily nutritional intake against these targets and displays the amount consumed and the amount remaining for each nutrient.
5. User can revisit the section to monitor their progress throughout the day.

Use Case 4 – Edit or Delete a Recipe; Use Case 4 – Copy, Edit or Delete a Recipe\
User Story - I want to edit the recipe's I've created or create an alternative version of an existing recipe

Main Flow:
1. User navigates to their saved recipes and selects a recipe.
2. Application displays its ingredients, instructions, and nutritional information.
3. User selects Copy, Edit or Delete.
4. If editing, the user modifies the ingredients, quantities, or instructions.
5. Application recalculates the nutritional information and saves the updated recipe.

## Entities
Entity 1 – User
Represents an individual using the application.

Entity 2 – Recipe
Represents a recipe created and saved by a user.

Entity 3 – Ingredient
Represents an individual food item included in a recipe or food log.

Entity 4 – NutritionInfo
Represents the nutritional composition of a food item, recipe, or meal.

Entity 5 – FoodLog
Represents a user's recorded food consumption for a particular day.

Entity 6 – NutritionGoals
Represents the user's daily nutritional targets.

##API Usage
API Name: USDA FoodData Central API

Documentation: https://fdc.nal.usda.gov/api-guide/

The API will primarily be used through two endpoints:
1. Food Search Endpoint
GET /fdc/v1/foods/search
- Allows users to search for ingredients by entering a food name or keyword.
- Returns a list of matching food items.
- Provides information such as the food description, FDC ID, and available nutrient information.
- Allows users to select the appropriate ingredient from the search results.
Example: When a user searches for "Chicken Breast", the app retrieves matching food items and displays them for selection.

2. Food Details Endpoint
GET /fdc/v1/food/{fdcId}
- Retrieves detailed nutritional information for a specific food item.
- Uses the food item's unique FDC ID obtained from the search results.
- Returns nutrient information such as calories, protein, carbohydrates, and fats.
- Allows the application to calculate nutritional values based on the quantity of each ingredient.
