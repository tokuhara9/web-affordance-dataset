# Human and VLM Web Element Affordance Dataset

This repository contains the official dataset for the paper:
"Investigation of Cognitive Gaps between Humans and VLMs on Web Element Affordances and Its Application to User Support" (MMAsia '26).

## Overview
This benchmark dataset evaluates the perception of clickable elements (affordance) on web pages, comparing human intuitive judgments with Vision-Language Model (VLM, GPT-4o) estimations.

- Images: 1,000 screenshots collected from Japanese municipal homepages.
- Human Annotations: Cross-annotated by 4 human annotators (each image independently evaluated twice).
- VLM Annotations: Bounding boxes predicted by GPT-4o with manual coordinate corrections.
- Coordinate Format: Normalized relative coordinates [x, y, width, height] in the range [0.0, 1.0].

## Dataset Structure (dataset.json)

```json
[
  {
    "image_id": 1,
    "file_name": "aibetsu.png",
    "site_url": "https://www.town.aibetsu.hokkaido.jp/",
    "human_annotations": [
      {
        "box_id": 3860,
        "annotator_id": "annotator_1",
        "bbox": [0.1234, 0.5678, 0.2100, 0.0450]
      }
    ],
    "vlm_annotations": [
      {
        "box_id": 1,
        "bbox": [0.1230, 0.5675, 0.2105, 0.0452]
      }
    ]
  }
]
```

## Bounding Box Calculation
To convert normalized coordinates back to pixel values on an image with width W and height H:
- X_pixel = x * W
- Y_pixel = y * H
- Width_pixel = width * W
- Height_pixel = height * H

## Quickstart (Python)

```python
import json

with open('dataset.json', 'r', encoding='utf-8') as f:
    dataset = json.load(f)

print(f"Total Images: {len(dataset)}")
sample = dataset[0]
print(f"Sample Image: {sample['file_name']}")
print(f"Human Annotation Count: {len(sample['human_annotations'])}")
print(f"VLM Annotation Count: {len(sample['vlm_annotations'])}")
```

## Citation
If you use this dataset in your research, please cite our paper:

```bibtex
@inproceedings{tokuhara2026mmasia,
  title={Investigation of Cognitive Gaps between Humans and VLMs on Web Element Affordances and Its Application to User Support},
  author={Tokuhara, Mahiro and Kinoshita, Yuuichiro and Nakamura, Satoshi},
  booktitle={Proceedings of the 2026 ACM Multimedia Asia (MMAsia '26)},
  year={2026}
}
```

## License
This project is licensed under the MIT License - see the LICENSE file for details.
