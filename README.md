# Colorchecker

This repo has data, yaml and weights necessary to train colorscale checker using yolov3

This repository represents IdLab's open-source colorscale checker using object detection methods, to be used in cutural and hertiage domain. It incorporates lessons learned and best practices evolved over hours of training and evolution on manually labelled datasets. This repo is based on ultralytics yolo v3 pytorch implementatiion. **All code and models are under active development, and are subject to modification or deletion without notice.** Use at your own risk.


## Pretrained Checkpoints

[assets3]: https://github.com/ultralytics/yolov3/releases
[assets5]: https://github.com/ultralytics/yolov5/releases

Model |size<br><sup>(pixels) |mAP<sup>val<br>0.5:0.95 |mAP<sup>test<br>0.5:0.95 |mAP<sup>val<br>0.5 |Speed<br><sup>V100 (ms) | |params<br><sup>(M) |FLOPS<br><sup>640 (B)
---   |---                   |---                     |---                      |---                |---                     |---|---              |---
[YOLOv3-tiny][assets3] |640  |17.6     |17.6     |34.8     |**1.2** | |8.8   |13.2
[YOLOv3][assets3]      |640  |43.3     |43.3     |63.0     |4.1     | |61.9  |156.3
[YOLOv3-SPP][assets3]  |640  |44.3     |44.3     |64.6     |4.1     | |63.0  |157.1
| | | | | | || |
[YOLOv5l][assets5]     |640  |**48.2** |**48.2** |**66.9** |3.7     | |47.0  |115.4


<details>
  <summary>Table Notes (click to expand)</summary>
  
  * AP<sup>test</sup> denotes COCO [test-dev2017](http://cocodataset.org/#upload) server results, all other AP results denote val2017 accuracy.  
  * AP values are for single-model single-scale unless otherwise noted. **Reproduce mAP** by `python test.py --data coco.yaml --img 640 --conf 0.001 --iou 0.65`  
  * Speed<sub>GPU</sub> averaged over 5000 COCO val2017 images using a GCP [n1-standard-16](https://cloud.google.com/compute/docs/machine-types#n1_standard_machine_types) V100 instance, and includes FP16 inference, postprocessing and NMS. **Reproduce speed** by `python test.py --data coco.yaml --img 640 --conf 0.25 --iou 0.45`  
  * All checkpoints are trained to 300 epochs with default settings and hyperparameters (no autoaugmentation). 
</details>


## Requirements

Python 3.8 or later with all [requirements.txt](https://github.com/ultralytics/yolov3/blob/master/requirements.txt) dependencies installed, including `torch>=1.7`. To install run:
```bash
$ pip install -r requirements.txt
```

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

To run inference on example images in `data/images`:
```bash
$ python detect.py --source data/images --weights colorchecker.pt --conf 0.25
```
<img width="500" src="https://github.com/tckrishna/colorchecker/blob/1ce33c44706e4c61fb41082c3814fdbed1113e36/data/images/test_batch1_pred.jpg">  

### PyTorch Hub

To run **batched inference** with YOLOv5 and [PyTorch Hub](https://github.com/ultralytics/yolov5/issues/36):
```python
import torch

# Model
model = torch.hub.load('ultralytics/yolov3', 'yolov3')  # or 'yolov3_spp', 'yolov3_tiny'

# Image
img = 'https://ultralytics.com/images/zidane.jpg'

# Inference
results = model(img)
results.print()  # or .show(), .save()
```


## Training

Run commands below to reproduce results on [COCO](https://github.com/ultralytics/yolov3/blob/master/data/scripts/get_coco.sh) dataset (dataset auto-downloads on first use). Training times for YOLOv3/YOLOv3-SPP/YOLOv3-tiny are 6/6/2 days on a single V100 (multi-GPU times faster). Use the largest `--batch-size` your GPU allows (batch sizes shown for 16 GB devices).
```bash
$ python train.py --data coco.yaml --cfg yolov3.yaml      --weights '' --batch-size 24
                                         yolov3-spp.yaml                            24
                                         yolov3-tiny.yaml                           64
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
