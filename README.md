# yolo-mask

## Demonstration :

![alt text](https://github.com/mohcineelharras/yolo-mask/gif.mp4)


## Requirements
```
pip install numpy
pip install pandas
pip install tensorflow=1.x.x
pip install keras==2.1.5
```

## Import Data

First you need to download the training set (links below) or your custom dataset. Moreover, you would need to download these weights (link below as well) trained on [WIDER FACE: A Face Detection Benchmark](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/index.html) dataset to detect faces.

Next, you should copy the file to you local git-cloned folder "yolo-mask/data"

## Data Analysis
The dataset wasn't big enough to have perfect results. Yet, the idea behind this project and the challenging tast was to get it to work even with very few amout of data.


## Preparing Data

I downloaded some weights trained on coco first and then trained to detect faces from internet.

Then I had to teach the NN to distinguish between a face with or without masks using the dataset I built myself and labeled.

For labeling each image, I had to use a tool called labelimg (more details on references).


## Training

1. Generate your own annotation file and class names file.  
    One row for one image;  
    Row format: `image_file_path box1 box2 ... boxN`;  
    Box format: `x_min,y_min,x_max,y_max,class_id` (no space).  
    For VOC dataset, try `python voc_annotation.py`  
    Here is an example:
    ```
    path/to/img1.jpg 50,100,150,200,0 30,50,200,120,3
    path/to/img2.jpg 120,300,250,600,2
    ...
    ```

2. Make sure you have run `python convert.py -w yolov3.cfg yolov3.weights model_data/yolo_weights.h5`  
    The file model_data/yolo_weights.h5 is used to load pretrained weights.

3. Modify train.py and start training.  
    `python train.py`  
    Use your trained weights or checkpoint weights with command line option `--model model_file` when using yolo_video.py
    Remember to modify class path or anchor path, with `--classes class_file` and `--anchors anchor_file`.

If you want to use original pretrained weights for YOLOv3:  
    1. `wget https://pjreddie.com/media/files/darknet53.conv.74`  
    2. rename it as darknet53.weights  
    3. `python convert.py -w darknet53.cfg darknet53.weights model_data/darknet53_weights.h5`  
    4. use model_data/darknet53_weights.h5 in train.py

References :
https://github.com/qqwweee/keras-yolo3
https://github.com/tzutalin/labelImg#labelimg
https://github.com/sthanhng/yoloface

Datasets used :
I built my own Dataset from pictures I got mainly in social media.
mask_off :
https://drive.google.com/drive/folders/1TvmM8oTJwr5MMQ7sTLiOhB3EI9HQGC0Q?usp=sharing
mask_on :
https://drive.google.com/drive/folders/1cJMfQ9tYSRgtwiaG_wumixHpIWGsm3od?usp=sharing
weights :
https://drive.google.com/file/d/1xYasjU52whXMLT5MtF7RCPQkV66993oR/view


