This repository reproduce VQA experiments of OFA model. 

As the original paper, we use the same dataset and evaluation metric as VQA v2.0. The dataset can be downloaded from [VQA v2.0](https://visualqa.org/download.html). The evaluation metric from [VQA v2.0](https://visualqa.org/evaluation.html). However, their preprocessing method results in a more than 100 GB zip file, which is difficult to download and unzip. I use the chunked version in https://github.com/OFA-Sys/OFA/issues/68#issuecomment-1096837349

```bash
bash download.sh
cd dataset/vqa_data
cat vqa_train_* > vqa_train.tsv
cat vqa_test_* > vqa_test.tsv
```

# Environment

```bash
export PYTHONPATH=$PYTHONPATH:/data/hzz5361/vision_and_lang/final/OFA/fairseq
export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python
```

# Evaluation

Download Pretrained Model 

The allcand evaluation is very demanding on GPU memory. As my RTX A5000 only has 24GB memory, I can only run the allcand evaluation with batch size 4. 


```bash
cd run_scripts/vqa
bash evaluate_vqa_beam_base.sh val
bash evaluate_vqa_base_allcand.sh val
```



# Results

<table border="1" width="100%">
    <tr align="center">
        <th>Task</th><th>Image Captioning</th><th>VQA</th><th>Visual Entailment</th><th colspan="3">Referring Expression Comprehension</th>
    </tr>
    <tr align="center">
        <td>Dataset</td><td>COCO</td><td>VQA v2</td><td>SNLI-VE</td><td>RefCOCO</td><td>RefCOCO+</td><td>RefCOCOg</td>
    </tr>
    <tr align="center">
        <td>Split</td><td>Karpathy test (CE/CIDEr)</td><td>test-dev/test-std</td><td>val/test</td><td>val/test-a/test-b</td><td>val/test-a/test-b</td><td>val-u/test-u</td>
    </tr>
    <tr align="center">
        <td>Metric</td><td>CIDEr</td><td>Acc.</td><td>Acc.</td><td colspan="3">Acc.</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Tiny</sub></td><td>119.0 / 128.7</td><td>70.3 / 70.4</td><td>85.3 / 85.2</td><td>80.20 / 84.07 / 75.00</td><td>68.22 / 75.13 / 57.66</td><td>72.02 / 69.74</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Medium</sub></td><td>130.4 / 140.3</td><td>75.4 / 75.5</td><td>86.6 / 87.0</td><td>85.34 / 87.68 / 77.92</td><td>76.09 / 83.04 / 66.25</td><td>78.76 / 78.58</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Base</sub></td><td>138.2 / 146.7</td><td>78.0 / 78.1</td><td>89.3 / 89.2</td><td>88.48 / 90.67 / 83.30</td><td>81.39 / 87.15 / 74.29</td><td>82.29 / 82.31</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Large</sub></td><td>142.2 / 150.7</td><td>80.4 / 80.7</td><td>90.3 / 90.2</td><td>90.05 / 92.93 / 85.26</td><td>85.80 / 89.87 / 79.22</td><td>85.89 / 86.55</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Huge</sub></td><td>145.3 / 154.9</td><td>82.0 / 82.0</td><td>91.0 / 91.2</td><td>92.04 / 94.03 / 88.44</td><td>87.86 / 91.70 / 80.71</td><td>88.07 / 88.78</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Base</sub></td><td>138.2 / 146.7</td><td>78.0 / 78.1</td><td>89.3 / 89.2</td><td>88.48 / 90.67 / 83.30</td><td>81.39 / 87.15 / 74.29</td><td>82.29 / 82.31</td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Base-Beam-3</sub></td><td> </td><td> 77.94/- </td><td></td><td></td><td></td><td></td>
    </tr>
    <tr align="center">
        <td>OFA<sub>Base-Beam-10</sub></td><td> </td><td> 77.56/- </td><td></td><td></td><td></td><td></td>
    </tr>
</table>
<br></br>