## DeepFM_Avazu_x4_001

A notebook to benchmark DeepFM on Avazu_x4_001 dataset.

Author: [XUEPAI Team](https://github.com/xue-pai)


### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  RAM: 500G+
  ```
+ Software

  ```python
  python: 3.6.5
  pandas: 1.0.0
  numpy: 1.18.1
  ```

### Dataset
In this setting, we preprocess the data split by removing the id field that is useless for CTR prediction. In addition, we transform the timestamp field into three fields: hour, weekday, and is_weekend. For all categorical fields, we filter infrequent features by setting the threshold min_category_count=2 (performs well) and replace them with a default <OOV> token. Note that we do not follow the exact preprocessing steps in AutoInt, because the authors neither remove the useless id field nor specially preprocess the timestamp field.

To make a fair comparison, we fix embedding_dim=16 as with AutoInt.


### Code
1. Install FuxiCTR
  
    Install FuxiCTR via `pip install fuxictr==1.0` to get all dependencies ready. Then download [the FuxiCTR repository](https://github.com/huawei-noah/benchmark/archive/53e314461c19dbc7f462b42bf0f0bfae020dc398.zip) to your local path.

2. Downalod the dataset and run [the preprocessing script](https://github.com/xue-pai/Open-CTR-Benchmark/blob/master/datasets/Avazu/Avazu_x4/split_avazu_x4.py) for data splitting. 

3. Download the hyper-parameter configuration file: [DeepFM_avazu_x4_tuner_config_01.yaml](./DeepFM_avazu_x4_tuner_config_01.yaml)

4. Run the following script to reproduce the result. 
  + --config: The config file that defines the tuning space
  + --tag: Specify which expid to run (each expid corresponds to a specific setting of hyper-parameters in the tunner space)
  + --gpu: The available gpus for parameters tuning.

  ```bash
  cd FuxiCTR/benchmarks
  python run_param_tuner.py --config YOUR_PATH/DeepFM_avazu_x4_tuner_config_01.yaml --tag 019 --gpu 0
  ```

### Results
```python
[Metrics] logloss: 0.371901 - AUC: 0.792990
```


### Logs
```python
2020-06-12 16:12:51,065 P7047 INFO {
    "batch_norm": "False",
    "batch_size": "10000",
    "data_format": "h5",
    "data_root": "../data/Avazu/",
    "dataset_id": "avazu_x4_3bbbc4c9",
    "debug": "False",
    "embedding_dim": "16",
    "embedding_dropout": "0",
    "embedding_regularizer": "0",
    "epochs": "100",
    "every_x_epochs": "1",
    "gpu": "0",
    "hidden_activations": "relu",
    "hidden_units": "[2000, 2000, 2000, 2000]",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['logloss', 'AUC']",
    "model": "DeepFM",
    "model_id": "DeepFM_avazu_x4_3bbbc4c9_019_72fc2cd3",
    "model_root": "./Avazu/DeepFM_avazu/min2/",
    "monitor": "{'AUC': 1, 'logloss': -1}",
    "monitor_mode": "max",
    "net_dropout": "0",
    "net_regularizer": "0",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2019",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Avazu/avazu_x4_3bbbc4c9/test.h5",
    "train_data": "../data/Avazu/avazu_x4_3bbbc4c9/train.h5",
    "use_hdf5": "True",
    "valid_data": "../data/Avazu/avazu_x4_3bbbc4c9/valid.h5",
    "verbose": "1",
    "version": "pytorch",
    "workers": "3"
}
2020-06-12 16:12:51,065 P7047 INFO Set up feature encoder...
2020-06-12 16:12:51,066 P7047 INFO Load feature_map from json: ../data/Avazu/avazu_x4_3bbbc4c9/feature_map.json
2020-06-12 16:12:52,773 P7047 INFO Total number of parameters: 76544576.
2020-06-12 16:12:52,773 P7047 INFO Loading data...
2020-06-12 16:12:52,775 P7047 INFO Loading data from h5: ../data/Avazu/avazu_x4_3bbbc4c9/train.h5
2020-06-12 16:12:55,644 P7047 INFO Loading data from h5: ../data/Avazu/avazu_x4_3bbbc4c9/valid.h5
2020-06-12 16:12:56,884 P7047 INFO Train samples: total/32343172, pos/5492052, neg/26851120, ratio/16.98%
2020-06-12 16:12:56,993 P7047 INFO Validation samples: total/4042897, pos/686507, neg/3356390, ratio/16.98%
2020-06-12 16:12:56,993 P7047 INFO Loading train data done.
2020-06-12 16:12:59,774 P7047 INFO Start training: 3235 batches/epoch
2020-06-12 16:12:59,774 P7047 INFO ************ Epoch=1 start ************
2020-06-12 16:27:51,766 P7047 INFO [Metrics] logloss: 0.372035 - AUC: 0.792794
2020-06-12 16:27:51,767 P7047 INFO Save best model: monitor(max): 0.420759
2020-06-12 16:27:52,043 P7047 INFO --- 3235/3235 batches finished ---
2020-06-12 16:27:52,088 P7047 INFO Train loss: 0.380125
2020-06-12 16:27:52,089 P7047 INFO ************ Epoch=1 end ************
2020-06-12 16:42:42,369 P7047 INFO [Metrics] logloss: 0.380053 - AUC: 0.789567
2020-06-12 16:42:42,373 P7047 INFO Monitor(max) STOP: 0.409514 !
2020-06-12 16:42:42,373 P7047 INFO Reduce learning rate on plateau: 0.000100
2020-06-12 16:42:42,373 P7047 INFO --- 3235/3235 batches finished ---
2020-06-12 16:42:42,423 P7047 INFO Train loss: 0.332604
2020-06-12 16:42:42,423 P7047 INFO ************ Epoch=2 end ************
2020-06-12 16:57:32,253 P7047 INFO [Metrics] logloss: 0.426078 - AUC: 0.776283
2020-06-12 16:57:32,256 P7047 INFO Monitor(max) STOP: 0.350205 !
2020-06-12 16:57:32,256 P7047 INFO Reduce learning rate on plateau: 0.000010
2020-06-12 16:57:32,256 P7047 INFO Early stopping at epoch=3
2020-06-12 16:57:32,256 P7047 INFO --- 3235/3235 batches finished ---
2020-06-12 16:57:32,303 P7047 INFO Train loss: 0.290542
2020-06-12 16:57:32,303 P7047 INFO Training finished.
2020-06-12 16:57:32,303 P7047 INFO Load best model: /home/xxx/xxx/OpenCTR1030/benchmarks/Avazu/DeepFM_avazu/min2/avazu_x4_3bbbc4c9/DeepFM_avazu_x4_3bbbc4c9_019_72fc2cd3_model.ckpt
2020-06-12 16:57:32,684 P7047 INFO ****** Train/validation evaluation ******
2020-06-12 16:57:55,907 P7047 INFO [Metrics] logloss: 0.372035 - AUC: 0.792794
2020-06-12 16:57:55,955 P7047 INFO ******** Test evaluation ********
2020-06-12 16:57:55,955 P7047 INFO Loading data...
2020-06-12 16:57:55,955 P7047 INFO Loading data from h5: ../data/Avazu/avazu_x4_3bbbc4c9/test.h5
2020-06-12 16:57:56,471 P7047 INFO Test samples: total/4042898, pos/686507, neg/3356391, ratio/16.98%
2020-06-12 16:57:56,471 P7047 INFO Loading test data done.
2020-06-12 16:58:19,930 P7047 INFO [Metrics] logloss: 0.371901 - AUC: 0.792990



```