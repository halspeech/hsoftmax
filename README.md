# hsoftmax
Implementation of hierarchical softmax based on Huffman tree

## Usage
Run the script as follows:  
```
python wenet/utils/huffman_tree.py \
--train-data ../egs/aishell/s1/fbank/train_sp/format.data \
--dict ../egs/aishell/s1/data/dict/lang_char.txt \
--tree-save-dir ../egs/aishell/s1/data/dict/tree
```
Add the following lines to train and test yaml files
```
hsoftmax:
    huffman_tree_dir: "dir/to/save"
    num_workers: 40 # number of CPU parallel workers for decoding
    beam_size: 10
```

## Description
This project is based on [wenet](https://github.com/wenet-e2e/wenet).
Please reference that for more info about running an experiment.

We only add and modify several files based on wenet:  
wenet/utils/huffman_tree.py: For building a Huffman tree based on frequencies of train set  
wenet/transformer/hsoftmax_layer.py: For GPU training and GPU/CPU decoding  
wenet/utils/multiprocessing.py: Helper classes included for parallel decoding in hsoftmax_layer.py  
wenet/transformer/asr_model.py: Several lines are added to enable hsoftmax  

## Performance
We reached a speedup in throughput of 1.14 in aishell using 30000 bpe tokens

## Implementation Details
![Implementation Details](implementation_details.jpg)
