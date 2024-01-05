# LF_Transformer


---

## 1. Setup the environment

Install [conda](https://docs.conda.io/en/latest/miniconda.html)

```bash
export PROJECT_DIR=<ABSOLUTE path to the repository root>
# example: export PROJECT_DIR=/home/myusername/repositories/revisiting-models
git clone https://github.com/anonymityanonymityanonymity/LF_Transformer $PROJECT_DIR
cd $PROJECT_DIR

conda create -n LF_transformer python=3.8.8
conda activate LF_transformer

conda install pytorch==1.7.1 torchvision==0.8.2 cudatoolkit=10.1.243 numpy=1.19.2 -c pytorch -y
conda install cudnn=7.6.5 -c anaconda -y
pip install -r ./requirements.txt
conda install nodejs -y
jupyter labextension install @jupyter-widgets/jupyterlab-manager

# if the following commands do not succeed, update conda
conda env config vars set PYTHONPATH=${PYTHONPATH}:${PROJECT_DIR}
conda env config vars set PROJECT_DIR=${PROJECT_DIR}
conda env config vars set LD_LIBRARY_PATH=${CONDA_PREFIX}/lib:${LD_LIBRARY_PATH}
conda env config vars set CUDA_HOME=${CONDA_PREFIX}
conda env config vars set CUDA_ROOT=${CONDA_PREFIX}

conda deactivate
conda activate LF_transformer
```


## 2. Run
Now we have to evaluate the tuned configuration with 15 different random seeds.

```bash
python ./bin/LF_transformer.py --force ./output/{dataset_name}/lf_transformer/tuned_reproduced_ours/{seed}.toml

#If you want to run the covtype dataset for seed 0
python ./bin/LF_transformer.py --force ./output/covtype/lf_transformer/tuned_reproduced_ours/0.toml
```

Our directory with evaluation results is located right next to yours, namely, at `output/california_housing/mlp/tuned`.

## 3. Ensembling
```bash
# If you run the LF_Transformer on all seed numbers for specific data,, the results will save output directory. And just run this single command
python ./bin/ensemble.py LF_transformer output/{dataset_name}/lf_transformer/tuned_reproduced_ours

```
Your results will be located at `output/{dataset}/LF_transformer/tuned_reproduced_ours_ensemble`

## 4. Datasets
https://drive.google.com/drive/folders/1YMKxKz4IXtXSiwt7aW10o-IkUobIm6jG
# by referring to
Gorishniy, Yury, et al. "Revisiting deep learning models for tabular data." Advances in Neural Information Processing Systems 34 (2021): 18932-18943.
https://github.com/Yura52/tabular-dl-revisiting-models
