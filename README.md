# Colorchecker

This repo has data, yaml and weights necessary to train colorscale checker using yolov3

This repository represents IdLab's open-source colorscale checker using object detection methods, to be used in cutural and hertiage domain. It incorporates lessons learned and best practices evolved over hours of training and evolution on manually labelled datasets. This repo is based on ultralytics yolo v3 pytorch implementatiion. **All code and models are under active development, and are subject to modification or deletion without notice.** Use at your own risk.


## Download Pretrained weights and dataset

Download the pretrained weights trained for ~300 epochs to directly use the model for inference.

To train the model, download colorchecker.yaml and colorchecker dataset. The dataset is a small 60-image dataset which is already split into train, test and evaluate. Train and test are used for training and validating the model, while evaluate is used to test the model after training.


The dataset and pretrained weights are present in the [weights.zip](https://github.com/tckrishna/colorchecker/blob/19bb2ae539e201e666ea6b50b745b7bb2c6b8f34/weights.zip) and [dataset.zip](https://github.com/tckrishna/colorchecker/blob/19bb2ae539e201e666ea6b50b745b7bb2c6b8f34/dataset.zip) respeectively.


## Requirements

Python 3.8 or later with all [requirements.txt](https://github.com/ultralytics/yolov3/blob/master/requirements.txt) dependencies installed, including `torch>=1.7`. To install run:
```bash
$ pip install -r requirements.txt
```

## Tutorials

* [Installation and general usage](https://colab.research.google.com/drive/1OreAxCrCTkTqbIxu2Z_8KWuCujKyyncI?usp=sharing)&nbsp; 🚀 RECOMMENDED

## Inference

`detect.py` runs inference on a variety of sources, downloading models automatically from the [latest YOLOv3 release](https://github.com/ultralytics/yolov3/releases) and saving results to `runs/detect`.
```bash

$ python detect.py --source 0  # webcam
                            file.jpg  # image 
                            file.mp4  # video
                            path/  # directory
                            path/*.jpg  # glob
                            'https://youtu.be/NUsoVlDFqZg'  # YouTube video
                            'rtsp://example.com/media.mp4'  # RTSP, RTMP, HTTP stream
```

<img width="500" src="https://github.com/tckrishna/colorchecker/blob/1ce33c44706e4c61fb41082c3814fdbed1113e36/data/images/test_batch1_pred.jpg">  


Use **--crop True** incase you want to delete/crop the detected colorscale from the picture.

To run inference on example images in `data/images`:
```bash
$ python detect.py --weights weights/best.pt --img 640 --conf 0.25 --source dataset/evaluate/ --crop True
```

## Training

Run commands below to reproduce results on [COCO](https://github.com/ultralytics/yolov3/blob/master/data/scripts/get_coco.sh) dataset (dataset auto-downloads on first use). Training times for YOLOv3/YOLOv3-SPP/YOLOv3-tiny are 6/6/2 days on a single V100 (multi-GPU times faster). Use the largest `--batch-size` your GPU allows (batch sizes shown for 16 GB devices).
```bash
$ python train.py --img 640 --batch 16 --epochs 100 --data colorchecker.yaml --weights weights/last.pt --nosave --cache
```
<img width="800" src="https://github.com/tckrishna/colorchecker/blob/f10b5ebd4f8b16a83d8db4c95ea523ba0e7dccf5/data/images/results.png">


## About Us
  
 [assets3]: https://s-team-ghent.github.io/
 [assets4]: https://tw06v072.ugent.be/kbr/
 [assets5]: http://www.floredegand.be/lamgods/
 [assets6]: https://tw06v072.ugent.be/eureca
 [assets7]: http://tw06v074.ugent.be/
  
 Research group homepage: [LINK][assets3]
  
Over the past years, IDLab researchers of Ghent University have developed several building blocks for multimodal data processing, computer vision, NLP/NER, spatio-temporal enrichment, data mining, and cross-collection linking which can - with some modifications - also be applied to the proposed social security cards collection.

In the domain of cultural heritage the team of prof. Steven Verstockt have built up a lot of expertise and (inter)national collaboration in the UGESCO, EURECA, Flore de Gand, CHANGE, DATA-KBR-BE, FAME and Museum in de Living projects.
  
Links to demonstrators of related projects:

* [DATA-KBR-BE][assets4] (Document layout analysis, image similarity, NER)
* [Flore de Gand][assets5] (Digitization, cross-collection linking, herbaria)
* [Eureca][assets6] (HTR, document layout analysis, labeling tool)
* [Ugesco][assets7] (Object detection, NER, crowdsourcing)


## Contact

**Issues should be raised directly in the repository.** For business inquiries or professional support requests please visit https://s-team-ghent.github.io/ or email Prof. Steven Verstockt at steven.verstockt@ugent.be.
  

## Citation

[![DOI](https://zenodo.org/badge/146165888.svg)](https://zenodo.org/badge/latestdoi/146165888)
