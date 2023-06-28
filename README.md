<div align="center">
  
# 【CVPR'2023 Highlight🔥】Video-Text as Game Players: Hierarchical Banzhaf Interaction for Cross-Modal Representation Learning
  
[![Conference](http://img.shields.io/badge/CVPR-2023(Highlight)-FFD93D.svg)](https://cvpr.thecvf.com/)
[![Project](http://img.shields.io/badge/Project-HBI-4D96FF.svg)](https://jpthu17.github.io/HBI/)
[![Paper](http://img.shields.io/badge/Paper-arxiv.2303.14369-FF6B6B.svg)](https://arxiv.org/abs/2303.14369)
</div>

The implementation of CVPR 2023 Highlight (Top 10%) paper [Video-Text as Game Players: Hierarchical Banzhaf Interaction for Cross-Modal Representation Learning](https://arxiv.org/abs/2303.14369).

In this paper, we creatively model video-text as game players with multivariate cooperative game theory to wisely handle the uncertainty during fine-grained semantic interaction with diverse granularity, flexible combination, and vague intensity.

## 📌 Citation
If you find this paper useful, please consider staring 🌟 this repo and citing 📑 our paper:
```
@inproceedings{jin2023video,
  title={Video-text as game players: Hierarchical banzhaf interaction for cross-modal representation learning},
  author={Jin, Peng and Huang, Jinfa and Xiong, Pengfei and Tian, Shangxuan and Liu, Chang and Ji, Xiangyang and Yuan, Li and Chen, Jie},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={2472--2482},
  year={2023}
}
```

## ⚡ Demo
<div align="center">
  
https://user-images.githubusercontent.com/53246557/221760113-4a523e7e-d743-4dff-9f16-357ab0be0d5b.mp4
</div>

## 📣 Updates
* Mar 28 2023: Our **HBI** has been selected as a Highlight paper at CVPR 2023! (Top 2.5% of 9155 submissions).
* Feb 28 2023: We will release the code asap. No later than the end of May. (I am busy with other DDLs. After that, I will open the source code as soon as possible. Please understand.)


## 😍 Visualization

### Example 1
<div align=center>
<img src="static/images/Visualization_1.png" width="800px">
</div>

<details>
<summary><b>More examples</b></summary>
  
### Example 2
<div align=center>
<img src="static/images/Visualization_2.png" width="800px">
</div>

### Example 3
<div align=center>
<img src="static/images/Visualization_3.png" width="800px">
</div>

### Example 4
<div align=center>
<img src="static/images/Visualization_4.png" width="800px">
</div>

### Example 5
<div align=center>
<img src="static/images/Visualization_5.png" width="800px">
</div>

### Example 6
<div align=center>
<img src="static/images/Visualization_6.png" width="800px">
</div>

### Example 7
<div align=center>
<img src="static/images/Visualization_0.png" width="800px">
</div>

</details>

## 🚀 Quick Start
### Setup

#### Setup code environment
```shell
conda create -n HBI python=3.9
conda activate HBI
pip install -r requirements.txt
pip install torch==1.8.1+cu102 torchvision==0.9.1+cu102 -f https://download.pytorch.org/whl/torch_stable.html
```

#### Download CLIP Model
```shell
cd HBI/models
wget https://openaipublic.azureedge.net/clip/models/40d365715913c9da98579312b702a82c18be219cc2a73407c4526f58eba950af/ViT-B-32.pt
# wget https://openaipublic.azureedge.net/clip/models/5806e77cd80f8b59890b7e101eabd078d9fb84e6937f9e85e4ecb61988df416f/ViT-B-16.pt
# wget https://openaipublic.azureedge.net/clip/models/b8cca3fd41ae0c99ba7e8951adf17d267cdb84cd88be6f7c2e0eca1737a03836/ViT-L-14.pt
```

#### Download Datasets
<div align=center>

|Datasets|Google Cloud|Baidu Yun|Peking University Yun|
|:--------:|:--------------:|:-----------:|:-----------:|
| MSR-VTT | [Download](https://drive.google.com/drive/folders/1LYVUCPRxpKMRjCSfB_Gz-ugQa88FqDu_?usp=sharing) | TODO | [Download](https://disk.pku.edu.cn:443/link/BE39AF93BE1882FF987BAC900202B266) |
| MSVD | [Download](https://drive.google.com/drive/folders/18EXLWvCCQMRBd7-n6uznBUHdP4uC6Q15?usp=sharing) | TODO | [Download](https://disk.pku.edu.cn:443/link/CC02BD15907BFFF63E5AAE4BF353A202) |
| ActivityNet | TODO | TODO | [Download](https://disk.pku.edu.cn:443/link/83351ABDAEA4A17A5A139B799BB524AC) |
| DiDeMo | TODO | TODO | [Download](https://disk.pku.edu.cn:443/link/BBF9F5990FC4D7FD5EA9777C32901E62) |

</div>

#### Train the Banzhaf Interaction Estimator

Train the estimator according to the label generated by the BanzhafInteraction in HBI/models/banzhaf.py.

```sh
Code is under preparation...
```

### Text-video Retrieval
<div align=center>

|Checkpoint|Google Cloud|Baidu Yun|Peking University Yun|
|:--------:|:--------------:|:-----------:|:-----------:|
| MSR-VTT | [Download](https://drive.google.com/file/d/1hoV9vsT0-KIjjIRPIB9D4dMXwrckvSLk/view?usp=sharing) | TODO | [Download](https://disk.pku.edu.cn:443/link/424DFFAC5D2CB600E73BCB67C05A73FD) |

</div>

#### Eval on MSR-VTT
```shell
CUDA_VISIBLE_DEVICES=0,1 \
python -m torch.distributed.launch \
--master_port 2502 \
--nproc_per_node=2 \
main_retrieval.py \
--do_eval 1 \
--workers 8 \
--n_display 50 \
--batch_size_val 128 \
--anno_path data/MSR-VTT/anns \
--video_path ${DATA_PATH}/MSRVTT_Videos \
--datatype msrvtt \
--max_words 24 \
--max_frames 12 \
--video_framerate 1 \
--init_model ${CHECKPOINT_PATH} \
--output_dir ${OUTPUT_PATH} 
```

#### Train on MSR-VTT
```shell
CUDA_VISIBLE_DEVICES=0,1 \
python -m torch.distributed.launch \
--master_port 2502 \
--nproc_per_node=2 \
main_retrieval.py \
--do_train 1 \
--workers 8 \
--n_display 50 \
--epochs 5 \
--lr 1e-4 \
--coef_lr 1e-3 \
--batch_size 128 \
--batch_size_val 128 \
--anno_path data/MSR-VTT/anns \
--video_path ${DATA_PATH}/MSRVTT_Videos \
--datatype msrvtt \
--max_words 24 \
--max_frames 12 \
--video_framerate 1 \
--estimator ${ESTIMATOR_PATH} \
--output_dir ${OUTPUT_PATH} \
--kl 2 \
--skl 1
```

### Video-question Answering
<div align=center>

|Checkpoint|Google Cloud|Baidu Yun|Peking University Yun|
|:--------:|:--------------:|:-----------:|:-----------:|
| MSR-VTT-QA | [Download](https://drive.google.com/file/d/15GZXMaPvowL4GgxtB9ETvb8vivdcE8Wd/view?usp=sharing) | TODO | [Download](https://disk.pku.edu.cn:443/link/DE99ECAD7C1E7F550A2753B561086CDF) |

</div>

#### Eval on MSR-VTT-QA

```shell
CUDA_VISIBLE_DEVICES=0,1 \
python -m torch.distributed.launch \
--master_port 2502 \
--nproc_per_node=2 \
main_vqa.py \
--do_eval \ 
--num_thread_reader=8 \
--train_csv data/MSR-VTT/qa/train.jsonl \
--val_csv data/MSR-VTT/qa/test.jsonl \
--data_path data/MSR-VTT/qa/train_ans2label.json \
--features_path ${DATA_PATH}/MSRVTT_Videos \
--max_words 32 \
--max_frames 12 \
--batch_size_val 16 \
--datatype msrvtt \
--expand_msrvtt_sentences  \
--feature_framerate 1 \
--freeze_layer_num 0  \
--slice_framepos 2 \
--loose_type \
--linear_patch 2d \
--init_model ${CHECKPOINT_PATH} \
--output_dir ${OUTPUT_PATH}
```

#### Train on MSR-VTT-QA

```shell
CUDA_VISIBLE_DEVICES=0,1 \
python -m torch.distributed.launch \
--master_port 2502 \
--nproc_per_node=2 \
main_vqa.py \
--do_train \ 
--num_thread_reader=8 \
--epochs=5 \
--batch_size=32 \
--n_display=50 \
--train_csv data/MSR-VTT/qa/train.jsonl \
--val_csv data/MSR-VTT/qa/test.jsonl \
--data_path data/MSR-VTT/qa/train_ans2label.json \
--features_path ${DATA_PATH}/MSRVTT_Videos \
--lr 1e-4 \
--max_words 32 \
--max_frames 12 \
--batch_size_val 16 \
--datatype msrvtt \
--expand_msrvtt_sentences  \
--feature_framerate 1 \
--coef_lr 1e-3 \
--freeze_layer_num 0  \
--slice_framepos 2 \
--loose_type \
--linear_patch 2d \
--estimator ${ESTIMATOR_PATH} \
--output_dir ${OUTPUT_PATH} \
--kl 2 \
--skl 1
```

## 🎗️ Acknowledgments
Our code is based on [EMCL](https://github.com/jpthu17/EMCL), [CLIP](https://github.com/openai/CLIP), [CLIP4Clip](https://github.com/ArrowLuo/CLIP4Clip/) and [DRL](https://github.com/foolwood/DRL). We sincerely appreciate for their contributions.
