# Learning To Invert: Simple Adaptive Attacks for Gradient Inversion in Federated Learning
This code corresponds to the following paper:

Ruihan Wu, Xiangyu Chen, Chuan Guo, and Kilian Q. Weinberger. [Learning To Invert: Simple Adaptive Attacks for Gradient Inversion in Federated Learning](https://openreview.net/forum?id=deit1AdsFU). UAI 2023. 

## 1. Reproduce the Results of Vision Dataset (Table 1)
### 1.1 CIFAR10 and LeNet 
To reproduce the results in Table 1 for CIFAR10 and LeNet, run the following script for B=1 
```
python main_learn_dlg.py --lr 1e-4 --epochs 200 --leak_mode $leak_mode --model MLP-3000 --dataset CIFAR10 --batch_size 256 --shared_model LeNet
```
by setting `leak_mode` as `None`, `sign`, `prune-0.99`, `gauss-0.1`.

Run the script below for B=4
```
python main_learn_dlg.py --lr 1e-4 --epochs 5000 --leak_mode $leak_mode --model MLP-10000 --dataset CIFAR10 --batch_size 256 --shared_model LeNet
```
by setting `leak_mode` as `batch-4`, `sign-batch-4`, `prune-0.99-batch-4`, `gauss-0.1-batch-4`.


### 1.2 CIFAR10 and ResNet20
To reproduce the results in Table 1 for CIFAR10 and ResNet, run the following script for B=1 
```
python main_learn_dlg_large_model.py --lr 1e-4 --epochs 40 --leak_mode $leak_mode --model MLP-3000 --dataset CIFAR10-hash --batch_size 256 --shared_model ResNet20
```
by setting `leak_mode` as `None`, `sign`, `prune-0.99`, `gauss-0.1`.

Run the following script for B=4
```
python main_learn_dlg_large_model.py --lr 1e-4 --epochs 200 --leak_mode prune-0.99-batch-4 --model MLP-3000 --dataset CIFAR10-hash --batch_size 256 --shared_model ResNet20
```
by setting `leak_mode` as `batch-4`, `sign-batch-4`, `prune-0.99-batch-4`, `gauss-0.1-batch-4`.

## 2. Reproduce the Results of Language Dataset (Table 1)
### 2.1 COLA and BERT
To reproduce the results in Table 1 for COLA and BERT, run the following script
```
python main_learn_dlg_large_model.py --epochs 100 --batch_size 16 --dataset cola-hash --shared_model BERT --model NLPMLP-600-1000 --lr $lr --leak_mode $leak_mode
```
by setting `(leak_mode, lr)` as `(None, 1e-3)`, `(sign, 1e-5)`, `(prune-0.99, 1e-3)`, `(gauss-0.001, 1e-4)`.

### 2.2 Wikitext and 3-Layers Transformers
To reproduce the results in Table 1 for COLA and BERT, run the following script
```
python main_learn_dlg_large_model.py --epochs 100 --batch_size 64 --dataset wikitext-hash --shared_model Transformer --model NLPMLP-600-1000 --lr $lr --leak_mode $leak_mode
```
by setting `(leak_mode, lr)` as `(None, 1e-3)`, `(sign, 1e-5)`, `(prune-0.99, 1e-3)`, `(gauss-0.001, 1e-4)`.

## Acknowledgement
We would like to thank the authors of [Breaching](https://github.com/JonasGeiping/breaching), from where we use their federated learning framework in our experiments for language datasets and models.
