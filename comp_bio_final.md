comp bio gorup final
================
Ethan Sharp
2025-11-11

- [ABSTRACT](#abstract)
- [BACKGROUND](#background)
- [STUDY QUESTION and HYPOTHESIS](#study-question-and-hypothesis)
  - [**Questions**](#questions)
  - [**Hypothesis**](#hypothesis)
  - [**Prediction**](#prediction)
  - [results](#results)
- [DISCUSSION](#discussion)
- [CONCLUSION](#conclusion)
- [REFERENCES](#references)

# ABSTRACT

# BACKGROUND

This dataset contains information about different health and lifestyle
factors that may influence heart attacks in the USA. It includes details
like age, cholesterol, blood pressure, and smoking habits, along with
outcomes like whether a heart attack occurred. The goal is to help
identify potential risks and trends that can lead to better heart health
awareness and prevention.

# STUDY QUESTION and HYPOTHESIS

## **Questions**

Does the gender, education level, and/or stress level an individual has
affect the probability of them getting a heart attack?

## **Hypothesis**

If an individual is male, has a higher level of education, and a higher
the stress level then we will see statistical significance with
correlation to having a heart attack because of how these factors affect
heart conditions over time.

## **Prediction**

An individual is male, has a higher level of education, and a higher the
stress level they will be more likely to have a heart attack at some
point in their life

\##**Methods** The database chosen for this study was the Kaggle
database, and the heart attack prediction set was the one chosen for
this study. It was chosen because it had enough entries for our purposes
and many variables to test. Once the variables were chosen, an excel
spreadsheet was created to hold all the data. Multiple linear regression
models were made testing variables against the outcomes of heart attack.
After all the variables were tested individually, they were then all
tested at the same time vs heart attack outcome to test for a
correlation between all of them.

## results

Stress Level vs HA (Violin Plot)

``` r
ggplot(heart_data, aes(x = Outcome, y = StressLevel, fill = Outcome)) +
  geom_violin(trim = FALSE, alpha = 0.7) +
  geom_boxplot(width = 0.1, fill = "white", alpha = 0.5) +
  labs(
    title = "Stress Levels by Heart Attack Outcome",
    x = "Heart Attack Outcome",
    y = "Stress Level (1–9)"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold"),
    legend.position = "none"
  )
```

Stress vs HA Alt (Ridge Plot)

``` r
library(ggplot2)
library(ggridges)

ggplot(heart_data, aes(x = StressLevel, y = Outcome, fill = Outcome)) +
  geom_density_ridges(alpha = 0.7, color = "black", scale = 1) +
  scale_fill_manual(values = c("No Heart Attack" = "skyblue", "Heart Attack" = "tomato")) +
  labs(
    title = "Distribution of Stress Levels by Heart Attack Outcome",
    x = "Stress Level (1–9)",
    y = "Heart Attack Outcome",
    fill = "Outcome"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold"),
    legend.position = "none",
    axis.title.y = element_text(face = "bold"),
    axis.title.x = element_text(face = "bold")
  )
```

Gender vs HA (Heat Map)

``` r
library(dplyr)
library(ggplot2)
library(viridis)  

# Summarize counts
gender_counts <- heart_data %>%
  group_by(Gender, Outcome) %>%
  summarise(count = n(), .groups = "drop")

#Heat map
ggplot(gender_counts, aes(x = Gender, y = Outcome, fill = count)) +
  geom_tile(color = "white", size = 0.8) +  # white borders between tiles
  geom_text(aes(label = count), color = "white", size = 6, fontface = "bold") +
  scale_fill_viridis(option = "C", direction = -1) +  # smooth and modern gradient
  labs(
    title = "Heart Attack Outcomes by Gender",
    x = "Gender",
    y = "Heart Attack Outcome",
    fill = "Count"
  ) +
  theme_minimal(base_size = 15) +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 20),
    axis.text = element_text(face = "bold", size = 14),
    axis.title = element_text(face = "bold", size = 16),
    legend.title = element_text(face = "bold", size = 14),
    legend.text = element_text(size = 12)
  )
```

Gender, Stress Level, and Education Level vs HA

``` r
library(ggplot2)

ggplot(heart_data, aes(
  x = EducationLevel,
  y = StressLevel,
  color = Outcome,       
  alpha = Outcome,  
  shape = Gender
)) +
  geom_jitter(width = 0.3, size = 4) +
  scale_alpha_manual(values = c("No Heart Attack" = .9, "Heart Attack" = 1)) +
  scale_shape_manual(values = c("Female" = 1, "Male" = 16)) +  # hollow vs filled
  scale_color_manual(values = c("No Heart Attack" = "lightblue3", "Heart Attack" = "indianred2")) + 
  labs(
    title = "Stress Levels by Education, Gender, and Heart Attack Outcome",
    x = "Education Level",
    y = "Stress Level (1–9)",
    color = "Heart Attack Outcome",
    alpha = "Heart Attack Outcome",
    shape = "Gender"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold")
  )
```

Education Level vs HA (Lollipop Graph)

``` r
library(dplyr)
library(ggplot2)

# Summarize counts
edu_counts <- heart_data %>%
  group_by(EducationLevel, Outcome) %>%
  summarise(count = n(), .groups = "drop")

# Fancy lollipop chart
ggplot(edu_counts, aes(x = EducationLevel, y = count, color = Outcome)) +
  geom_segment(aes(x = EducationLevel, xend = EducationLevel, y = 0, yend = count), linewidth = 1.2) +
  geom_point(size = 6) +
  scale_color_manual(values = c("No Heart Attack" = "skyblue", "Heart Attack" = "tomato")) +
  labs(
    title = "Heart Attack Outcomes by Education Level",
    x = "Education Level",
    y = "Count of Individuals",
    color = "Heart Attack Outcome"
  ) +
  theme_minimal(base_size = 14) +
  theme(plot.title = element_text(hjust = 0.5, face = "bold"))
```

# DISCUSSION

# CONCLUSION

# REFERENCES

<https://www.mybib.com/j/OceanicFertileGiraffe>
