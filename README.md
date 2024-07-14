# Forecasting the Power Output of a Wind Turbine

### Outline
"Machine Learning in Renewable Energy Systems"
Datasets of a British and a Brazilian wind farm were used for the project. The primary goal involved predicting the wind power for a minimum of one turbine from each farm for the subsequent time step (10 min), hour, and day. Additionally, participants were tasked with the selection of relevant features, either through manual or automated means. This process, along with all undertaken steps, was to be documented and explained.

## How to use this GitHub repository
1. Clone this repository
2. Set up a new virtual environment with the given environment.yml file
```
conda env create -f environment.yml
```
3. Download the [British data](https://zenodo.org/record/5841834#.ZEajKXbP2BQ) and the [Brazilian data](https://zenodo.org/record/1475197#.ZD6iMxXP2WC) and put them into their corresponding data folder
4. Make sure that your folder structure looks like this:
```
├───data
│   ├───British
│   │   ├───Kelmarsh_SCADA_2016_3082
│   │   ├───Kelmarsh_SCADA_2017_3083
│   │   ├───Kelmarsh_SCADA_2018_3084
│   │   ├───Kelmarsh_SCADA_2019_3085
│   │   ├───Kelmarsh_SCADA_2020_3086
│   │   └───Kelmarsh_SCADA_2021_3087
│   └───Brazilian
│       ├───UEPS_v1.nc
│       └───UEBB_v1.nc
├───notebooks
│   ├───DataInspection.ipynb
│   ├───MovingAverage.ipynb
│   ├───RegressionVariants.ipynb
│   ├───XGBoost.ipynb
│   └───Evaluation.ipynb
├───src
├───.gitignore
├───environment.yml
└───README.md
```
5. You should now be able to run all the notebooks. For every examined model there is a corresponding notebook. Additionally, there is a notebook for the data inspection and one for the overall evaluation and comparison of the models. Please make sure that you select the correct kernel, i.e. the one from the virtual environment you created in step 2. 

Each notebook is self-contained, allowing you to execute it independently without relying on the others. However, there are references within them. Therefore, we advise running the notebooks in the suggested sequence:

1. _DataInspection.ipynb_
2. _MovingAverage.ipynb_
3. _RegressionVariants.ipynb_
4. _XGBoost.ipynb_
5. _Evaluation.ipynb_

Please run the cells of the respective notebooks in the corresponding order since we overwrite some variables in rare cases.

## Models

Overall, we examine four different models within this project:

1. _Moving Average_ (ma)
2. _Ridge Regression_ (rr)
3. _Kernel Ridge Regression_ (kernel)
4. _XGBoost Regression_ (xgb)

For a detailed description of the models please refer to the corresponding notebooks, where hyperparameter tuning, forecasting performance and the transfer learning challenge are discussed. 
Please find the implementation of the models in the src/models folder.

All models are implemented according to the BaseEstimator class of sklearn. This design enables efficient hyperparameter tuning through the use of GridSearchCV and RandomizedSearchCV.

In each case we discuss, it is essential to apply one or more transformations to the time series data. The classes responsible for these transformations can be found in the src/datahandling/preprocessing.py. Importantly, these transformation classes are also compatible with sklearn, making them suitable for integration into a pipeline. You can find a short overview of the transformers at the end of the data inspection notebook.

## Results

All the models produce generally satisfactory results, both visually and in terms of metrics.
In summary, we conclude that for the given task, the _Ridge Regression_ and _XGB_ models stand out as the top choices. _Ridge Regression_ is the preferred option when computational efficiency and interpretability are prioritized. On the other hand, _XGB_ is the optimal choice when aiming for the highest possible performance across all datasets.

Note that in this project, our focus is solely on the examination of supervised learning approaches. However, potential future endeavors might involve exploring purely time series-driven techniques like SARIMA. Additionally, we could explore deep learning approaches, with Long Short-Term Memory networks (LSTMs) being a suitable architecture for handling time series data. Moreover, considering our transformation of the data into a supervised learning problem, we could also consider the use of a straightforward Multi-Layer Perceptron (MLP).
Moreover, a more comprehensive investigation into the hyperparameter space of computationally intensive models such as _XGB_ and _Kernel Ridge Regression_ could be conducted, leveraging additional computational resources. This could potentially lead to improved outcomes.
