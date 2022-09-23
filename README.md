# All Repos for RLT Detection

This is the parent repo for all RLT detection related tools, source code, datasets and results.

## Prerequisites

**All the pictures are collected from** [Google Maps](https://www.google.com/maps).
You can find the dataset for this project in the [images Directory](https://github.com/RituAhmed/images/tree/f82e4fe325b9c75cd62421d53bc674931cc85255). The image annotation task has been done in [Label Studio](https://labelstud.io/). For further image annotation task it is recommended to use this Label Studio and export it as a COCO dataset. To install this application use the following commands:
```
# Install the package into python virtual environment
pip install -U label-studio
# Launch it!
label-studio
```
**For the python virtual environment Anconda is used. To install the conda follow this link:**

```
https://opensourceoptions.com/blog/setup-anaconda-python-to-work-with-visual-studio-code-on-windows/
```
**After preparing the Dataset it is required to organize it for the training.** For the training atleast two types of datasets are needed-train dataset and test dataset. We can split it in different ways. Here ,[cocosplit](https://github.com/akarazniewicz/cocosplit) is usd to split the dataset. To install this use the following commands:
```
git clone https://github.com/akarazniewicz/cocosplit.git
next Command, pip install -r requirements
python cocosplit.py --having-annotations --multi-class -s 0.8 /path/to/your/coco_annotations.json train.json test.json
```
It will split coco_annotation.json into train.json and test.json with ratio 80%/20% respectively. The dataset is prepared for this repo, if we just want to use this repo you dont need to install either label studio or cocosplit, you can just clone the all_repos_for_rlt_det or you can just download it but we must need to install the Anconda. In this repo you can find the dataset under the [cocosplit directory](https://github.com/RituAhmed/cocosplit/tree/408ffa501160b55b2a43ca1978f891ebbab317cb).

**MMDetection is used to detect the RLT in google map statelite view.** [MMDetection](https://github.com/open-mmlab/mmdetection) is an open source object detection toolbox based on PyTorch. It is a part of the OpenMMLab project. The master branch works with PyTorch 1.5+. MMDetection works on Linux, Windows and macOS. It requires Python 3.6+, CUDA 9.2+ and PyTorch 1.5+. Since we already installed ANACONDA, we can just skip this step. To install the MMDetection follow this link:
```
https://github.com/open-mmlab/mmdetection/edit/master/docs/en/get_started.md
```
To Train with a new dataset follow this link: 
```
https://github.com/open-mmlab/mmdetection/blob/master/docs/en/2_new_data_model.md
```
To understand it more precisely follow the steps:
```
First create a dataset under the directory mmdetection_rlt/mmdet/datasets. You can take rltdetection.py as an example for your dataset. For this work [rltdetection.py](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/mmdet/datasets/rltdetection.py) is created and used.

Next step is to import it in mmdetection_rlt/mmdet/datasets/_init.py_ file.
We are now ready to select and use any network. In my case i have used Faster RCNN, resnet50 with FPN as a backbone. Faster RCNN is an object detection architecture presented by Ross Girshick, Shaoqing Ren, Kaiming He and Jian Sun in 2015, and is one of the famous object detection architectures that uses convolution neural networks like YOLO (You Look Only Once) and SSD ( Single Shot Detector). For this we need to prepare a config file first. 
Find the config file for this project [here](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/configs/faster_rcnn/faster_rcnn_r50_fpn_1x_rlt.py). Edit the  models, datasets, schedule files under this according to your need.
By default the results folder (work_dirs) is created at the root of mmdetection_rlt directory. To move it somewhere else, add a "work_dir=<your directory>" line in your config file.
After completing all the steps, to train the model use the following command:

python mmdetection_rlt/tools/train.py mmdetection_rlt/configs/faster_rcnn/faster_rcnn_r50_fpn_1x_rlt.py  
```
# How to use this Repo?
After finishing all the installation, First run the command:
```
git clone git@github.com:RituAhmed/all_repos_for_rlt_det.git
```
The trained model can be found [here](https://github.com/RituAhmed/work_dirs/tree/df00be477e3a00c5ba5a19f1b5715b9400b5e326). Extract any of the .rar file under this directory to have the complete traine model/.pth file.

To test the trained model with single image run the file [inferencedemo.ipynb](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/inferencedemo.ipynb).
```
**Note** Before run the program change the config_file and checkpoint_file address accornding to your adrdress.
```
To test the whole trained model use the following command:
```
python mmdetection_rlt/tools/test.py mmdetection/configs/faster_rcnn/faster_rcnn_r50_fpn_1x_rlt.py work_dirs/faster_rcnn_r50_fpn_1x_rlt/latest.pth --eval bbox 
```
## Detection output example:

![Result1](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/Demoresult/result10.png)
![Result2](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/Demoresult/result11.png)
![Result3](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/Demoresult/result8.png)
![Result4](https://github.com/RituAhmed/mmdetection_rlt/blob/f5d9cbf6726190cf1b50490459541e52619ce02e/Demoresult/result15.png)
