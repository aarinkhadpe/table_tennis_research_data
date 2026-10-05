# Table tennis ball trajectory dataset and prediction results

This folder contains the ball trajectories and the evaluation results for the paper's comparison of three trajectory predictors: **Physics-only**, **End-to-End GP** and **Hybrid-GP**.

All files are plain CSV with a header row. Missing values are empty cells.

All positions, including table corners and predictions, use one fixed Cartesian frame:

- **Origin:** approximately the centre of the table surface.
- **x:** across the table's width. The side edges are at x ≈ ±857 mm.
- **y:** along the table's length. The end lines are at y ≈ ±1412 mm, and the net is at y ≈ 0.
- **z:** vertical, pointing up. The table surface is at z ≈ 0.

Cameras sample at 125 Hz.

## Files

### Measured data

**trajectories.csv**: 167 cleaned ball trajectories, one row per frame. All models were trained and evaluated on this file.

**shot_index.csv**: one row per shot. identifies the fold in which the shot was used.

**table_corners.csv**: the four corners of the table surface in the table frame.

### Prediction results

We ran 5-fold cross-validation over the 166 evaluated shots, split into the folds listed in **shot_index.csv**. In each fold, all three predictors were fitted on the training shots. Each test shot was then predicted from its **first 20 frames** only (the observation window). The predictors output positions in the same table frame as the measurements.

**predictions.csv**: the predicted continuation of every test shot, for each predictor.

**crossing_errors.csv**: the error metric reported in the paper. 

**paired_bootstrap_ci.csv**: paired comparisons between predictors. The comparison uses shots that both predictors scored. For each shot, the difference is **error(predictor_a) − error(predictor_b)**. A positive value means **predictor_b** had smaller errors.

**latency.csv**: time of a prediction call for each predictor to compare performance.
