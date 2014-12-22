
```R
# Merge two dataframes on a specified column in each dataframe
merged_data <- merge(country_data, gdp_data, by.x = "CountryCode", by.y = "X", all = FALSE)

# Order/sort the data frame based on a column in descending order
merged_date_sorted <- arrange(merged_data, desc(gdp_rank_num))

# Subset out the data frame rows where a column value has a certain value  => mean = 32.96667
q4_df <- merged_date_sorted[(merged_date_sorted$Income.Group == "High income: OECD"),]

# Subset out the data frame rows where a column value has a certain value  => mean = 91.91304
q4_df_b <- merged_date_sorted[(merged_date_sorted$Income.Group == "High income: nonOECD"),]

# Subset the merged data - getting two columns (variables)
q5_df <- merged_date_sorted[,c("gdp_rank_num","Income.Group")]
# 
q5_df_compcases <- q5_df[complete.cases(q5_df),]

# Add a column to the dataframe containing the quantile id of quantile breakdown of a numeric column (variable)
q5_df_compcases$gdp_quantile_id = cut(q5_df_compcases$gdp_rank_num, breaks = quantile(q5_df_compcases$gdp_rank_num, probs=seq(0,1, by=0.20)), include.lowest=TRUE)

# Create a "pivot table" of counts - how observations fall into classifications of two qualitative variables (Gender [M, F] vs. Marital Status [married, not married])
table(q5_df_compcases$Income.Gropu, q5_df_compcases$gdp_quantile_id)

q5_df_compcases[189, 3] <- as.factor("(1,48]")
```
