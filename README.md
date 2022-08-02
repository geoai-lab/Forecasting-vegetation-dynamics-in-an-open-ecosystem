# Forecast vegetation dynamics in open ecosystem

### Overall description
The ConvLSTM model leverages the backbone of a LSTM model but applies convolutional operations to process the 2D image at each time step. In this study, we adopted a ConvLSTM model to forecast the NDVI values in Cape Peninsula, which provides a machine-learning based method to estimate the vegetation dynamics in open ecosystem. 

### Repository organization

* "Data" folder: This folder has six files, "age.grd", “covariates_250m_peninsula.grd”, “NDVI.grd”, “newprec_01.tif”, “newprec_07.tif” and "QA.grd". The "age.grd" file contains fire history data which is included in the form of vegetation age calculated using the Table Mountain National Park (TMNP) fire scar database. "covariates_250m_peninsula.grd" contains 12 variables, namely (1) elevation, (2) slope, (3) aspect, (4) topographic position index (TPI), (5) topographic roughness index (TRI), (6) highest temperature in January (summer in South Africa), (7) lowest temperature in July (winter), (8) mean precipitation in January, (9) mean precipitation in July, (10) mean solar radiation in January, (11) mean solar radiation in July, (12) vegetation type. “newprec_01.tif” and “newprec_07.tif” are used to update the environmental variables ((8) and (9)) in "covariates_250m_peninsula.grd". The " NDVI.grd " file has the same size of 172 (height) by 63 (width) with a spatial resolution of 250 meters, the original data is obtained from the MOD13Q1. The quality of NDVI data could be indicated by the quality assessment file ("QA.grd").

* "SourceCode" folder: This folder has five subfolders (namely "ablation study", “ConvLSTM mutisteps ahead forecasting”, “ConvLSTM optimal variables combination”, “FC-LSTM multisteps ahead forecasting” and "SimpleRNN multisteps ahead forecasting"), and eight Jupyter Notebook files (namely "ConvLSTM_smoothed_NDVI_all_variables_linearactivate.ipynb", "ConvLSTM_smoothed_NDVI_all_variables_without_slope_tuned.ipynb", "ConvLSTM_smoothed_NDVI_only_linear_activation.ipynb", "ConvLSTM_smoothed_NDVI_with_improved_four_variables_linearactivate.ipynb", "ConvLSTM_unsmoothed_NDVI_only_linear_activation.ipynb", "baseline_smoothedNDVI.ipynb", "baseline_unsmoothedNDVI.ipynb" and "multi_steps_baseline_smoothedNDVI.ipynb"). The " ablation study " folder contains the source code for testing each variable importance. The “ConvLSTM mutisteps ahead forecasting” folder contains the source code for testing ConvLSTM's performance on different time step length forecasting. The “ConvLSTM optimal variables combination” folder contains the source code for finding the best environmental variables combination to improve the model performance. The “FC-LSTM multisteps ahead forecasting” folder contains the source code testing FC-LSTM's performance on different time step length forecasting. The “SimpleRNN multisteps ahead forecasting” folder contains the source code testing SimpleRNN's performance on different time step length forecasting. The "ConvLSTM_smoothed_NDVI_all_variables_linearactivate.ipynb" file contains source code for training ConvLSTM model with smoothed NDVI data and all 13 environmental variables. The "ConvLSTM_smoothed_NDVI_all_variables_without_slope_tuned.ipynb" file contains source code for training ConvLSTM model with smoothed NDVI data and all 12 environmental variables (exclude "slope"). The "ConvLSTM_smoothed_NDVI_only_linear_activation.ipynb" file contains source code for training ConvLSTM model with only smoothed NDVI data. The "ConvLSTM_smoothed_NDVI_with_improved_four_variables_linearactivate.ipynb" file contains source code for training ConvLSTM model with only smoothed NDVI data and four environmental variables that improve the performance of model. The "ConvLSTM_unsmoothed_NDVI_only_linear_activation.ipynb" file contains source code for training ConvLSTM model with only unsmoothed NDVI data. The "baseline_smoothedNDVI.ipynb" file contains source code of two baselines trained with smoothed NDVI data in the paper. The "baseline_unsmoothedNDVI.ipynb" file contains source code of two baselines trained with unsmoothed NDVI data in the paper. The "multi_steps_baseline_smoothedNDVI.ipynb" file contains source code of two baselines trained with smoothed NDVI data for multi-step ahead predictions in the paper.

* "PretrainedModel" zip file: The "PretrainedModel.zip" is a zip file of pretrained models to make the download of the pertained models easier. The zip file is available [here.](https://geoai.geog.buffalo.edu/VariousResources/PretrainedModel.zip)

### Use the pretrained model 

Using the pretrained model for vegetation dynamic will need the following steps:

1. Setup the virtual environment: Please create a new virtual environment using Anaconda and install the dependent packages using the following commands (please run them in the same order below):
 ```bash
                     conda create -n EnvForecasting python=3.8
                     conda activate EnvForecasting
                     pip install tensorflow==2.2.0
                     pip install keras==2.3.1
                     pip install rasterio
 ```
2. Download the pretrained model, and unzip it to a folder that you would prefer.

3. Use the pretrained model to forecast the vegetation dynamics in Cape Peninsula.
 ```bash
import tensorflow as tf
    
ConvLSTM_model = tf.keras.models.load_model("the folder path of the pretrained model")
prediction = ConvLSTM_model.predict(test_data)
print(prediction)
 ```


### Project dependencies:
* Python 3.8
* Keras 2.3.1
* Tensorflow 2.2.0
