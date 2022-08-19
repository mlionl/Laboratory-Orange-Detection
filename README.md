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

More information: https://github.com/wkentaro/labelme

## *Model*

Detectron2 was the model implemented. 




## *Results*

https://user-images.githubusercontent.com/102746511/185192696-3ff55731-2923-49e2-9107-3e25749447dc.mp4

## *Discussion*




## *Next steps*
