# DiAMoNDBack: Diffusion-denoising Autoregressive Model for Non-Deterministic Backmapping of C$\alpha$ Protein Traces

Paper: LINK TO PAPER

A transferable approach for backmapping generic C$\alpha$ protein traces using Denoising Diffusion Probabilistic Models (DDPMs).

The DDPM models contained herein are adapted from the implementation by https://github.com/lucidrains/denoising-diffusion-pytorch, borrowing also from some changes to this implementation by https://github.com/tiwarylab/DDPM_REMD. 


## Environmnet

The environment file provided at `env.yml` can be used to create the `DiffBack` environment with:

```bash
$ conda env create -f env.yml
```

The environment can then be activated with:

```bash
$ conda activate diffback
```

## Performing backmapping

To backmap your own C$\alpha$ traces, or atomistic PDBs extracting only the C$\alpha$ positions, using our pre-trained model:

```bash
$ cd scripts
$ python ...

```

## Training

We provide the functionality to train DDPM backmapping models both from scratch and fine-tune pre-trained models. We recommend fine-tuning models starting from the pre-trained model provided in `pre_trained_models/PDB_trained`. This pre-trained model was trained on 65k+ PDB structures and serves as a good starting point for building bespoke backmapping models on possibly small amounts of available atomistic data. 


### Fine-tuning

To fine-tune begin with compiling a directory containing atomistic PDB structures that will be used for fine-tuning, for example in `data/train_pdbs`. Then, with the environment activated, navigate to the scripts directory and execute the training script specifying the pre-trained model path for fine-tuning;

```bash
$ cd scripts
$ python train.py --pdb_dir ../data/train_pdbs/ --save_name test_run --finetune ../pre_trained_models/PDB_trained/model.pt
```

The model will begin training and periodically output checkpoints to a `./results/train_{save_name}` directory. The argument provided to `--pdb_dir` should be a directory containing PDB files that will by default be processed for featurization and saved to `data/processed_features`. As featurization can become costly for large quantities of structures, this preprocessing step can be skipped by providing the `--run_preprocess 0` flag in which case the existing feature files with the associated `save_name` contained in `data/processed_features` will be used. 

### Training from scratch 

With a directory containing PDB structures that will be used for training, for example in `data/train_pdbs`, the same training script as for fine-tuning can be run simply without the `--finetune` argument:

```bash
$ cd scripts
$ python train.py --pdb_dir ../data/train_pdbs/ --save_name test_run 
```

Model checkpoints will start saving to a `./results/train_{save_name}` directory, with the same options for handling feature preprocessing available for training from scratch as discussed in the fine-tuning routines. 

## Data splits

Training and evaluation splits in pdb format for all data used to train and test the models presented in the paper are available for download at: LINK TO DATA SPLITS

## Citation

```bibtex
@article{
}
```
