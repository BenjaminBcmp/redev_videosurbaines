| Nom                  | Backbone   | Type      | tpsInfMoy (en s) | boxAP | maskAP | PQ   | Taille (en MB) |
|----------------------|------------|-----------|------------------|-------|--------|------|----------------|
| Faster R-CNN         | R50-FPN    | Object(2) | 0.12             | 40.2  | -      | -    | 160            |
| Faster R-CNN         | X101-FPN   | Object(2) | 0.27             | 43.0  | -      | -    | 401            |
| YOLOv3-608           | Darknet-53 | Object(1) | 0.053            | 31.0  | -      | -    | 237            |
| Tiny YOLOv3          | -          | Object(1) | 0.01             | 6.4   | -      | -    | 34             |
| RetinaNet            | R101       | Object(1) | 0.22             | 39.9  | -      | -    | 228            |
| Mask R-CNN           | R50-FPN    | Instance  | 0.16             | 41.0  | 37.2   | -    | 178            |
| Mask R-CNN           | X101-FPN   | Instance  | 0.30             | 44.3  | 39.5   | -    | 431            |
| Cascade (Mask) R-CNN | R50        | Instance  | 0.18             | 44.3  | 38.5   | -    | 288            |
| Panoptic FPN         | R50-FPN    | Panoptic  | 0.21             | 40.0  | 36.5   | 41.5 | 184            |
| Panoptic FPN         | R101-FPN   | Panoptic  | 0.25             | 42.4  | 38.5   | 43.0 | 261            |