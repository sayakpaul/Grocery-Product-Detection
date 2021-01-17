# Grocery-Product-Detection
This repository builds a product detection model to recognize products from grocery shelf images. The dataset comes from [here](https://github.com/gulvarol/grocerydataset). Everything from data preparation to model training is done using [Colab Notebooks](https://colab.research.google.com/) so that no setup is required locally. All the relevant commentaries have been included inside the Colab Notebooks. 

## Repository organization

```
├── Colabs
│   ├── GroceryDataset_EDA_Prep.ipynb: EDA and data preparation notebook. 
│   ├── GroceryDataset_Inference.ipynb: Performs inference with the trained model.
│   └── GroceryDataset_Model_Training.ipynb: Trains an SSD MobileDet model using TFOD API.
├── Deliverables
│   ├── image2products.json: Contains test image names as keys and the number of products contained in each image as values.
│   └── metrics.json: mAP, precision and recall computed on test set.
├── Misc Files
│   ├── generate_tfrecord.py: Generates TFRecords from the provided dataset. 
│   └── ssdlite_mobiledet_dsp_320x320_products_sync_4x4.config: Configuration file needed by the TFOD API. 
└── README.md
```

## Results

Following snaps taken from TensorBoard after loading the evaluation logs (logs are available [here](https://drive.google.com/drive/folders/1sT5ztmXFRM69iYJvtcfMwGAzdgVtii29?usp=sharing)) - 

![](https://i.ibb.co/7ttLyBt/Screenshot-2021-01-16-at-8-42-58-PM.png)

![](https://i.ibb.co/GMLTnwQ/Screenshot-2021-01-16-at-8-43-26-PM.png)

As we can see with 10k training steps the metrics keep on shining. I believe with more sophisticated hyperparameter tuning and a longer training schedule performance can further be improved. 

![](https://i.ibb.co/xSxXSRF/Screenshot-2021-01-16-at-8-44-32-PM.png)

![](https://i.ibb.co/6gTxm6V/Screenshot-2021-01-16-at-8-46-51-PM.png)

## Notes
* The provided dataset is converted to TFRecords for easy compatibility with the TFOD API. Further notes are available inside the `Colabs/GroceryDataset_EDA_Prep.ipynb` notebook.
* Augmentation used
	* Horizontal flips
	* Random crops
* Detection network used: SSD MobileDet.
* Training hyperparameters are available inside `Misc\ Files/ssdlite_mobiledet_dsp_320x320_products_sync_4x4.config` file. 
* Recall reported in `Deliverables/metrics.json` is from **AR@100** (as can be see on the TensorBoard snaps above).

## Trained model files

Find them [here](https://drive.google.com/drive/folders/1sT5ztmXFRM69iYJvtcfMwGAzdgVtii29?usp=sharing). If you are looking for the checkpoints, the latest ones are prefixed with `model.ckpt-10000`. There's also a frozen inference graph. 

## Dataset citation
```
@article{varol16a,
      TITLE = {{Toward Retail Product Recognition on Grocery Shelves}},
      AUTHOR = {Varol, G{"u}l and Kuzu, Ridvan S.},
      JOURNAL = {ICIVC},
      YEAR = {2014}
}
```
