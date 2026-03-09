# Data4Econ_Hackaton
Data4Econ Hackathon is an hackathon dedicated to data analytics for economics. This event brings together students, researchers, and professionals to tackle real-world challenges using data provided by Alperia and Gruppo Dolomiti Energia.

## Introduction
The goal of this study is to forecast the hourly energy production of a plant for January 2025 using historical data from 2024 and weather forecasts. We adopt an AI-based approach trained on 2024 data (actual production and observed weather) to estimate future production from forecasted meteorological variables. 

## Dataset and preprocessing
The available data include hourly plant production for 2024, as well as hourly observed and forecasted weather data for the same year, covering five locations: the municipality hosting the plant and four neighboring municipalities. For each location, the available meteorological variables are wind speed, wind direction, precipitation, and relative humidity.
During preprocessing, all data were merged into a single hourly dataset. Each hour of 2024 was associated with forecasted meteorological variables from all five locations. The resulting dataset contains 8,784 hourly observations, each described by 96 features and the corresponding production value.
Due to a degradation in model performance, a feature selection step was applied to remove highly correlated variables, reducing the feature set to 16 variables. For prediction, a similar dataset was built for January 2025 using only forecasted meteorological variables, which was then used to generate the production estimates.

## Predictive models 
The first model evaluated was a simple Multi-Layer Perceptron (MLP). On the baseline dataset, its performance was inferior to other models such as XGBoost and Long Short-Term Memory (LSTM) networks. However, after applying feature augmentation, the MLP performance improved significantly, achieving a MAPE of 0.36 on the validation set. The best configuration consisted of two linear layers with 32 and 1 neurons, with Layer Normalization applied between them.

Given the sequential nature of the problem, LSTM networks were expected to be well suited. This was confirmed by an initial MAPE of 0.64 using only the four baseline features. However, performance did not improve when using the augmented dataset and degraded further when all augmented features were included. This is likely due to many features being moving averages, which already capture temporal structure, reducing the effectiveness of the LSTM. Combined with long training times, this prevented effective fine-tuning of feature selection and hyperparameters.

## Discussion
Overall, data augmentation proved to be a key factor, providing substantial performance gains for most tested models. More complex models such as LSTMs were unsuitable due to long training times and limited time availability. Intermediate models such as XGBoost and MLPs offered the best trade-off between simplicity and performance.

During testing, the trained model was evaluated on January 2025. The augmented dataset was used to generate hourly production estimates, which were then compared against observed production data to assess predictive performance.
