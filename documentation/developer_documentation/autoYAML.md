# YAML file 

## Input explanations

| Input | YAML entry | Description |
| --- | --- | -- |
| Run Analysis *(optional)* | run_analysis | An input of "t" means you want to run WEAT analysis. |
| Run Cleaning *(optional)* | run_cleaning | An input of "t" means you want to run WEAT cleaning. |
| Model Directory ***(required for analysis)*** | model_directory | Filepath to the directory containing word embedding models |
| Output Directory ***(required for analysis)*** | output_directory | Filepath to where the TEMP folder (which generated test models and a vocabulary file) should be created and saved. |
| Output File ***(required for analysis)*** | output_file | Filepath to where the WEAT results should be saved. The results will be saved as a JSON file. |
| Test Directory ***(required for analysis)*** | test_directory | Filepath to directory containing json files that specify the groups/domain vocabulary to be tested|
| Embeddings Suffix *(optional)* | embeddings_suffix | The suffix of the files containing word embedding vectors, in order to differentiate these files from the vocabulary files. Default is "npy". |
| Vocabulary Suffix *(optional)* | vocabulary_suffix | The suffix of the files containing the vocabulary that correspond to the word embedding vectors. Default is "txt". |
| Reusing models generated by the Fetchvec module *(optional)* | reuse_fetchvec | If you enter "t" in this field, the pre-processing stage will be skipped, so that the models generated from pre-processing previously are reused. Only turn this on if you are running on the same set of tests. Turning it on may speed up the WEAT computations. |
|  Cleaning CSV file ***(required for cleaning)*** | clean_csv | Filepath to where the input cleaning CSV is located (e.g. clean.csv) |
| Cleaning output file ***(required for cleaning)*** | clean_out | Filepath to where the WEAT cleaning should be saved. The results will be saved as a CSV file.