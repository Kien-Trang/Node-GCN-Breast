## Requirements
The main packages for this project:
* `python==3.10`
* `torch==2.0.1`
* `torch_geometric==2.4.0`

## Preparation

The given dataset and processed data used in this work can be download from this [link](https://drive.google.com/drive/folders/1EsCotSBWpPonaduHS5Rya10YO4EXv8dT?usp=sharing). Please create and put them as the following structure:

```
node-GCN-breast
├── Dataset
│       ├── BUSBRA
│       |       ├── data-edge
│       |       |         ├── k2
│       |       |         ├── k4
│       |       |         ├── k6
│       |       |         └── k8
│       |       | 
│       |       └── original
|       |
│       └── BUSI-with-GT
│               ├── data-edge
│               |         ├── k2
│               |         ├── k4
│               |         ├── k6
│               |         └── k8
│               | 
│               └── original
|                 
├── dataloader.py
├── Graph-construct-v4-node-attr.ipynb
├── Graph-construct-v4-Patch-building.ipynb
├── models.py
├── Node-classify-and-Img-Classify.ipynb
├── utils.py
└── README.md

```
`** Note that`: each k folder can be downloaded and tested seperately, due to the extraction from zip file may take longer time.

## Step-by-step for running code
#### 1) Running Graph-construct-v4-Patch-building.ipynb



Setting the `dataset_name`, note that `dataset_name` can be `BUSI-with-GT` or `BUSBRA`.The number of `k` can be `2`, `4`, `6`, `8`. An example of `k` is as follows:
```python
# Selecting dataset and k
dataset_name = 'BUSI-with-GT'  # 'BUSI-with-GT' or  'BUSBRA' 
k = 6  # '2' '4' '6' '8'
```

The output of this file will generate in the two folder:
1. the raw folder, under the directory: 
```bash
./Dataset/<name of dataset>/data-edge/<train or test>/<number of k>/raw
```
* `<name of dataset>`: can be `BUSBRA` or `BUSI-with-GT`
* `<number of k>`: can be `k2`, `k4`, `k6`, `k8`
* `<train or test>`: can be `train` or `test`
Example: `./Dataset/BUSI-with-GT/data-edge/k6/train/raw`

2. the patch-image folder, under the directory: 
```bash
./Dataset/<name of dataset>/data-edge/<train or test>/<number of k>/patch-image
```
* `<name of dataset>`: can be `BUSBRA` or `BUSI-with-GT`
* `<number of k>`: can be `k2`, `k4`, `k6`, `k8`
* `<train or test>`: can be `train` or `test`
Example: `./Dataset/BUSI-with-GT/data-edge/k6/train/patch-image`

`**Note that:` The structure is similar to process the test folder (in the below cell)

##### [OPTIONAL] For manually setting the path

However, Setting the directory for input mask and output patch, the defaults setting are as follows:
```python
mask_dir = 'Dataset/BUSI-with-GT/original/Masks/'
patch_dir  = 'Dataset/BUSI-with-GT/data-edge/train/patch-image/'
```

In the working directories, the default settings are as follows:

```python
#working directories
benign_dir  = 'Dataset/BUSI-with-GT/original/train/benign'
malignant_dir  = 'Dataset/BUSI-with-GT/original/train/malignant'
normal_dir  = 'Dataset/BUSI-with-GT/original/train/normal'
```
Please specify the directory to each corresponding folder in case of other defined paths.




#### 2) Running Graph-construct-v4-node-attr.ipynb

Setting the option for forming a node attributes(features). Note that this part will continue to process the previous part, the directory should be the same as previous one. 


Setting the `dataset_name`, note that `dataset_name` can be `BUSI-with-GT` or `BUSBRA`.The number of `k` can be `2`, `4`, `6`, `8`. An example of `k` is as follows:
```python
# Selecting dataset and k
dataset_name = 'BUSI-with-GT'  # 'BUSI-with-GT' or  'BUSBRA' 
k = 6  # '2' '4' '6' '8'
```



The output of this part is `train_node_attributes.txt`, which is stored as the same directory of the previous part.

`**Note that:` The structure is similar to process the test folder (in the below cell)

##### [OPTIONAL] For manually setting the path
The example setting is:
```python
patch_dir  = 'Dataset/BUSI-with-GT/data-edge/k6/'
folder = 'train'
```

#### 3) Running Node-classify-and-Img-Classify.ipynb

Setting the option directory for training the node and for image classification

Setting the `dataset_name`, note that `dataset_name` can be `BUSI-with-GT` or `BUSBRA`.The number of `k` can be `2`, `4`, `6`, `8`. An example of `k` is as follows:
```python
# Selecting dataset and k
dataset_name = 'BUSI-with-GT'  # 'BUSI-with-GT' or  'BUSBRA' 
k = 6  # '2' '4' '6' '8'
```

Or can be adjust manually as follows:

```python
root_path = 'Dataset/BUSI-with-GT/data-edge/k6/'
mask_dir = 'Dataset/BUSI-with-GT/original/Masks/'
base_dir = 'Dataset/BUSI-with-GT/original/test/'
```

For the `root_path` can be adjust the dataset and number of k similar to the previous ones. The `mask_dir` and `base_dir` is storing the Masks and test set of orignal corresponding dataset (can be BUSBRA or BUSI-with-GT)


# Citations

```
@article{kien2024ngcn,
  title={Node-Based Graph Convolutional Network With SLIC Method for Breast Cancer Ultrasound Images Classification},
  author={Kien Trang, Fung Fung Ting, Bao Quoc Vuong, and Chee-Ming Ting},
  journal={IEEE Access},
  volume={12},
  pages={171036 - 171054},
  year={2024},
  publisher={IEEE}
}
```
