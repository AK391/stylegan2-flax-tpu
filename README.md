# StyleGAN2 Flax TPU


This implementation is adapted from the [stylegan2](https://github.com/matthias-wright/flaxmodels/tree/main/flaxmodels/stylegan2) codebase by [Matthias Wright](https://github.com/matthias-wright).

Specifically, the features we've added allow for better scaling of [StyleGAN2](https://arxiv.org/abs/1912.04958) training on TPUs:
* 🏭 Enable data-parallel training on TPU pods (tested on TPU v2 to v4 generations)
* 💾 Google Cloud Storage (GCS) integration/dataset sharding between workers
* 🏖 Quality-of-life improvements (e.g. improved W&B logging)

**[This food does not exist! Click to see more samples 🍪🍰🍣🍹](https://nyx-ai.github.io/stylegan2-flax-tpu/)**

[![These Cookies Do Not Exist](https://user-images.githubusercontent.com/140592/179369671-32cf8c67-a3d5-43a4-a200-1ba91e736ae2.png)](https://nyx-ai.github.io/stylegan2-flax-tpu/)

## 🧑‍🔧 Install
1. Clone the repository:
   ```sh
   git clone https://github.com/nyx-ai/stylegan2-flax-tpu.git
   ```
2. Go into the directory:
   ```sh
   cd stylegan2-flax-tpu
   ```
3. Install [Jax](https://github.com/google/jax#installation) according to your platform.
4. Install requirements:
   ```sh
   pip install -r requirements.txt
   ```

## 🖼 Generate Images

We released four 256x256 pretrained models: cookie, cheesecake, sushi and cocktail. Download them from the [latest release](https://github.com/nyx-ai/stylegan2-flax-tpu/releases).

```
python generate_images.py \
   --checkpoint checkpoints/cookie-256.pkl \
   --seeds 0 42 420 666 \
   --truncation_psi 0.7 \
   --out_path generated_images
```

Check the Colab notebook for more examples: 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nyx-ai/stylegan2-flax-tpu/blob/master/notebook/image_generation.ipynb)


## ⚙️ Train Custom Models
Add your images into a folder `/path/to/image_dir`:
```
/path/to/image_dir/
    0.jpg
    1.jpg
    2.jpg
    4.jpg
    ...
```
and create a TFRecord dataset:
```sh
python dataset_utils/images_to_tfrecords.py --image_dir /path/to/image_dir/ --data_dir /path/to/tfrecord
```
For more detailed instructions please refer to [this README](https://github.com/matthias-wright/flaxmodels/tree/main/training/stylegan2#preparing-datasets-for-training).

The following command trains with 128 resolution and batch size of 8.
```sh
python main.py --data_dir /path/to/tfrecord
```
Read more about suitable training parameters [here](https://github.com/matthias-wright/flaxmodels/tree/main/training/stylegan2#training).

## 🙏 Acknowledgements
* This work is based on Matthias Wright's [stylegan2](https://github.com/matthias-wright/flaxmodels/tree/main/training/stylegan2) implementation.
* The project received generous support from [Google's TPU Research Cloud (TRC)](https://sites.research.google/trc/about/).
