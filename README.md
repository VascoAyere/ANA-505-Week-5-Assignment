# Obesity Ghana analysis
# Vasco Ayere Avoka
# 2024-06-18


# Load packages ----
if(!require(pacman)) install.packages("pacman")
pacman::p_load(
  tidyverse,
  janitor,
  inspectdf,
  DataExplorer,
  here,  # new package we will use soon
)

# Load data ----
obesity_ghana <- read_csv(here("data/2012GHA_seniorhigh_public_use.csv"))


library(ggplot2)

#  Plotting the distribution of the 'Age and Sex' 
ggplot(obesity_ghana, aes(x = Sex,)) +
  geom_bar() +
  theme_minimal() +
  labs(title = "Distribution of Age and Sex",
       x = "Sex",
       y = "Age")

# Create a scatterplot of Age versus Weight
Weight_Height_Scatte <- ggplot(obesity_ghana, aes(x = Weight, y = Height)) +
  geom_point() +
  theme_minimal() +
  labs(title = "Scatterplot of Age vs. obese",
       x = "Weight",
       y = "Height")
Weight_Height_Scatter
ggsave(Weight_Height_Scatter, filename = ("outputs/obesity_distribution_plot.jpeg") )



# Create a scatterplot of Height versus Weight
Weight_Height_Scatter <- ggplot(obesity_ghana, aes(x = Weight, y = Height)) +
  geom_point() +
  theme_minimal() +
  labs(title = "Scatterplot of Height vs. Weight",
       x = "Weight",
       y = "Height")
Weight_Height_Scatter
ggsave(Weight_Height_Scatter, filename =("outputs/height_weight_plot.jpeg"))




# Distribution of Age and Sex
Age_Sex_plot <- ggplot(obesity_ghana, aes(x=Age, fill=factor(Sex))) +
  geom_bar(position='dodge') +
  scale_fill_manual(values=c("#66c2a5", "#fc8d62"), labels=c('Male', 'Female')) + 
  labs(title='Distribution of Students by Age and Sex', x='Age', y='Freq', fill='Sex') +
  theme_minimal(base_size = 15)

ggsave(Age_Sex_plot, filename =("outputs/age_sex_barchart.jpeg"))



# Bar chart for Days Active (60+ minutes) in the Past Week
bar_days_active <- ggplot(obesity_ghana, aes(x=`days active 6o mins plus 7 past days`)) +
  geom_bar(fill="#e41a1c") + # 'Set1' color
  labs(title='Days Active for 60+ Minutes in the Past Week', x='Days Active', y='Number of students') +
  scale_x_continuous(breaks=1:8)+
theme_minimal(base_size = 15)
ggsave(bar_days_active, filename = ("outputs/bar_days_active_bar.jpeg"))


# Bar chart for Days Walked or Biked to School in the Past Week

bar_walked_biked <- ggplot(obesity_ghana, aes(x=`walk or bike to school past 7 days`)) +
  geom_bar(fill="#e41a1c") + # 'Set1' color
  labs(title='Days Walked or Biked to School in the Past Week', x='Days Walked/Biked', y='Number of student') +
  scale_x_continuous(breaks=1:8) +
  theme_minimal(base_size = 15)
ggsave(bar_walked_biked, filename = ("outputs/bar_walked_biked_bar.jpeg"))
