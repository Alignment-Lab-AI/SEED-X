# SEED-X
[![arXiv](https://img.shields.io/badge/arXiv-2404.14396-b31b1b.svg)](https://arxiv.org/abs/2404.14396)
[![Demo](https://img.shields.io/badge/ARC-Demo-blue)](https://arc.tencent.com/en/ai-demos/multimodal)
[![Static Badge](https://img.shields.io/badge/Model-Huggingface-yellow)](https://huggingface.co/AILab-CVC/SEED-X-17B)
[![arXiv](https://img.shields.io/badge/arXiv-2405.04007-b31b1b.svg)](https://arxiv.org/abs/2405.04007)
[![Static Badge](https://img.shields.io/badge/Dataset-Huggingface-yellow)](https://huggingface.co/datasets/AILab-CVC/SEED-Data-Edit)

We introduce [SEED-X](https://arxiv.org/abs/2404.14396), a unified and versatile foundation model, which can serve as various multimodal AI assistants **in the real world** after different instruction tuning, capable of responding to a variety of user needs through unifying **multi-granularity comprehension and generation**.

All models, instruction tuning code and inference code are released! 

## News
**2024-07-12** :hugs: We release [SEED-Story](https://github.com/TencentARC/SEED-Story), a MLLM capable of generating multimodal long stories based on the pre-trained SEED-X (an earlier version). We also release StoryStream, a large-scale dataset designed for training and benchmarking multimodal story generation.

**2024-05-21** :hugs: A new online [demo](https://arc.tencent.com/en/ai-demos/multimodal) of the general instruction-tuned model SEED-X-I is available, with faster inference speed than the demo using Zero GPU on huggingface.

**2024-05-03** :hugs: We release **3.7M image editing data** [SEED-Data-Edit](https://huggingface.co/datasets/AILab-CVC/SEED-Data-Edit), which includes (1) Large-scale high-quality editing data produced by an **automatic pipeline**, (2) **Real-world scenario data** scraped from the internet that more accurately reflects user image editing intentions, (3) High-precision **multi-turn** editing data annotated by Photoshop experts.

**2024-05-02** :hugs: We release the **training code** for instruction tuning from the pre-trained foundation model **SEED-X**. Our codebase supports (a) large-scale multi-node training with deepspeed zero-2 and zero-3, (b) highly-efficient multiple training datapipes. To the best of our knowledge, our SEED series is the first open-source work on training MLLM that unifies multimodal comprehension and generation.

**2024-04-27** :hugs: We release the [models](https://huggingface.co/AILab-CVC/SEED-X-17B) including the pre-trained foundation model **SEED-X**, the general instruction-tuned model **SEED-X-I**, the editing model **SEED-X-Edit**, and our de-tokenier, which can generate realistic images from ViT features (w/o or w/ a condition image).

**2024-04-22** :hugs: We release an online [gradio demo](https://huggingface.co/spaces/tttoaster/SEED-X-17B) of a general instruction-tuned model SEED-X-I. SEED-X-I can follow multimodal instruction (including images with dynamic resolutions) and make responses with images, texts and bounding boxes in multi-turn conversation. SEED-X-I **does not support image manipulation**. If you want to experience SEED-X-Edit for high-precision image editing, the inference code and model will be released soon.

## TODOs
- [x] Release the multimodal foundation model SEED-X.
- [x] Release the instruction-tuned model SEED-X-Edit for high-precision image editing.
- [x] Release 3.7M in-house image editing data.
- [x] Release trainig code for instruction tuning.

## Introduction
![image](https://github.com/AILab-CVC/SEED-X/blob/main/demos/teaser.jpg?raw=true)

![image](https://github.com/AILab-CVC/SEED-X/blob/main/demos/case_example.jpg?raw=true)
The introduced SEED-X, a unified and versatile foundation model, can serve as various multimodal AI assistants **in the real world** after different instruction tuning, capable of responding to a variety of user needs through unifying
**multi-granularity comprehension and generation**. Our instruction tuned models can
function as an interactive designer, generating images without descriptive captions while illustrating
creative intent, and showcasing visualizations of modified images based on user’s intent. They can act
as knowledgeable personal assistants, comprehending images of arbitrary sizes and offering relevant
suggestions in multi-turn conversations.

![image](https://github.com/AILab-CVC/SEED-X/blob/main/demos/combination_seed_x.jpg?raw=true)
SEED-X is able to take multiple images as input, and follow its aesthetic vision and transform mediocre (or even low-resolution and low-quality) photos into something more impressive (In the example above, some of the input images have a resolution lower than 200). Feel free to try it by yourself in [demo](https://arc.tencent.com/en/ai-demos/multimodal) (Set "Force Image Generation" as True).

## [SEED-Data-Edit](https://huggingface.co/datasets/AILab-CVC/SEED-Data-Edit)
![image](https://github.com/AILab-CVC/SEED-X/blob/main/demos/SEED-Data-Edit.jpg?raw=true)
Data examples of instruction-guided image editing in SEED-Data-Edit, which includes (1)
High-quality editing data produced by an **automatic pipeline** (first row), (2) **Real-world scenario
data** scraped from the internet that more accurately reflects user image editing intentions (second
row), (3) High-precision **multi-turn** editing data annotated by Photoshop experts (third row).

## [SEED-Story](https://github.com/TencentARC/SEED-Story)
The introduced SEED-Story, powered by SEED-X, is capable of **generating multimodal long stories** from user-provided images and texts as the beginning of the story. The generated story consists of rich and coherent narrative texts, along with images that are consistent in characters and style. The story can span up to 25 multimodal sequences, even though we only use a maximum of 10 sequences during training.

![image](https://github.com/TencentARC/SEED-Story/blob/master/assets/teaser.jpg)

## Usage

### Dependencies
- Python >= 3.8 (Recommend to use [Anaconda](https://www.anaconda.com/download/#linux))
- [PyTorch >=2.0.1](https://pytorch.org/)
- NVIDIA GPU + [CUDA](https://developer.nvidia.com/cuda-downloads)

### Installation
Clone the repo and install dependent packages

  ```bash
  git clone https://github.com/AILab-CVC/SEED-X.git
  cd SEED-X
  pip install -r requirements.txt
  ```

### Model Weights
We release the pretrained De-Tokenizer, the pre-trained foundation model **SEED-X**, the general instruction-tuned model **SEED-X-I**, the editing model **SEED-X-Edit** in in [SEED-X-17B Hugging Face](https://huggingface.co/AILab-CVC/SEED-X-17B).

You can also download them separately as below,
- Check the SEED-X de-tokenizer weights in [AILab-CVC/seed-x-17b-de-tokenizer](https://huggingface.co/AILab-CVC/seed-x-17b-de-tokenizer)
- Check the pre-trained foundation model **SEED-X** weights in [AILab-CVC/seed-x-17b-pretrain](https://huggingface.co/AILab-CVC/seed-x-17b-pretrain)
- Check the general instruction-tuned model **SEED-X-I** weights in [AILab-CVC/seed-x-17b-instruct](https://huggingface.co/AILab-CVC/seed-x-17b-instruct)
- Check  the editing model **SEED-X-Edit** weights in [AILab-CVC/seed-x-17b-edit](https://huggingface.co/AILab-CVC/seed-x-17b-edit)

Please download the checkpoints and save them under the folder `./pretrained`. For example, `./pretrained/seed_x`.

You also need to download [stable-diffusion-xl-base-1.0](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) and [Qwen-VL-Chat](https://huggingface.co/Qwen/Qwen-VL-Chat), and save them under the folder `./pretrained`. Please use the following script to extract the weights of visual encoder in Qwen-VL-Chat.
```bash
python3 src/tools/reload_qwen_vit.py
```
### Inference
#### Inference with SEED-X De-tokenizer
```bash
# For image reconstruction with ViT image features
python3 src/inference/eval_seed_x_detokenizer.py
# For image reconstruction with ViT image features and conditional image
python3 src/inference/eval_seed_x_detokenizer_with_condition.py
```

#### Inference with pre-trained model SEED-X
```bash
# For image comprehension and detection
python3 src/inference/eval_img2text_seed_x.py
# For image generation
python3 src/inference/eval_text2img_seed_x.py
```

#### Inference with the general instruction-tuned model SEED-X-I
```bash
# For image comprehension and detection
python3 src/inference/eval_img2text_seed_x_i.py
# For image generation
python3 src/inference/eval_text2img_seed_x_i.py
```

#### Inference with the editing model SEED-X-Edit
```bash
# For image editing
python3 src/inference/eval_img2edit_seed_x_edit.py
```

### Instruction Tuning
#### Training
1. Prepare the pretrained models including the pre-trained foundation model **SEED-X** and the visual encoder of Qwen-VL-Chat (See Model Weights).
2. Prepare the instruction tuning data. For example, for "build_llava_jsonl_datapipes" dataloader, each folder stores a number of jsonl files, each jsonl file contains 10K pieces of content, with an example of the content as follows:
```bash
{"image": "coco/train2017/000000033471.jpg", "data": ["What are the colors of the bus in the image?", "The bus in the image is white and red.", "What feature can be seen on the back of the bus?", "The back of the bus features an advertisement.", "Is the bus driving down the street or pulled off to the side?", "The bus is driving down the street, which is crowded with people and other vehicles."]}
```

For "build_caption_datapipes_with_pixels" dataloder, each folder stores a number of .tar files and reads image-text pairs in the form of webdataset.

For "build_single_turn_edit_datapipes" dataloder,  each folder stores a number of jsonl files, each jsonl file contains 10K pieces of content, with an example of the content as follows:
```bash
{"source_image": "source_images/f6f4d0669694df5b.jpg", "target_image": "target_images/f6f4d0669694df5b.jpg", "instruction": "Erase the car that is parked in front of the Roebuck building."}
```
3. Run the following script.

```bash
# For general instruction tuning for multimodal comprehension and generation
sh scripts/train_seed_x_sft_comp_gen.sh
```

```bash
# For training language-guided image editing
sh scripts/train_seed_x_sft_edit.sh
```
#### Inference with your own model
1. Obtain "pytorch_model.bin" with the following script.
```bash
cd train_output/seed_x_sft_comp_gen/checkpoint-xxxx
python3 zero_to_fp32.py . pytorch_model.bin
```
2. Change "pretrained_model_path" in "configs/clm_models/agent_seed_x.yaml" with the new checkpoint. For example,
```bash
pretrained_model_path: train_output/seed_x_sft_comp_gen/checkpoint-4000/pytorch_model.bin
```
3. Change the "llm_cfg_path" and "agent_cfg_path" in the inference script (See below), which will automatically load the trained LoRA weights onto the pretrained model SEED-X.
```bash
llm_cfg_path = 'configs/clm_models/llm_seed_x_lora.yaml'
agent_cfg_path = 'configs/clm_models/agent_seed_x.yaml'
```
4. Run the inference script,
```bash
# For image comprehension
python3 src/inference/eval_img2text_seed_x_i.py
# For image generation
python3 src/inference/eval_text2img_seed_x_i.py
# For image editing
python3 src/inference/eval_img2edit_seed_x_edit.py
```


## Citation
If you find the work helpful, please consider citing:
```bash
@article{ge2024seed,
  title={SEED-X: Multimodal Models with Unified Multi-granularity Comprehension and Generation},
  author={Ge, Yuying and Zhao, Sijie and Zhu, Jinguo and Ge, Yixiao and Yi, Kun and Song, Lin and Li, Chen and Ding, Xiaohan and Shan, Ying},
  journal={arXiv preprint arXiv:2404.14396},
  year={2024}
}
```


## License
`SEED` is licensed under the Apache License Version 2.0 except for the third-party components listed in [License](License_Seed-X.txt). 

During training SEED-X, we freeze the original parameters of LLaMA2 and optimize the LoRA module.
