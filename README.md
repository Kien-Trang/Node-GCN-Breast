## Requirements
The main packages for this project:
* `python==3.10`
* `torch==2.0.1`
* `torch_geometric==2.4.0`

## Preparation

## Step-by-step running code
#### 1) Running Graph-construct-v4-Patch-building.ipynb

Setting the directory for input mask and output patch, the defaults setting are as follows:
```python
mask_dir = 'Dataset/BUSI-with-GT/original/Masks/'
patch_dir  = 'Dataset/BUSI-with-GT/data-edge/train/patch-image/'
```

Setting the number of `k`, note that `k` can be `2, 4, 6, 8`. An example of `k` is as follows:
```python
# Selecting k
k = 6
```

In the working directories, the default settings are as follows:

```python
#working directories
benign_dir  = 'Dataset/BUSI-with-GT/original/train/benign'
malignant_dir  = 'Dataset/BUSI-with-GT/original/train/malignant'
normal_dir  = 'Dataset/BUSI-with-GT/original/train/normal'
```
Please specify the directory to each corresponding folder in case of other defined paths.

The output of this file will generate in the two folder:
1. the raw folder, under the directory: 
```bash
./Dataset/<name of dataset>/data-edge/<train or test>/<number of k>/raw
```
* `<name of dataset>`: can be `BUSBRA` or `BUSI-with-GT`
* `<number of k>`: can be `k3`, `k5`, `k7`, `k9`
* `<train or test>`: can be `train` or `test`
Example: `./Dataset/BUSI-with-GT/data-edge/k7/train/raw`

2. the patch-image folder, under the directory: 
```bash
./Dataset/<name of dataset>/data-edge/<train or test>/<number of k>/patch-image
```
* `<name of dataset>`: can be `BUSBRA` or `BUSI-with-GT`
* `<number of k>`: can be `k3`, `k5`, `k7`, `k9`
* `<train or test>`: can be `train` or `test`
Example: `./Dataset/BUSI-with-GT/data-edge/k7/train/patch-image`

`**Note that:` The structure is similar to process the test folder (in the below cell)


#### 2) Running Graph-construct-v4-node-attr.ipynb

Setting the directory for forming a node attributes(features). Note that this part will continue to process the previous part, the directory should be the same as previous one. 
The example setting is:
```python
patch_dir  = 'Dataset/BUSI-with-GT/data-edge/k7/'
folder = 'train'
```

The output of this part is `train_node_attributes.txt`, which is stored as the same directory of the previous part.

`**Note that:` The structure is similar to process the test folder (in the below cell)

#### 3) Running Node-classify-and-Img-Classify.ipynb

Setting the directory for training the node and for image classification

```python
root_path = 'Dataset/BUSI-with-GT/data-edge/k7/'
mask_dir = 'Dataset/BUSI-with-GT/original/Masks/'
base_dir = 'Dataset/BUSI-with-GT/original/test/'
```

For the `root_path` can be adjust the dataset and number of k similar to the previous ones. The `mask_dir` and `base_dir` is storing the Masks and test set of orignal corresponding dataset (can be BUSBRA or BUSI-with-GT)
