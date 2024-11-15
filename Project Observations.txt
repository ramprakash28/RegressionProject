Project Observations

Power Usage Reg project
Your R model summary output confirms the results of the regression model for Usage_kWh as the dependent variable. Here’s a summary of the findings:
Key Results:
Intercept: 3.38, indicating the baseline Usage_kWh when all predictors are zero.
Lagging_Reactive_kVarh: 0.188, with a highly significant p-value (< 2e-16), showing a positive relationship between Lagging_Reactive_kVarh and Usage_kWh.
CO2_tons: 1877, also highly significant (p < 2e-16), suggesting that higher CO2 emissions are strongly associated with increased energy usage.
WeekStatusWeekend: -0.223, with a significant p-value (0.000295), indicating slightly lower energy usage on weekends compared to weekdays.
Model Fit:
Multiple R-squared: 0.9783, meaning the model explains approximately 97.8% of the variance in Usage_kWh.
F-statistic: 5.271e+05 with a p-value < 2.2e-16, indicating the overall model is statistically significant.
This output supports the conclusion that all chosen predictors contribute significantly to explaining the variance in energy usage, with CO2_tons showing the largest effect size. Let me know if you need further interpretation or additional analysis steps!

Here’s an interpretation of each element in your regression model based on the R output:
### 1. **Significance Testing and P-Values**
   - **Intercept**: The p-value is less than \(2 \times 10^{-16}\), indicating it is highly significant. This suggests the baseline energy usage (`Usage_kWh`) is significantly different from zero when all other predictors are at zero.
   - **Lagging_Reactive_kVarh**: The p-value is less than \(2 \times 10^{-16}\), showing strong statistical significance. This means that the relationship between `Lagging_Reactive_kVarh` and `Usage_kWh` is highly reliable.
   - **CO2_tons**: Also with a p-value less than \(2 \times 10^{-16}\), this predictor is highly significant. This implies a robust association between CO2 emissions and energy usage.
   - **WeekStatus (Weekend)**: The p-value for the weekend category is 0.000295, which is significant at conventional levels (e.g., 0.05). This indicates that the difference in energy usage between weekdays and weekends is statistically significant.

### 2. **Confidence Intervals (Interpretation)**
   Although specific confidence intervals are not displayed in the summary, the standard errors provided allow us to estimate the intervals around each coefficient. For instance, with the small standard errors, we can infer narrow confidence intervals, reinforcing the reliability of the estimated coefficients.

### 3. **Interpretation of Regression Coefficients**
   - **Intercept (3.38)**: This represents the estimated `Usage_kWh` when all other predictors are zero. Practically, it’s the baseline energy consumption level, though not directly interpretable in the real-world context since CO2 and reactive power are rarely zero in operation.
   
   - **Lagging_Reactive_kVarh (0.188)**: For each additional unit increase in lagging reactive power (`Lagging_Reactive_kVarh`), the energy usage (`Usage_kWh`) increases by 0.188 kWh, assuming all other variables are constant. This implies that higher lagging reactive power is associated with greater energy consumption, possibly due to inefficiencies in power usage.
   - **CO2_tons (1877)**: For each additional ton of CO2 emissions, the energy usage increases by 1877 kWh, holding other factors constant. This large coefficient suggests a very strong association between emissions and energy usage, indicating that as production or operations increase (leading to higher CO2 output), energy consumption rises correspondingly.
   - **WeekStatusWeekend (-0.223)**: Being a categorical variable, `WeekStatus` compares weekends to weekdays. The negative coefficient of -0.223 means that energy usage is about 0.223 kWh lower on weekends than on weekdays, holding other variables constant. This could reflect reduced industrial activity or operations on weekends.

### 4. **Goodness-of-Fit Metrics**
   - **R-squared (0.9783)**: The model explains approximately 97.8% of the variance in `Usage_kWh`, indicating a very good fit. This high value suggests that the selected predictors effectively capture the variations in energy usage.
   
   - **Adjusted R-squared (0.9783)**: The adjusted R-squared is also 0.9783, almost identical to R-squared. This indicates that the model doesn’t suffer from overfitting despite multiple predictors, as adjusted R-squared accounts for the number of predictors in the model.
  
   Overall, the high R-squared and adjusted R-squared values indicate that the model has a strong explanatory power for `Usage_kWh`, and the significant p-values for each predictor imply that they are all meaningful contributors to the model.
