#MedImgSeg

# Consistency Label Transferring Network for Medical Image Segmentation
## Introduction
Official pytorch implementation of paper "Consistency Label Transferring Network for Medical Image Segmentation"

This model can simultaneously identify pixel level label-discriminated mask
meanwhile maintain the semantic information and anatomical structure of medical image to precisely define segmentation boundary by collating the label and semantic related
region through an image synthesis procedure. In addition, the produced lesion mask is further prompted by a joint discrimination strategy for the synthetized and generated image belonging to the opposite category. Extensive experiments of
the proposed method on BraTS and ISIC datasets demonstrate consistently superior performance over existing state-of-the-art methods.

Comparison between the other methods of weakly supervised segmentation and ours. (a) Ground Truth (GT),
(b) Ours, (c) PSA (Ahn and Kwak 2018), (d) SEAM (Wang et al. 2020) and (e) IRN (Ahn, Cho, and Kwak 2019).
<div align=center><img width="1500" height="1200" src="https://raw.githubusercontent.com/mlcb-jlu/MedImgSeg/master/img-folder/weak_result_contrast.png"/></div>

Comparision of the segmentation performance JA, DI, AC, SE and SP (%) of our weakly supervised pipeline on
(a) BraTS dataset and (b) ISIC dataset against CAM (Zhou et al. 2016), CAM+CRF (Zhou et al. 2016), PCM (Wang
et al. 2020), PCM+CRF (Wang et al. 2020), PSA (Ahn and Kwak 2018), SEAM (Wang et al. 2020), IRN (Ahn, Cho, and Kwak 2019)
<div align=center><img width="450" height="500" src="https://raw.githubusercontent.com/mlcb-jlu/MedImgSeg/master/img-folder/weak%20superbised%20accuracy%20result.png"/></div>

This code was made public to share our research for the benefit of the scientific community. Do not use it for immoral purposes.
## Prerequisites
## Clone this repo
Our code is built based on Pytorch, and the packages to be installed are as follows:
```
sudo git clone https://github.com/mlcb-jlu/MedImgSeg
cd MedImgSeg/
```

```
conda create -n CBFNet python=3.6.6
source activate
conda activate CBFNet
```
Install the pytorch you need on the pytorch official website:https://pytorch.org/get-started/locally/. 
```
conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch -c nvidia
```
Then install the dependencies: (Anaconda is recommended.)

```
pip install pillow tqdm tensorboardx pyyaml visdom opencv-python nibabel libsvm matplotlib
```


## Data Preparation
To evaluate the segmentation performance of different methods, we conducted experiments on two different medical datasets, including BraTS datasets and ISIC datasets.
You can download for training and testing.(location:https://pan.baidu.com/s/1rx29DxWq5W6bTh9NcvT0Tw, password:1111)

* Anyway you should get the dataset folders like:
```
your_project_location
 - dataset
   - BraTS
     - brats_1
       - 563_A_weak
       - 563_B_weak
       - testA
         - images
         - labels
       - testB
       - val
         - images
         - labels
       - few_sample
         - stage2_50
           - A
           - B
   - ISIC
     - ...
```
## Quick Test
你可以下载我们提供的训练完的模型，然后放到对应目录下。运行demo.sh快速测试模型分割效果，分割效果保存在结果目录中。 (location:https://pan.baidu.com/s/1oWbK0j5Xl6E2MUQU6TCRzg, password:1111)
```
bash ./demo.sh
```

## Training and Testing
* Step1：you need to run visdom and open the corresponding address in the browser to monitor each loss:
```
python -m visdom.server
```
* Step2： you should change the PATH in the executable bash files to your virtual environment location.
To training , validating and testing on BraTS dataset and ISIC dataset:
```
bash ./start_train.sh
bash ./start_test.sh
bash ./start_crf.sh
```
* Then you will get the result folders like:
```
your_project_location
 - results
   - BraTS
     - brats_1
       - val_folder
         - crf_deal1
           - 1~8 # The segmentation results after dense-CRF post-processing on validation set
           - results.txt # The best segmentation results of the model on the validation set
       - crf_deal1
         - 1~8 # The segmentation results after dense-CRF post-processing on test set
         - results.txt  # The best segmentation results of the model on the test set
   - ISIC
     - ..
```

