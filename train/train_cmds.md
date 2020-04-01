# DeepLabv3
## Lancer l'entraînement

Préparation de l'environnement :
```bash
cd ~/redev/redev_videosurbaines
screen -S train
source .venv/bin/activate
```
Lancement de l'entraînement :

```bash
cd train/pytorch_seg_ref_scripts
python train.py --lr 0.02 --dataset coco -b 3 --model deeplabv3_resnet50 --aux-loss --output-dir "../deeplabv3_resnet50"
```

## Reprendre l'entraînement