The Adjusted R-squared is slightly lower than the R-squared because it accounts for the number of predictors in the model. R-squared tends to increase with the addition of more predictors, regardless of whether they improve the model's predictive power. In contrast, adjusted R-squared adjusts for the number of predictors, providing a more realistic measure of the model's fit by penalizing the inclusion of non-informative predictors.
In your case, the adjusted R-squared is close to the R-squared, indicating that most predictors in your model are likely informative. If the difference were large, it could suggest that some predictors aren’t significantly contributing to explaining the variability in the response variable.
R-squared will always be higher (or at least the same) as adjusted R-squared because R-squared is purely based on the variance explained by the model.

Assumptions and Potential Issues:
1.The results from the **Durbin-Watson test** indicate the following:
- **Durbin-Watson Statistic (DW)**: 1.0634, which is significantly below 2. This suggests the presence of positive autocorrelation in the residuals.
- **p-value**: Less than \(2.2 \times 10^{-16}\), which is extremely low. This provides strong evidence against the null hypothesis of no autocorrelation, indicating that autocorrelation is indeed present.
### Interpretation and Implications
The presence of positive autocorrelation means that residuals from one observation are correlated with residuals from the next. This violates the assumption of independent errors in linear regression, which can lead to underestimated standard errors, overestimated t-statistics, and potentially misleading inferences about predictor significance.
### Next Steps
To address autocorrelation, you might consider:
1. **Time-Series Models**: If the data is time-ordered, a time-series model like ARIMA could better capture the temporal dependencies.
2. **Generalized Least Squares (GLS)**: GLS can be used to adjust for autocorrelation within a regression framework.
3. **Including Lagged Variables**: Sometimes adding lagged versions of the response or predictors helps in capturing the autocorrelation structure.

2.The primary plot to check for heteroscedasticity in a regression model is the Residuals vs. Fitted plot.
Interpretation:
Homoscedasticity (constant variance): If the residuals are randomly scattered around zero with no visible pattern, this suggests homoscedasticity (the assumption of constant variance holds).
Heteroscedasticity (non-constant variance): If you observe a pattern, such as a funnel shape where residuals become larger or smaller as fitted values increase, this indicates heteroscedasticity
The Residuals vs. Fitted plot you've shared shows signs of heteroscedasticity:
Pattern in Residuals: The plot shows a distinct pattern where residuals are not evenly spread around zero. In particular, there is a cone-shaped or funnel pattern, with residuals exhibiting larger variance at lower fitted values and tighter clustering around zero as fitted values increase.
Interpretation:
This funnel shape suggests that the residual variance is not constant, a classic indication of heteroscedasticity.
In practical terms, this means that the model’s predictions are less accurate for some fitted values compared to others, violating the homoscedasticity assumption.

3.
Interpretation of VIF:
VIF = 1: No correlation with other variables.
VIF > 5: Indicates moderate multicollinearity, often considered a potential problem.
VIF > 10: Suggests high multicollinearity, and you may need to consider removing or combining predictors.
Based on the VIF values we got:
Lagging_Reactive_kVarh: VIF = 4.78
CO2_tons: VIF = 4.69
WeekStatus: VIF = 1.11
Interpretation
Lagging_Reactive_kVarh and CO2_tons:
Both have VIF values below 5, which indicates moderate multicollinearity but not at a level that typically causes concern.
Although these VIF values are higher than 1, they do not exceed 5, so they do not indicate problematic multicollinearity.
WeekStatus:
With a VIF of 1.11, this predictor shows no signs of multicollinearity.
Conclusion
The VIF values do not suggest any severe multicollinearity in your model. All values are within acceptable ranges, so there is no need to take corrective actions (like removing variables or using techniques like PCA or ridge regression).
Your model's multicollinearity is manageable, and the predictors are independently contributing to the model without significant overlap. Let me know if you need further clarification or additional diagnostics!

