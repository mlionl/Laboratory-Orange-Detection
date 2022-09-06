# Orange-Detection

## *Description*

Inspired by some papers and articles, I took pictures of citrus trees in a countryside near Seville during the harvest season. Establishing a first approach of a system for localization and estimating the number of oranges is the main goal of this repository. Estimating the number of fruits is a really complex task that is carried out by very experienced farmers. It is a crucial task so a more efficient estimation method could be beneficial for the farmer. 

## *Data*

Images were taken by a drone, due to time and resources limitations I only labeled 13 images using Labelme Tool. I labeled each fruits of the trees one by one using rectangular mode. So at the end, I got 13 json files that represent the coordenates of each fruits.

*Some examples of the data:*

<p float="left">
  <img src="https://user-images.githubusercontent.com/102746511/185049214-bc091664-866f-473a-8054-b515afe555fc.JPG" width="240" />
  <img src="https://user-images.githubusercontent.com/102746511/185050224-416f2e01-6a88-48ee-9c4e-f7edd4191f4e.JPG" width="240" /> 
  <img src="https://user-images.githubusercontent.com/102746511/185050290-19eaa08b-a330-4e58-af20-d43381b24025.JPG" width="240" />
  <img src="https://user-images.githubusercontent.com/102746511/185050473-49a06099-0f8f-4199-9cf4-65e82666072f.JPG" width="240" />
</p>

### *Labeling process*

Labelme is an open source tool for labeling images. I created rectangular labels so I got 13 json files with follow structure:
```
   {
      "label": "naranja",
      "points": [
        [
          2251.1627906976746,
          705.2093023255815
        ],
        [
          2355.813953488372,
          816.8372093023256
        ]
      ],
      "group_id": null,
      "shape_type": "rectangle",
      "flags": {}
    }
    ...
```
- Label: Name of label.
- Points: Coordenates  [xmin, ymin, xmax, ymax]
- group_id: --
- Shape_type: Shape's type of label
- Flags: --

More information: https://github.com/wkentaro/labelme.

The model choosen is fed with labels in coco format so a transformation of the format Labelme to coco is mandatory.

## *Model*

Detectron2 is Facebook AI Research's next generation library that provides state-of-the-art detection and segmentation algorithms. We can find all resources of Detectron2 at https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md. In this project I implemented a COCO-Detection/faster_rcnn_R_50_FPN_3x model. The election of the model was based on the architecture, labeling mode and format, the ratio train time, inference time and BOX AP.

More information Faster RCNN: https://arxiv.org/abs/1506.01497

## *Training*

The training was running on Google Collab, using GPU to speed up the process. I set these parameters:

```
- cfg.OUTPUT_DIR=OUTPUT_DIR -> Output directory where model will be saved.
- cfg.merge_from_file(model_zoo.get_config_file("COCO-Detection/faster_rcnn_R_50_FPN_3x.yaml")) -> Set the Architecture.
- cfg.DATASETS.TRAIN = ("dataset_naranja_train",) -> Set train set.
- cfg.DATASETS.TEST = ("dataset_naranja_test",) -> Set test set.
- cfg.DATALOADER.NUM_WORKERS = 1 ->
- cfg.MODEL.WEIGHTS = model_zoo.get_checkpoint_url("COCO-Detection/faster_rcnn_R_50_FPN_3x.yaml") -> Load weights
- cfg.SOLVER.IMS_PER_BATCH = 1 -> Images per batch
- cfg.SOLVER.BASE_LR = 0.0025 -> Learning Rate.
- cfg.SOLVER.MAX_ITER = 20000 -> Number of iterations
- cfg.SOLVER.STEPS = []  ->
- cfg.MODEL.ROI_HEADS.NUM_CLASSES = 1 -> Number of classes.
- cfg.SOLVER.CHECKPOINT_PERIOD = 1000 -> Save checkpoint each X iterations
- cfg.MODEL.ROI_HEADS.BATCH_SIZE_PER_IMAGE = 100 ->
- cfg.TEST.EVAL_PERIOD = 1000 -> Test evaluation each X iterations
```

## *Results*
 
 Evaluation results for bbox: 

|   AP   |  AP50  |  AP75  |  APs  |  APm   |  APl   |
|:------:|:------:|:------:|:-----:|:------:|:------:|
| 15.703 | 50.659 | 3.366  | 0.000 | 16.093 | 15.875 |


Coco format has an specific evaluation method. Average precision is the main metric for evaluate this problems, for more info about it: https://cocodataset.org/#detection-eval

AP could take values form 0 to 100. At this point, General AP is 15,703%. AP50 means the AP whe Intersection Over Union (Threshold) is 0.5. AP50 is 50.659%.

https://user-images.githubusercontent.com/102746511/185192696-3ff55731-2923-49e2-9107-3e25749447dc.mp4

## *Discussion*

## *Next steps*
