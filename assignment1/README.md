# Assignment 1 - COVID-19 Forecast

## **Models and Features**

I used autoregression models with the number of cases in previous days as features.

## Getting Started

### Packages Used

- tqdm>=4.50
- pandas
- statsmodels>=0.12
- sklearn
- numpy
- scipy

### Install Requirements

    pip install -r requirements.txt

### Train Models and Forecast

To generate the result of the prediction, one can run through model_regression.ipynb cell by cell.
Or you can also run it with the following command.

    cd notebook
    ipython model_regression.ipynb
    
## Methodology

### Pre-processing

1. Cases with negative numbers
    
    Some of the numbers of cases in the csv downloaded from the website are negative, which are not reasonable. Two measures are proposed to fix this problem. One is setting all negative value to 0, and the other is applying absolute function (np.abs()) to negative value
    
    In this project, I applied the second measure to the dataset, since, by observation, the second value seems more likely to the original data.

2. Cropping data

    Most of the data in the early phase of the COVID-19 outbreak are not accurate due to the low awareness of the disease. Therefore, in this project, I trained the model only with the data later than 1st July 2020.

3. Smoothing

    There are some noises in the raw data. To smooth the curve of the number of cases, I applied a Savitzky-Golay filter with window size 51 (days) and polynomial order of 3.

### Model

1. Auto Regression (AutoReg)

    The autoregression model is built with a python package statsmodels. The primary tenable parameter is the window size for autoregression. In this project, the window size for autoregression is different from model to model; that is, different countries have different window size for autoregression. The selection of window sizes is base on the performance on the test set.

2. ReLU

    As mentioned above, the cases should not be negative, but this is not always the case for autoregression. Therefore, I wrote a ReLU (Rectified Linear Unit) function, which would set negative values to zero, and apply it to the output of autoregression prediction.

3. Round to Int (rint)

    The number of cases should not be fractional. I rounded them to integers before producing the final prediction.
    
## Result

Below are the plots of ground truth data and prediction in the test data for five countries - Greece, India, Russia, Turkey, United_States_of_America. 
The MAPE is around 20% - 30%, which is mediocre.

![Greece](https://raw.githubusercontent.com/TYLearChen/NTHU-CS4602/master/assignment1/image/Greece.png)

MAPE of Greece: 31.059%

---

![India](https://raw.githubusercontent.com/TYLearChen/NTHU-CS4602/master/assignment1/image/India.png)

MAPE of India: 29.797%

---

![Russia](https://raw.githubusercontent.com/TYLearChen/NTHU-CS4602/master/assignment1/image/Russia.png)

MAPE of Russia: 23.288%

---

![Turkey](https://raw.githubusercontent.com/TYLearChen/NTHU-CS4602/master/assignment1/image/Turkey.png)

MAPE of Turkey: 18.154%

---

![United_States_of_America](https://raw.githubusercontent.com/TYLearChen/NTHU-CS4602/master/assignment1/image/United_States_of_America.png)

MAPE of United_States_of_America: 23.280%

## GitHub Repository

> <https://github.com/TYLearChen/NTHU-CS4602/tree/master/assignment1>

## References

> Brownlee, J. (2020, August 14). Autoregression Models for Time Series Forecasting With Python. Retrieved October 11, 2020, from <https://machinelearningmastery.com/autoregression-models-time-series-forecasting-python/>
