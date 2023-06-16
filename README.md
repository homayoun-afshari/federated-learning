# Initialization
## Root Folder
1. Create a folder named `mldl2023` in your Google drive.
2. Download the `datasets` folder from the repository and upload its content into `.../mldl2023/datasets`.
3. Download the `models` folder from the repository and upload its content into `.../mldl2023/models`.
4. Download the `utils` folder from the repository and upload its content into `.../mldl2023/utils`.
5. Download the `pretrained` folder from the repository and upload its content into `.../mldl2023/pretrained`.

## IDDA Dataset
1. Download and unzip it the IDDA dataset from https://mega.nz/file/yBwVGR6A#z2AyGYdsuHERRY67i6JKxhK9cbgVwhYWp4PyrrITbMQ.
2. Locate the `idda` folder and upload its content into `.../mldl2023/data/idda`.

## GTAV Dataset
1. Download and unzip the GTAV dataset from https://mega.nz/file/ERkiQBaY#h-wktK7U7MpIG5nf-rMWF7d76NEM5ae_MrAmELftNR0.
2. Locate the `GTA5` folder and upload its content into `.../mldl2023/data/GTA5`.

# Experiments
## Steps
Regarding the `instruction.pdf` file in the repository, a notebook is created for each step. For each notebook, please note that,
1. In the `Storage` section, the path to the `mldl2023` must be specified.
2. In the `Server Driver` section, you will find two important variables: `params` and `config`. The first variable sets the default parameters to run the experiment. The second one is a dictionary of the current configuration that is to be tested (if a certain parameter is not specified in the latter, the default from the former is used).

Please pay attention that before running the `step_3_4.ipynb` notebook, you are required to run the `style_extractor.ipynb` notebook to extract the styles from IDDA dataset according to the instructions. This operation creates a new folder in `.../mldl2023/data/idda/styles`. The content is a collection of styles of the clients. The amount of storage usage will be around 3GB.

## Storage
After running each notebook, a new folder is created in `.../mldl2023/storage/X` where `X` is a serialized representation of the `config` variable. For this purpose, each key in the `config` dictionary is compressed before serialization. The list of possible acronyms are provided in `acronyms.csv` in the repository. The content of `X` saves the checkpoint of each notebook to enable a restoration mechanism after disconnecting a notebook. This checkpoint is created after each successful epoch in the centralized experiments or after each communication round in the federated experiments. The content of `X` is as follows:
1. `log.txt` to log the storage mechanism. The storage usage is negligible.
2. `params.json` to store the default parameters used in the corresponding experiment. The storage usage is negligible.
3. `config.json` to store the configuration set for the corresponding experiment. The storage usage is negligible.
4. `scores.json` to store the scores of the clients. The storage usage is negligible. Note that this file will only be created by `step_5.ipynb` notebook.
5. `metrics.csv` to store the experiment results. The storage usage is negligible.
6. `model-main.pth` to store the model's state in each checkpoint. The storage usage is around 50MB. Note that this file will not be created by `step_4_2.ipynb` and `step_4_3.ipynb` notebooks.
7. `model-bestIdda.pth` to store the model's state when it has the best performance regarding the idda dataset when the model is trained on the GTAV dataset. The storage usage is around 50MB. Note that this file will only be created by `step_3_2.ipynb` and `step_3_4.ipynb` notebooks.
8. `model-bestSame.pth` to store the model's state when it has the best performance regarding the same-domain test dataset. The storage usage is around 50MB. Note that this file will not be created by `step_4_2.ipynb` and `step_4_3.ipynb` notebooks.
9. `model-bestDiff.pth` to store the model when it has the best performance regarding the different-domain test dataset. The storage usage is around 50MB. Note that this file will not be created by `step_4_2.ipynb` and `step_4_3.ipynb` notebooks.
10. `model-teacher.pth` to store the teacher model's state in each checkpoint. The storage usage is around 50MB. Note that this file will only be created by `step_4_2.ipynb` and `step_4_3.ipynb` notebooks.
11. `model-student.pth` to store the student model's state in each checkpoint. The storage usage is around 50MB. Note that this file will only be created by `step_4_2.ipynb` and `step_4_3.ipynb` notebooks.


Please pay attention that to continue an unfinished experiment, you are only required to use the same `config` dictionary. In case you want to reset an experiment, manually delete its corresponding folder from the `storage` folder. Note that changing the `param` variable in an existing experiment does not have any effects.

## Evaluation
For the purposes of confirmation and comparison, you can run the `evaluation.ipynb` notebook to evaluate all the best models stored for each step of the project. This notebook loads a pretrained model for each step and test it on the IDDA dataset. Please note that all the results are already contained in the notebook.

# More!
You can find more information about this project and our implementations in the paper.pdf file located in the repository.
