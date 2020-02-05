# Plan de test

## Motivation

Le but de ces tests est de pouvoir comparer les algorithmes entre eux autant que possible. Les algorithmes testés appartiennent à 4 catégories : détection d'objet, segmentation sémantique, segmentation d'instance et segmentation panoptique. Pour chaque catégorie, les sorties des algorithmes sont différentes mais certains scores permettent de comparer deux algorithmes appartenant à des catégories différentes.

## Données

Les algorithmes seront évalués sur le jeu de données `val_2017` de [COCO](http://cocodataset.org/#download) qui contient 5000 images, ce qui nécessite que les algorithmes à tester aient été entrainés sur `train_2017`. Des annotations sont disponibles pour ce jeu de données :

- Train/Val annotations : contient les bbox et les masques à l'intérieur de ces bbox pour la détection d'objet et la segmentation d'instance 
- Panoptic Train/Val annotations : contient les annotations pour la segmentation panoptique.

## Métriques

Différentes métriques seront évaluées suivant la catégorie à laquelle appartient l'algorithme. Les métriques sont :

- boxAP : AP mesuré sur les bbox
- maskAP : AP mesuré sur les masques à l'intérieur des bbox
- tpsInfMoy : temps d'inférence moyen par image
- PQ : panoptic quality
- mIoU : IoU moyen sur tous les masques prédits dans l'image

La taille (en MB) de chaque modèle sera aussi relevée.

## Outils

Les tests seront effectués sur [Google Colab](colab.research.google.com/) afin d'utiliser l'environnement d'exécution mis à disposition de chaque utilisateur.
L'inférence sera effectuée sur le GPU (certains algorithmes utilisent aussi le CPU en parallèle). Cet environnement comporte :

- GPU : Tesla P100 (16 Go de RAM)
- CPU : Intel(R) Xeon(R) CPU @ 2.00GHz (1 core)
- 13 Go de RAM

## Tableau récapitulatif

| Nom                  | Backbone     | Type      | Métriques                     | Code                                                                    | Licence                                                             | Notes                                                          |
|----------------------|--------------|-----------|------------------------------|----------------|-------------------------------------------------------------------------|---------------------------------------------------------------------|----------------------------------------------------------------|
| Faster R-CNN         | R50-FPN      | Object(2) | boxAP, tpsInfMoy              | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | Le plus rapide de detectron2 (prendre lr sched x3)             |
| Faster R-CNN         | X101-FPN     | Object(2) | boxAP, tpsInfMoy               | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | Le plus performant de detectron2 (prendre lr sched x3)         |
| YOLOv3-608           | Darknet-53   | Object(1) | boxAP, tpsInfMoy              | [Lien](https://pjreddie.com/darknet/yolo/)                                     | [Lien](https://github.com/pjreddie/darknet/blob/master/LICENSE)             | Entrainé sur COCO train+val 2014                               |
| Tiny YOLOv3          | -            | Object(1) | boxAP, tpsInfMoy              | [Lien](https://pjreddie.com/darknet/yolo/)                                     | [Lien](https://github.com/pjreddie/darknet/blob/master/LICENSE)             | Entrainé sur COCO train+val 2014                               |
| RetinaNet            | R101         | Object(1) | boxAP, tpsInfMoy              | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | Pas de test avec R50 car les temps d'inférence sont similaires |
| Mask R-CNN           | R50-FPN      | Instance  | boxAP, maskAP, tpsInfMoy      | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | Le plus rapide de detectron2 (prendre lr sched x3)             |
| Mask R-CNN           | X101-FPN     | Instance  | boxAP, maskAP, tpsInfMoy      | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | Le plus performant de detectron2 (prendre lr sched x3)         |
| Cascade (Mask) R-CNN | R50          | Instance  | boxAP, maskAP, tpsInfMoy      | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | lr sched x3                                                    |
| Panoptic FPN         | R50-FPN      | Panoptic  | boxAP, maskAP, PQ, tpsInfMoy  | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | lr sched x3                                                    |
| Panoptic FPN         | R101-FPN     | Panoptic  | boxAP, maskAP, PQ, tpsInfMoy  | [Lien](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md) | Apache 2.0                                                          | lr sched x3                                                    |
| DeepLabv3+           | WideResNet38 | Semantic  | mIoU                          | [Lien](https://github.com/NVIDIA/semantic-segmentation)                         | [Lien](https://github.com/NVIDIA/semantic-segmentation/blob/master/LICENSE) | A tester sur cityscape                                         |
Légende :

- R50/R101 : ResNet 50/101
- X101 : ResNeXt 101
- FPN : Feature Pyramid Network

## Remarques

L'environnement d'exécution de Google Colab est remis à zéro après une déconnexion ou toutes les 12h. Il faut donc avoir un script qui permet d'obtenir le même environnement d'exécution à chaque reconnexion. Il faut aussi s'assurer que le hardware fourni est le même à chaque connexion.

La segmentation sémantique n'est pas évaluée sur COCO car nous n'avons pas trouvé de modèles déjà entrainés (d'autres datasets sont plus populaires pour la segmentation sémantique). La métrique d'évaluation pour la segmentation sémantique est de toute façon différente des autres méthodes (mIoU vs AP) donc seul le temps d'inférence sera utilisable pour comparer DeepLab aux autres algorithmes.
