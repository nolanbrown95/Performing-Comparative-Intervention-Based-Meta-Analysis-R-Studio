# Performing-Comparative-Intervention-Based-Meta-Analysis-R-Studio
# Load metafor package
library(metafor)

# Load dataset
data(dataset_name)

# Define the outcome measure
outcome <- "outcome_measure"

# Filter the dataset to include only the two interventions of interest
intervention1 <- "intervention_name_1"
intervention2 <- "intervention_name_2"
dataset_interventions <- subset(dataset_name, intervention %in% c(intervention1, intervention2))

# Calculate effect sizes for each study using the outcome measure
effect_sizes <- escalc(measure = "OUTCOME_MEASURE", data = dataset_interventions, append = TRUE)

# Create a forest plot to visualize the effect sizes
forest(effect_sizes, slab = dataset_interventions$study, comb.fixed = FALSE)

# Conduct a meta-analysis using a random effects model
meta_analysis <- rma(yi, vi, data = effect_sizes, method = "REML")

# Print the summary of the meta-analysis
summary(meta_analysis)

# Conduct a subgroup analysis to compare the two interventions
subgroup_analysis <- rma(yi, vi, mods = ~ intervention, data = effect_sizes, method = "REML")

# Print the summary of the subgroup analysis
summary(subgroup_analysis)
In the above code, you would need to replace "dataset_name" with the name of your dataset, "outcome_measure" with the name of the outcome measure you are interested in, "intervention_name_1" and "intervention_name_2" with the names of the two interventions you want to compare, and adjust any other relevant variables to your specific analysis.

The subset() function is used to filter the dataset to only include studies that used the two interventions of interest. The escalc() function is used to calculate effect sizes for each study using the specified outcome measure. The forest() function is used to visualize the effect sizes using a forest plot.

The rma() function is used to conduct both the meta-analysis and subgroup analysis, using a random effects model with restricted maximum likelihood estimation (REML). The summary() function is used to print the summary results of each analysis.

Note: this is for random effects model analysis only. To use a mixed effects analysis, you must first determine whether it is indicated. This depends on heterogeneity across studies. See "Mixed-Versus-Random-Effects-When-To-Use" for more information.
