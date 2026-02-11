# AI Audit Appendix (Assignment 04)

## Tool(s) Used
> Claude Haiku 4.5

## Task(s) Where AI Was Used
> Task 1: Implement a regression estimate using statsmodels.formula.api.ols

> Task 2: Write the model summary to the output file

> Task 3: Create a scatter plot with the regression

> Task 4: Print key results such as intercept, slope, and R²


## Prompt(s)
> Prompt 1: "uses statsmodels.formula.api.ols to estimate ret ~ x_var"

> Prompt 2: "write a string of the model summary to the output file"

> Prompt 3: "create a scatter plot with a regression line. reference script for labels"

> Prompt 4: "print the key results referenced in the script"


## Output Summary
> Output 1: 
    model = ols(f"ret ~ {x_var}", data=df).fit()
    return model

> Output 2:
        f.write(str(model.summary()))

> Output 3:
    df_clean = df[[x_var, 'ret']].dropna()
    
    # Create figure and axes
    fig, ax = plt.subplots(figsize=(10, 6))
    
    # Scatter plot
    ax.scatter(df_clean[x_var], df_clean['ret'], alpha=0.5, label='Observations')
    
    # Regression line
    intercept = model.params['Intercept']
    slope = model.params[x_var]
    x_range = np.array([df_clean[x_var].min(), df_clean[x_var].max()])
    y_pred = intercept + slope * x_range
    ax.plot(x_range, y_pred, 'r-', linewidth=2, label='Fitted Line')
    
    # Set axis limits to central data (2–98 percentiles)
    x_min, x_max = df_clean[x_var].quantile([0.02, 0.98])
    y_min, y_max = df_clean['ret'].quantile([0.02, 0.98])
    ax.set_xlim([x_min, x_max])
    ax.set_ylim([y_min, y_max])
    
    # Add title (include R²), xlabel, ylabel, legend
    ax.set_title(f"{title}\nR² = {model.rsquared:.4f}", fontsize=12)
    ax.set_xlabel(xlabel, fontsize=11)
    ax.set_ylabel("Annual Return", fontsize=11)
    ax.legend()
    ax.grid(True, alpha=0.3)
    
    # Save
    plt.savefig(output_path, dpi=300, bbox_inches='tight')
    plt.close()

> Output 4:
    # Extract parameters
    intercept = model.params['Intercept']
    slope = model.params[x_var]
    intercept_se = model.bse['Intercept']
    slope_se = model.bse[x_var]
    intercept_tstat = model.tvalues['Intercept']
    slope_tstat = model.tvalues[x_var]
    intercept_pval = model.pvalues['Intercept']
    slope_pval = model.pvalues[x_var]
    
    # Print coefficients with standard errors, t-stats, p-values
    print(f"\nIntercept (β₀):  {intercept:.6f}  (SE: {intercept_se:.6f})")
    print(f"                 t-stat: {intercept_tstat:.4f}  p-value: {intercept_pval:.4f}")
    print(f"\nSlope (β₁):      {slope:.6f}  (SE: {slope_se:.6f})")
    print(f"                 t-stat: {slope_tstat:.4f}  p-value: {slope_pval:.4f}")
    
    # Print fit statistics
    print(f"\nR²:              {model.rsquared:.4f}")
    print(f"Adjusted R²:     {model.rsquared_adj:.4f}")
    print(f"N:               {model.nobs:.0f}")
    
    # Significance assessment at 5%
    sig_at_5pct = slope_pval < 0.05
    direction = "positive" if slope > 0 else "negative"
    sig_text = "significant" if sig_at_5pct else "not significant"
    print(f"\nSlope is {direction} and {sig_text} at 5% level")
    
    print("=" * 60 + "\n")

## Verification & Modifications (Disclose • Verify • Critique)
- **Verify:** How you checked the output (e.g., ran the script, spot-checked regression table)
> I ran the script and visually checked the output graphs and tables for any errors.

- **Critique:** What was wrong/incomplete and why
> I did not find any errors in the AI's code for this assignment. 

- **Modify:** What you changed in your final work
> I did not make any changes to the AI output for this assignment.
