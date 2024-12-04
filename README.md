# justiceR

**justiceR** is an R package that provides tools for criminal justice data analysis, offering a range of functions to simplify and enhance data-driven insights in this field.

## Installation

You can install the development version of **justiceR** from GitHub using the `devtools` package:

``` r
# Install devtools if you haven't already
install.packages("devtools")

# Install justiceR from GitHub
devtools::install_github("mr4909/justiceR@develop")
```

## generate_codebook()

The `generate_codebook()` function is a tool for exploring and documenting your dataset. It generates a detailed codebook that provides descriptive statistics for each variable in your data frame. These statistics are particularly useful for understanding your data before performing more in-depth analyses.

**Key Features:**

-   Descriptive Statistics: Generate descriptive statistics for numeric, categorical, logical, and date variables.
-   Customization Options:
    -   Variable Descriptions: Provide custom descriptions for each variable to enhance clarity.
    -   Hide Sensitive Statistics: Conceal statistics for specific variables to protect sensitive information.
-   Top Categories Selection: Specify the number of top categories to display for categorical variables.
-   Flexible Output Formats: Output codebooks in `kable` format for easy integration into reports and documents.

``` r
library(justiceR)

# Example data frame
df <- data.frame(
  age = c(25, 30, 22, 40, NA, 35, 28),
  start_date = as.Date(c("2020-01-01", "2020-02-15", NA, "2020-03-10", "2020-04-20", "2020-05-25", "2020-06-30")),
  active = c(TRUE, FALSE, TRUE, FALSE, TRUE, NA, FALSE),
  crime_type = factor(c("Theft", "Assault", "Theft", "Fraud", "Assault", "Theft", "Robbery"))
)

# Generate codebook with metadata
generate_codebook(df)
```
This will create a well-organized codebook summarizing each variable:

- **Numeric Variables:** Statistics such as minimum, average, median, maximum, and standard deviation.
- **Categorical Variables:** The most frequent categories and their percentages.
- **Logical Variables:** Counts and percentages of TRUE and FALSE values.
- **Date Variables:** The earliest and latest dates in the dataset.

### Hiding Sensitive Statistics

Suppose you want to hide the statistics for the active variable to protect sensitive information:

``` r
generate_codebook(
  df, 
  hide_statistics = c("active")
)
```

**Output:** Statistics for the active variable will be replaced with "Hidden" in the codebook.

### Customizing Top Categories

By default, generate_codebook() displays the top 5 categories for categorical variables. You can adjust this number using the top_n parameter:

``` r
# Decrease the number of top categories displayed for the 'crime_type' variable
generate_codebook(
  df, 
  top_n = 2
)
```

**Output:** Up to 2 top categories for each categorical variable will be displayed. If a variable has fewer than the top_n categories, all categories will be shown.

### Adding Additional Columns

This produces a codebook that includes the descriptive statistics for each variable along with the metadata provided in extra_vars.

``` r
# Additional metadata
extra_vars <- data.frame(
  VariableName = c("age", "start_date"),
  Description = c("Age of the individual", "Date supervision began"),
  Notes = c("Collected from surveys", "Derived from administrative records")
)

# Generate codebook with metadata
generate_codebook(df, extra_vars = extra_vars, extra_key = "VariableName")
```

- extra_vars: A data frame containing metadata such as descriptions and notes about the variables in your dataset.  
- extra_key: The column in extra_vars that corresponds to the variable names in the dataset. In this example, it is VariableName.  


# License

This package is licensed under the GPL-3 license. See the LICENSE file for more details.

# Contact and Support

Developed by Mari Roberts. For questions, feedback, or to report issues, please contact [mroberts\@csg.org](mailto:mroberts@csg.org)

