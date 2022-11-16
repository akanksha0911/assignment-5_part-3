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


## 1. Database and subsampling setup on Lightly and Labels setup on lebel studio:

Dataset:
We want to train a classifier predicting whether a webcam targeting a mountain is showing sunny, cloudy, or very cloudy weather.
To gather our dataset, we use the webcam at Jungfraujoch targeting the mountain Jungfrau in Switzerland.
These 365 images are downloaded at a medium but sufficient resolution with a total size of 28 MB.

![image](https://user-images.githubusercontent.com/77387431/202115789-c2571df5-ea0c-4942-8e6d-418c2ee6edbe.png)


```bash
# Set the directory the images should be downloaded to.
export WEATHER_DIR_RAW=path/to/dataset/weather_raw
# Download the images to the directory you just specified.
python source/1_scrape_junfraujoch.py
```

   
## 2. Analyze and subsample the dataset

First, let's analyze the dataset and its distribution of data using the Lightly webapp.

Embedding view of the dataset
<img width="1242" alt="image" src="https://user-images.githubusercontent.com/77387431/202116232-efb7a7b3-a9d8-4c4f-b1a1-2dd9019291b2.png">

Sampling using the CORESET sampler to choose a diverse subset of only 30 images to be labelled.
Use it by clicking on `Create Sampling`, set the amount of datapoints to 30
and specify the name of the new tag to be created as `Coreset_30`.

<img width="1409" alt="image" src="https://user-images.githubusercontent.com/77387431/202116022-5e89cce1-ff8d-4520-ab3f-9a4c213496f6.png">


## 3. Label a subset of images to train a classifier


#### 3.1 Run Label Studio

export LABEL_STUDIO_BASE_DATA_DIR=$WEATHER_DIR_LABELED export LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true && label-studio start

<img width="1771" alt="image" src="https://user-images.githubusercontent.com/77387431/202116913-245ae7ef-e5b1-4126-a43d-8385e0008ed7.png">

![image](https://user-images.githubusercontent.com/77387431/202117576-212b73f7-d8db-418f-bd3f-ed5b05038a16.png)



#### 3.2 Configure Storage

<img width="1410" alt="image" src="https://user-images.githubusercontent.com/77387431/202117040-5abff607-f716-4e85-96d7-dda3e7b6549a.png">


##### 3.3 Configure the labelling interface

<img width="1137" alt="image" src="https://user-images.githubusercontent.com/77387431/202117145-9351111b-1f59-4693-bb93-e1357fddd07d.png">



#### 3.4 Add labelling instructions
<img width="1345" alt="image" src="https://user-images.githubusercontent.com/77387431/202117272-d82169f9-c385-4717-b2d0-cc6565da1f2a.png">


#### 3.5 Labelling
<img width="1778" alt="image" src="https://user-images.githubusercontent.com/77387431/202117405-c81762f5-dbaa-46c4-b7b6-788086f1aeda.png">

![image](https://user-images.githubusercontent.com/77387431/202117700-4570e42c-d308-447f-bc2a-a24981d7ecee.png)


#### 3.6 Export of Labels

![image](https://user-images.githubusercontent.com/77387431/202117793-4fe98885-daf7-40b0-b490-9c9b073e47b7.png)


## 4. Train a model and do active learning
![image](https://user-images.githubusercontent.com/77387431/202117860-e402ab8c-e73d-4143-8bad-4bd790ce9a39.png)

![image](https://user-images.githubusercontent.com/77387431/202117929-aa19b5cd-d947-4879-ba7a-dc9945ba076e.png)


<img width="1696" alt="image" src="https://user-images.githubusercontent.com/77387431/202116498-7746cd1b-fd38-41ed-b59a-c273d137ab1f.png">


## 5. Label the additional 15 images

<img width="1055" alt="Screen Shot 2022-11-15 at 11 51 03 PM" src="https://user-images.githubusercontent.com/77387431/202120388-f99acc21-b97c-46d0-8d2a-4f05975dad8a.png">


## 6. Train a model on the new labels

## 7. Apply the model on new images