4.The updated plot shows that all Cook’s Distance values are well below the threshold of 0.5 and 1, with no points approaching these levels. This indicates that no observations in your dataset are highly influential based on Cook’s Distance.
Interpretation
Since none of the points exceed a Cook's Distance of 0.5 or 1, there are no observations that disproportionately affect the model's coefficients.
This suggests that the model is stable and not overly influenced by any single observation.
Conclusion
No action is needed regarding influential points, as the data does not contain points with high Cook's Distance values. This is a positive outcome, indicating that your model's coefficients are robust to individual observations.
The output shows that no observations have Cook's Distance values greater than 0.5 or 1, as indicated by the empty results for both influential_points and highly_influential_points. This confirms that:
No influential points exceed the commonly used thresholds (0.5 or 1), meaning that there are no observations with a disproportionately large influence on the regression model.
Interpretation
This result suggests that your model is stable and not unduly affected by any individual data points. This is generally a positive indication for model robustness, as it implies that your regression estimates are not skewed by any particular observation.
Let me know if you'd like to proceed with additional diagnostics or need further assistance with interpreting or refining the model!

Option 1: Log Transformation of the Response Variable

To address the heteroscedasticity in our model, we explored two commonly used remediation techniques: **log transformation** and **Weighted Least Squares (WLS)**.

1. **Log Transformation**: 
   - We first applied a log transformation to the response variable, `Usage_kWh`, to stabilize variance and address heteroscedasticity. Since `Usage_kWh` contained one negative value, we opted to filter out this observation rather than adding a constant (e.g., 0.1) to make it positive.
   - This decision was based on the minimal impact of excluding a single value, ensuring a simpler interpretation of the model without arbitrary adjustments. 
   - After applying the log transformation, we observed an improvement in the model’s fit, with a reduction in heteroscedasticity and stabilized variance across residuals. However, there was still minor residual heteroscedasticity present.

2. **Weighted Least Squares (WLS)**:
   - We then applied the WLS approach, which assigns weights to observations based on the variance of residuals, allowing us to retain all data points without transformation.
   - The WLS model further improved the model's fit by effectively addressing heteroscedasticity, yielding consistent variance in residuals and improved normality in residual distribution.
   - Given these improvements and the retention of data without transformation, Weighted Least Squares (WLS) appears to be an effective and suitable approach for our analysis.

---

This summary captures the rationale and outcomes of each technique, highlighting the strengths of the WLS approach as the preferred solution in this case. Let me know if you'd like further adjustments!

Based on the output from the log-transformed model, here’s a breakdown of the results and the diagnostics:
Model Summary
Coefficients:
The estimates for Lagging_Reactive_kVarh, CO2_tons, and WeekStatusWeekend are all statistically significant with very low p-values (< 2e-16).
The interpretation of coefficients is now in terms of log-transformed Usage_kWh. For example, a 1-unit increase in CO2_tons is associated with an increase in the log of Usage_kWh by approximately 83.98, which corresponds to a multiplicative effect on the original Usage_kWh.
Goodness-of-Fit:
Multiple R-squared: 0.8756
Adjusted R-squared: 0.8756
These values indicate that about 87.56% of the variability in the log-transformed Usage_kWh is explained by the model, which is quite high.
Diagnostic Plots
Residuals vs. Fitted Plot:
The funnel shape that previously indicated heteroscedasticity has been reduced but is still slightly visible. This suggests that the log transformation helped address heteroscedasticity but did not completely eliminate it.
The slight pattern remaining could be due to other non-linear relationships or additional underlying factors.
Q-Q Plot:
The Q-Q plot shows that most residuals follow a normal distribution, but there are deviations at both tails (particularly on the right). This is common in large datasets and might not be a significant issue if most points align closely with the line.
Scale-Location Plot:
The Scale-Location plot indicates improved homoscedasticity compared to the original model, with residuals more evenly spread across fitted values.
The residuals show a more consistent variance along the fitted values, though some deviation still exists for very high values.
Residuals vs. Leverage Plot:
This plot does not show any points with Cook's Distance close to 1, indicating that there are no highly influential points.
Conclusion and Recommendations
The log transformation has generally improved the model’s fit by addressing heteroscedasticity and stabilizing variance across residuals.
Remaining Minor Heteroscedasticity: There’s still a slight pattern in the residuals, but it is much reduced. This might be acceptable depending on the analysis context. Alternatively, you could try Weighted Least Squares as an additional step if complete homoscedasticity is critical.
Interpretation: Since the model is now in a log-linear form, interpret coefficients in terms of percentage changes in the original Usage_kWh.

