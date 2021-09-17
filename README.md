GitHub Link - https://github.com/thamidurm/CS4622-ML-project

# Preprocessing Steps

- Initially removed the `id` and `recorded_by` columns as they are unique and constant respectively.
- Only categorical data was missing. `Nan` values for nominal data were imputed as a new `unknown` category.
- Binary variables were imputed using their mode.
- `region_code` was dropped as it has invalid data. It was not cleaned because `region` has the same data.
    - It has 26 values while Tanzania has only [22 regions](https://en.wikipedia.org/wiki/Subdivisions_of_Tanzania)
    - All of the extra values seem to be caused by input errors
        - e.g.: `88` for `8` etc.
- All categorical values were converted to lower case and their spaces and dashes were removed to "normalize" them.
- Boolean features were converted to `0` or `1`
- No feature scaling was applied since boosted trees were used.
- Tried removing outliers using IQR of continuous features.
    - It is commented out in the notebook because it did not improve performance. 
- Sub-villages with less than 2 entries were encoded as a single `low frequency` sub-village.
    - Same was tried for `wpt_name`, `installer`, `funder`, `ward` features but it did not improve performance. 


# Feature Engineering

- CatBoost model's One Hot Encoding mechanism were used to encode categorical data.

- Feature selection was guided by plots and experiments.
    - Removed one of redundant feature pairs. (e.g: `payment` and `payment_type`)
        - Removing some of them affected the model performance negatively, therefore those were left alone.
    - Similar features were excluded to see their impact on the model.
    - Only `payment`, `source_class`, `extraction_type` were dropped as dropping others impacted performance during testing.
- Converting `recorded_at` to a timestamp
    - First tried splitting to date,month, year. 
    - However, converting to a timestamp improved the performance.
- Creating new features
    - Attempted to create some combinations of correlated categorical features.
        - However, these features did not improve performance. Therefore it was not explored further, and these features were removed.
        - e.g: `scheme_name_scheme_management`, `scheme_name_basin`
    - Tried to replace  `construction_year` with a duration instead. - This did not improve performance.
    - Amount_Tsh per population was also calculated - also did not improve performance
    - Log of continuous values were tried out - they did not improve performance as well.

## Proof of Submission

![Proof of Submission](images/submission.png)