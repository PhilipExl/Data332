# Load required libraries
library(ggplot2)
library(viridis)
library(hrbrthemes)
library(dplyr)
library(readxl)
library(tidyr)

# Resetting RStudio Environment
rm(list = ls())

# Set working directory
setwd('~/Desktop/College/Junior/Spring Semester/DATA-332/inclass/student_data')

# Read Excel data
df_course <- read_excel('Course.xlsx', .name_repair = 'universal' )
df_registration <- read_excel('Registration.xlsx', .name_repair = 'universal' )
df_student <- read_excel('Student.xlsx', .name_repair = 'universal' )

# Merge student and registration data
df_merged <- left_join(df_registration, df_student, by = "Student.ID")

# Merge with course data
df_merged <- left_join(df_merged, df_course, by = "Instance.ID")

# Convert Birth Date to Birth Year
df_merged$Birth_Year <- format(as.Date(df_merged$Birth.Date, format="%Y-%m-%d"), "%Y")

# Count students per major
df_major_count <- df_merged %>%
  group_by(Title) %>%
  summarise(Num_Students = n())

# Grouped bar chart for majors
ggplot(df_major_count, aes(x = reorder(Title, -Num_Students), y = Num_Students, fill = Title)) +
  geom_bar(stat = "identity") +
  labs(title = "Number of Students Per Major",
       x = "Major",
       y = "Number of Students") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  scale_fill_brewer(palette = "Set2")

# Extract birth year and count students
df_birth_year <- df_merged %>%
  group_by(Birth_Year) %>%
  summarise(Num_Students = n())

# Grouped bar chart for birth year
ggplot(df_birth_year, aes(x = as.factor(Birth_Year), y = Num_Students, fill = as.factor(Birth_Year))) +
  geom_bar(stat = "identity") +
  labs(title = "Number of Students by Birth Year",
       x = "Birth Year",
       y = "Number of Students") +
  theme_minimal() +
  scale_fill_brewer(palette = "Paired")

# Summarize total cost by major and payment plan
df_cost <- df_merged %>%
  group_by(Title, Payment.Plan) %>%
  summarise(Total_Cost = sum(Total.Cost, na.rm = TRUE), .groups = "drop")

# Grouped bar chart for total cost per major
ggplot(df_cost, aes(x = Title, y = Total_Cost, fill = Payment.Plan)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(title = "Total Cost Per Major (Segmented by Payment Plan)",
       x = "Major",
       y = "Total Cost") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  scale_fill_brewer(palette = "Dark2")

# Summarize total balance due by major and payment plan
df_balance <- df_merged %>%
  group_by(Title, Payment.Plan) %>%
  summarise(Total_Balance_Due = sum(Balance.Due, na.rm = TRUE), .groups = "drop")

# Grouped bar chart for balance due per major
ggplot(df_balance, aes(x = Title, y = Total_Balance_Due, fill = Payment.Plan)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(title = "Total Balance Due Per Major (Segmented by Payment Plan)",
       x = "Major",
       y = "Total Balance Due") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  scale_fill_brewer(palette = "Pastel1")

# Print key insights
cat("Insights from the Data:\n")

# Top 3 Majors by Enrollment
top_majors <- df_major_count %>% arrange(desc(Num_Students)) %>% head(3)
print(top_majors)

# Most common birth year
common_birth_year <- df_birth_year %>% arrange(desc(Num_Students)) %>% head(1)
print(common_birth_year)

# Highest total cost major
highest_cost <- df_cost %>% arrange(desc(Total_Cost)) %>% head(1)
print(highest_cost)

# Major with the highest balance due
highest_balance <- df_balance %>% arrange(desc(Total_Balance_Due)) %>% head(1)
print(highest_balance)

# Image display:
<p> This chart shows four grouped bar charts of student enrollment, costs and payments</p>

<img src="~/Desktop/College/Junior/Spring Semester/DATA-332/inclass/student_data/studentData.png" height = 250 width = 400>
