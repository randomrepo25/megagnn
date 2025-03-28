# Mega-GNN

## Setup

- Create a new Conda environment, and activate.
```bash
conda env create -f env.yml
conda activate megagnn

```
- Install Pytorch and Pytorch Geometric
```bash
conda install pytorch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 pytorch-cuda=11.8 -c pytorch -c nvidia
conda install pyg -c pyg
pip install -r requirements.txt
```
- Lastly, install genagg
```bash
cd genagg 
pip install -e .
```


## Data

The data needed for the experiments can be found on [Kaggle](https://www.kaggle.com/datasets/ealtman2019 ibm-transactions-for-anti-money-laundering-aml/data). To use this data with the provided training scripts, you first need to perform a pre-processing step for the downloaded transaction files (e.g. `HI-Small_Trans.csv`):
  ```
  python format_kaggle_files.py /path/to/kaggle-files/HI-Small_Trans.csv
  ```
  - Make sure to change the filepaths in the `data_config.json` file. The `aml_data` path should be changed to wherever you stored the `formatted_transactions.csv` file generated by the pre-processing step.

The data for node classification experiments can be found on [ETH-Kaggle](https://drive.google.com/drive/folders/1u-NZ96U1SObxXEdWuClOufInbv_5vB1g?usp=sharing).



## Run the Code
To use different datasets, change the dataset name and the downstream task, and run the model with the additional parameters provided in utils.py.
- MEGA-GIN
```bash
python main.py --data Small_HI --model gin --emlps --reverse_mp --ego --flatten_edges --edge_agg_type gin --n_epochs 80 --save_model --task edge_class
```
- MEGA-PNA
```bash
python main.py --data Small_HI --model pna --emlps --reverse_mp --ego --flatten_edges --edge_agg_type pna --n_epochs 80 --save_model --task edge_class
```

### Acknowledgements

We used the codebase of [Multi-GNN](https://github.com/IBM/Multi-GNN) and [GenAgg](https://github.com/Acciorocketships/generalised-aggregation) and thank their authors for their excellent work.
