# Kickstarter Projects Analysis Tool

## Overview

The Kickstarter Projects Analysis Tool is a C++ program designed to analyze Kickstarter project data from a CSV file. It provides insights into various aspects of the projects, including success rates, top-funded projects, time trends, and more. The tool uses several statistical and analytical methods to categorize and display data based on user-defined criteria.

## Features

1. **Success Rates Analysis:**
   - By Country
   - By Main Category
   - By Category
   - By Backers
   - By Goal
   - By Project Numbers

2. **Top Funded Projects:**
   - By Countries
   - By Categories
   - By Main Category
   - By Currency

3. **Time Trends Analysis:**
   - Overall Trends
   - Top 20 Categories Over Years
   - Top 10 Countries Over Years
   - Top 5 Main Categories Over Years

## Requirements

- C++ compiler (e.g., GCC, Clang)
- Standard C++ library
- A CSV file with Kickstarter project data

## Data File

The program reads data from a CSV file. Ensure that the CSV file follows the structure:

- `id`
- `name`
- `category`
- `mainCategory`
- `currency`
- `deadline`
- `goal`
- `launched`
- `pledged`
- `state`
- `backers`
- `country`
- `usdPledged`
- `usdPledgedReal`
- `usdGoalReal`

### Example File Path

Modify the path in the code to point to your CSV file on line 958:

```cpp
ifstream file("/Path/to/dsaProjectData.csv");
```

## Usage

1. **Menu Options:**

   - **Success Rates**: Analyze success rates based on various factors.
   - **Top Funded Projects**: Find top-funded projects by country, category, main category, or currency.
   - **Time Trends**: Analyze trends over time, including top categories, countries, and main categories by year.
   - **Exit**: Exit the program.

2. **Submenu Options:**

   - **Success Rates Menu:**
     - By Country
     - By Main Category
     - By Category
     - By Backers
     - By Goal
     - By Project Numbers

   - **Top Funded Projects Menu:**
     - By Countries
     - By Categories
     - By Main Category
     - By Currency

   - **Time Analysis Menu:**
     - Overall Trends
     - Top 20 Categories
     - Top 10 Countries
     - Top 5 Main Categories

## Functions

- **topFundedProjectsByMainCategory()**: Displays the top-funded projects for each main category.
- **topFundedProjectsByCurrency()**: Displays the top-funded projects by currency.
- **analyzeTimeTrends()**: Analyzes and displays trends over time, including average pledged amounts, most popular categories, and more.
- **bubbleSort2()**: Sorts a vector of pairs using bubble sort.
- **top20CategoriesForYear()**: Finds and displays the top 20 most popular categories for a specified year.
- **top10CountriesForYear()**: Finds and displays the top 10 countries for a specified year.
- **top5MainCategoriesForYear()**: Finds and displays the top 5 main categories for a specified year.

## Memory Management

The `deleteVectors()` function is used to clear vectors of KickstarterProject objects to free memory. Make sure to call this function before exiting the program to ensure proper cleanup.

## Error Handling

The program handles various errors, including:

- Invalid pledged or goal amounts
- Unknown project states
- Errors opening the CSV file

Error messages are displayed to the user for troubleshooting.
