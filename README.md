## 
This assignment combines [Lightly](https://www.lightly.ai) and [LabelStudio](https://labelstud.io) 
for showing a complete workflow of creating a machine learning model including Active Learning on image task.
1. It starts with collecting unlabelled data. 
2. Then it uses Lightly to choose a subset of the unlabelled to be labelled.
3. This subset is labelled with the help of LabelStudio.
4. A machine learning model is trained on the labeled data and Active Learning is used to choose the next batch to be labelled.
5. This batch is labelled again in LabelStudio.
6. The machine learning model is trained on the updated labelled dataset.
7. Finally, the model is used to predict on completely new data. 


## 0. Database and subsampling setup on Lightly and Labels setup on lebel studio:

Dataset:
We want to train a classifier predicting whether a webcam targeting a mountain is showing sunny, cloudy, or very cloudy weather.
To gather our dataset, we use the webcam at Jungfraujoch targeting the mountain Jungfrau in Switzerland.
These 365 images are downloaded at a medium but sufficient resolution with a total size of 28 MB.

```bash
# Set the directory the images should be downloaded to.
export WEATHER_DIR_RAW=path/to/dataset/weather_raw
# Download the images to the directory you just specified.
python source/1_scrape_junfraujoch.py
```

   
## 2. Analyze and subsample the dataset

First, let's analyze the dataset and its distribution of data using the Lightly webapp.

Embedding view of the dataset
Sampling using the CORESET sampler to choose a diverse subset of only 30 images to be labelled.
Use it by clicking on `Create Sampling`, set the amount of datapoints to 30
and specify the name of the new tag to be created as `Coreset_30`.



## 3. Label a subset of images to train a classifier


#### 3.1 Run Label Studio
```

#### 3.2 Configure Storage

##### 3.3 Configure the labelling interface


#### 3.4 Add labelling instructions
```

#### 3.5 Labelling


#### 3.6 Export of Labels

## 4. Train a model and do active learning



## 5. Label the additional 15 images



## 6. Train a model on the new labels

## 7. Apply the model on new images
