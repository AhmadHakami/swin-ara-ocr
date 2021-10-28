# swin-transformer-ocr
ocr with [swin-transformer](https://arxiv.org/abs/2103.14030)

## Overview
Simple and understandable swin transformer ocr project.
The model in this repository heavily relied on high-level open source projects like timm and x_transformers.
And also you can find that the procedure of training is intuitive thanks to legibility of pytorch-lightning.

The model in this repository encodes input image to context vector with 'shifted-window` which is swin-transformer encoding mechanism. And it decodes the vector with normal auto-regressive transformer.

If you are not familiar with transformer ocr structure, [transformer-ocr](https://github.com/YongWookHa/transformer-ocr) would be easier to understand because it uses traditional convolution network (ResNet-v2) for encoder.

## Performance
With private korean handwritten text dataset, the accuracy(exact match) is 95%.

## Data
```bash
./dataset/
├─ preprocessed_image/
│  ├─ cropped_image_0.jpg
│  ├─ cropped_image_1.jpg
│  ├─ ...
├─ train.txt
└─ val.txt

# in train.txt
cropped_image_0.jpg\tHello World.
cropped_image_1.jpg\tvision-transformer-ocr
...
```

You should preprocess the data first. Crop the image by word or sentence level area. Put all image data in specific directory. Ground truth information should be provided with txt file. In the txt file, write image file name and label with `\t` seperator in the same line.

## Configuration
In `settings/` directory, you can find `default.yaml`. You can set almost every hyper-parameters in that file. Copy one and edit it as your experiment version. I recommend you to run with the default setting first, before you change it.

## Train
```bash
python run.py --version 0 --setting settings/default.yaml --num_workers 16
```
You can check your training log with tensorboard.  
```
tensorboard --log_dir tb_logs --bind_all
```  

## Predict
It's not really hard to add prediction function to the pytorch-lightning module with fully-trained model. I will leave it empty for now. But I would glady do it if there's any request.

_Predict code request has been received. The code will be updated by early Nov._

enjoy the code.

## Citations

```bibtex
@misc{liu-2021,
    title   = {Swin Transformer: Hierarchical Vision Transformer using Shifted Windows},
	author  = {Ze Liu and Yutong Lin and Yue Cao and Han Hu and Yixuan Wei and Zheng Zhang and Stephen Lin and Baining Guo},
	year    = {2021},
    eprint  = {2103.14030},
	archivePrefix = {arXiv}
}
```
