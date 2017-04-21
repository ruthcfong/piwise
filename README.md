# PiWiSe

Pixel-wise segmentation on the [VOC2012][dataset] dataset using
[pytorch][pytorch].

- [x] [FCN](https://arxiv.org/abs/1605.06211)
- [x] [SegNet](https://arxiv.org/abs/1511.00561)
- [x] [PSPNet](https://arxiv.org/abs/1612.01105)
- [x] [UNet](https://arxiv.org/abs/1505.04597)
- [ ] [RefineNet](https://arxiv.org/abs/1611.06612)

## Setup

See dataset examples [here][dataset_example].

### Download

Download [image archive][dataset_download] and extract and do:

```
mkdir data
mv VOCdevkit/VOC2012/JPEGImages data/images
mv VOCdevkit/VOC2012/SegmentationClass data/labels
rm -rf VOCdevkit
```

### Install

We recommend using [pyenv][pyenv]:

```
pyenv virtualenv 3.6.0 piwise
pyenv activate piwise
```

then install requirements with `pip install -r requirements.txt`.

## Usage

For latest documentation use:

```
python main.py --help
```

Supported model parameters are `fcn8`, `fcn16`, `fcn32`, `unet`, `segnet1`,
`segnet2`, `pspnet`.

### Training

If you want to have visualization open an extra tab with:

```
python -m visdom.server -port 5000
```

Train the SegNet model 30 epochs with cuda support, visualization
and checkpoints every 100 steps:

```
python main.py --cuda --model segnet2 train --datadir data \
    --num-epochs 30 --num-workers 4 --batch-size 4 \
    --steps-plot 50 --steps-save 100
```

### Evaluation


Then we want to do semantic segmentation on `foo.jpg`:

```
python main.py --model segnet2 --state segnet2-30-0 eval foo.jpg foo.png
```

The segmented class image can now be found at `foo.png`.

[pyenv]: https://github.com/pyenv/pyenv
[pytorch]: http://pytorch.org
[dataset]: http://host.robots.ox.ac.uk/pascal/VOC/
[dataset_example]: http://host.robots.ox.ac.uk/pascal/VOC/voc2012/segexamples
[dataset_download]: http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
