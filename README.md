# x62-data-challenge-student-pathways

## Part1

### Data quality: For each feature (column), what is the data type? Is there any missing data?

    Column DISTRICT_TYPE has type object, contains 0 empty cells
    Column DISTRICT_NAME has type object, contains 0 empty cells
    Column DISTRICT_CODE has type float64, contains 2745 empty cells
    Column ACADEMIC_YEAR has type object, contains 0 empty cells
    Column DEMO_CATEGORY has type object, contains 0 empty cells
    Column STUDENT_POPULATION has type object, contains 0 empty cells
    Column AWARD_CATEGORY has type object, contains 0 empty cells
    Column WAGE_YEAR1 has type float64, contains 0 empty cells
    Column WAGE_YEAR2 has type float64, contains 0 empty cells
    Column WAGE_YEAR3 has type float64, contains 0 empty cells
    Column WAGE_YEAR4 has type float64, contains 0 empty cells
    17960 of 20705 lines is complete

DISTRICT_TYPE, DISTRICT_NAME, ACADEMIC_YEAR, DEMO_CATEGORY, STUDENT_POPULATION, AWARD_CATEGORY have type string.  
DISTRICT_CODE, WAGE_YEAR1, WAGE_YEAR2, WAGE_YEAR3, WAGE_YEAR4 have type float.  
DISTRICT_CODE contains missing cells.

### Range: What are the unique values for each categorical column? What is the range of values of the numeric columns? Are the numeric column values normally distributed?

I consider DISTRICT_CODE as categorical value even though it is a float.

#### Categorical column unique values

    Column: DISTRICT_TYPE
        All
        Legislative District
        School District
    Column: DISTRICT_NAME
        ABC Unified
        Acalanes Union High
        Acton-Agua Dulce Unified
        Adelanto Elementary
        Alameda County Office of Education
        Alameda Unified
        Albany City Unified
        Alhambra Unified
        All
        Alpaugh Unified
        Alpine County Office of Education
        Alta Vista Elementary
        Alvord Unified
        Amador County Office of Education
        Amador County Unified
        Anaheim Union High
        Anderson Union High
        Anderson Valley Unified
        Antelope Valley Union High
        Antioch Unified
        Apple Valley Unified
        Arcadia Unified
        Arcata Elementary
        Arena Union Elementary
        Armona Union Elementary
        Aromas - San Juan Unified
        Assembly District 1
        Assembly District 10
        Assembly District 11
        Assembly District 12
        [662 more unique values...]
    Column: DISTRICT_CODE
        110017.0
        161143.0
        161168.0
        161200.0
        161259.0
        175101.0
        461432.0
        661622.0
        710074.0
        761663.0
        761721.0
        761739.0
        861820.0
        961838.0
        1010108.0
        1062265.0
        1062364.0
        1062547.0
        1073999.0
        1075275.0
        1075598.0
        1162661.0
        1262901.0
        1262927.0
        1410140.0
        1510157.0
        1573742.0
        1610165.0
        1663875.0
        1663958.0
        [542 more unique values...]
    Column: ACADEMIC_YEAR
        2018-2019
    Column: DEMO_CATEGORY
        All
        Foster Status
        Gender
        Homeless Status
        Race
    Column: STUDENT_POPULATION
        All
        American Indian or Alaska Native
        Asian
        Black or African American
        Did Not Experience Homelessness in K-12
        Experienced Homelessness in K-12
        Female
        Foster Youth
        Hispanic or Latino
        Male
        Native Hawaiian or Other Pacific Islander
        None Reported
        Not Foster Youth
        Two or More Races
        White
    Column: AWARD_CATEGORY
        Associate Degree
        Bachelor's Degree - Did Not Transfer
        Bachelor's Degree - Transferred
        Community College Certificate

#### Numeric column ranges

    WAGE_YEAR1: 0.0 - 97993.000000
    WAGE_YEAR2: 0.0 - 132847.000000
    WAGE_YEAR3: 0.0 - 146728.000000
    WAGE_YEAR4: 0.0 - 153910.000000

#### Numeric column normal distribution check

With such amount of zeros clearly not.  
After removing lines with 4 wage values of zeros, it is still not normal distribution.

### Semantics: What is the meaning of the columns? Are any columns related to other columns? (If so, how?)

ACADEMIC_YEAR: Unclear whether it is academic year when the student graduated or when the student enrolled.
AWARD_CATEGORY: Category of award the student earned.  
WAGE_YEAR1, WAGE_YEAR2, WAGE_YEAR3, WAGE_YEAR4: Wage of a student after graduation in respective years.  
The following columns related to another.  
DISTRICT_TYPE describes whether the value at DISTRICT_NAME and DISTRICT_CODE is the district of student or that of the
school.  
DEMO_CATEGORY describes the aspect of demographical partition at STUDENT_POPULATION.

### Which demographic shows the highest WAGE_YEAR3? Which demographic shows the lowest WAGE_YEAR3?

Those reported none has the lowest WAGE_YEAR3.  
Those reported All has the highest WAGE_YEAR3.

### Are there any people with negative wage trends? Describe these people by their demographics.

Lines that has WAGE_YEAR3 less than WAGE_YEAR2 or WAGE_YEAR2 less than WAGE_YEAR1 has STUDENT_POPULATION of these

    STUDENT_POPULATION
    All                                        46
    Not Foster Youth                           36
    Male                                       34
    Did Not Experience Homelessness in K-12    16
    Female                                     15
    White                                      11
    Hispanic or Latino                          9
    Asian                                       6
    Experienced Homelessness in K-12            4
    Black or African American                   2
    Two or More Races                           1

### Are there any people with positive wage trends? Describe these people by their demographics.

Lines that has WAGE_YEAR3 greater than WAGE_YEAR2 or WAGE_YEAR2 greater than WAGE_YEAR1 has STUDENT_POPULATION of these

    STUDENT_POPULATION
    All                                          671
    Female                                       421
    Not Foster Youth                             419
    Male                                         410
    Hispanic or Latino                           293
    White                                        244
    Did Not Experience Homelessness in K-12      236
    Asian                                        174
    Experienced Homelessness in K-12              33
    Black or African American                     15
    Two or More Races                              9
    Foster Youth                                   2
    None Reported                                  2
    Native Hawaiian or Other Pacific Islander      2
    American Indian or Alaska Native               2

## Part 3

### Which features best predict the target outcome (WAGE_YEAR4)?

WAGE_YEAR3 does because it has the greatest coefficient in the trained model.

### What does your model say about the people or populations whose data is provided?

From the coefficient in the model I would claim: although STUDENT_POPULATION and AWARD_CATEGORY has significant
correlation with wage of all 4 years, the first 3 years already explains 4th year well enough and as long as we have
access to wages of first 3 years, we can predict the 4th year without them.   

### What features, if any, would you like to have had to make a better model?

Major of programs students participated. School rankings. Average GPA of students.


