# IASFilter

This is the code for IASFilter, an adaptive label-noise filtering framework for molecular regression tasks.
IASFilter requires the following Python libraries:

```text
numpy
pandas
scikit-learn
scikit-optimize
rdkit
```

Recommended installation:

```bash
conda install -c conda-forge numpy pandas scikit-learn scikit-optimize rdkit
```

Or install the common Python packages with `pip` and RDKit with `conda`:

```bash
conda install -c conda-forge rdkit
pip install numpy pandas scikit-learn scikit-optimize
```

Next, we demonstrate an application example of IASFilter: A molecular dataset is filtered using IASFilter, and the filtered data are subsequently used to train the four downstream models considered in this study. The model performances before and after filtering are compared to evaluate the effectiveness of IASFilter.

The example dataset is provided in:

```text
datasets/example_train.csv
```
The input file should contain molecular SMILES and corresponding property labels. The first two columns will be used by the notebook and renamed as:
```text
SMILES,Label
```

If you want to use your own dataset, replace `datasets/example_train.csv` by your path

Also, you can also modify the codes to be suitable for your specific data file type

The full IASFilter workflow is provided in:

```text
IASFilter.ipynb
```

This is a user-friendly format. Just open the notebook and run all cells directly.

## Output

The filtering results are saved in:

```text
datasets/example_results/
```

The generated files include clean datasets and noisy datasets:

```text
clean_{count}.csv
noise_{count}.csv
```

`clean_*.csv` contains molecules retained as clean samples.

`noise_*.csv` contains molecules identified as potentially noisy samples.

The variable `count` is used as a filtering intensity. Bigger count indicates a conservative filtering.

## Model Scripts

Model scripts are provided in:

```text
model_script
```

This folder contains notebooks for downstream molecular property prediction models used in our main text:

```text
model_script/GCN.ipynb
model_script/KRR.ipynb
model_script/MLP.ipynb
model_script/XGBoost.ipynb
```

These scripts can be used to train and evaluate prediction models on the original or filtered datasets.

## Notes

The notebook uses `n_jobs=60` in several model training and Bayesian search steps. Please adjust this value according to the number of CPU cores available on your machine.

Invalid SMILES strings may cause RDKit parsing errors. It is recommended to check and standardize molecular SMILES before running IASFilter.

## Data and reproduce

All datasets used in this study for method construction are freely available from the following sources:

- ESOL, FreeSolv, Lipophilicity, Bace, Ro, FreeSolv_cal and QM8: https://doi.org/10.1039/c7sc02664a
- Ro and Td: https://doi.org/10.1016/j.cej.2025.160218
- fm_reg and skin_permeability: https://biosig.lab.uq.edu.au/deeppk/data
- AS: https://doi.org/10.1038/s41467-020-19594-z
- OS: https://doi.org/10.1038/s41597-022-01142-7

All datasets used in our work are listed above, which are publicly and freely available. We gratefully acknowledge these studies for providing the datasets in this work. 
Also, we also provide source data for our results: https://github.com/Royysr/IASFilter-source_data
To split datasets and inject noise, please use the script:
```text
analysis_script/inject_noise.ipynb
```

To obtain the prediction residual and uncertainty, please use the script:
```text
analysis_script/noise_response.ipynb
```

To evaluate data diversity, please use the script:
```text
analysis_script/diversity_evaluation.ipynb
```
