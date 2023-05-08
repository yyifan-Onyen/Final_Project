# Final_Project of deep learning
## TieZheng Zhang & Yifan Zhou
---------------------------------------------------------------------------------------
### Prerequsite
This code is developed with Python3 (`python3`). PyTorch 1.9+ is required. 
Using the below code to create the environment required for our project.
```bash
conda env create --file requirements.yaml python=3
conda activate barf-env
```
---------------------------------------------------------------------------------------
### Dataset
we using the dataset can be found in the link (https://drive.google.com/drive/folders/128yBriW1IG_3NJ5Rp7APSTZsJqdJdfc1)

DAE.ipynb is used to generate the noise and denoise

---------------------------------------------------------------------------------------
### Running the code
- #### BARF models
  To train and evaluate BARF:
  ```bash
  # <GROUP> and <NAME> can be set to your likes, while <SCENE> is specific to datasets
  
  # Blender (<SCENE>={chair,drums,ficus,hotdog,lego,materials,mic,ship})
  python3 train.py --group=<GROUP> --model=barf --yaml=barf_blender --name=<NAME> --data.scene=<SCENE> --barf_c2f=[0.1,0.5]
  python3 evaluate.py --group=<GROUP> --model=barf --yaml=barf_blender --name=<NAME> --data.scene=<SCENE> --data.val_sub= --resume
  
  # LLFF (<SCENE>={fern,flower,fortress,horns,leaves,orchids,room,trex})
  python3 train.py --group=<GROUP> --model=barf --yaml=barf_llff --name=<NAME> --data.scene=<SCENE> --barf_c2f=[0.1,0.5]
  python3 evaluate.py --group=<GROUP> --model=barf --yaml=barf_llff --name=<NAME> --data.scene=<SCENE> --resume
  ```
  All the results will be stored in the directory `output/<GROUP>/<NAME>`.
  You may want to organize your experiments by grouping different runs in the same group.
  
  If you want to evaluate a checkpoint at a specific iteration number, use `--resume=<ITER_NUMBER>` instead of just `--resume`.

- #### Training the original NeRF
  If you want to train the reference NeRF models (assuming known camera poses):
  ```bash
  # Blender
  python3 train.py --group=<GROUP> --model=nerf --yaml=nerf_blender --name=<NAME> --data.scene=<SCENE>
  python3 evaluate.py --group=<GROUP> --model=nerf --yaml=nerf_blender --name=<NAME> --data.scene=<SCENE> --data.val_sub= --resume
  
  # LLFF
  python3 train.py --group=<GROUP> --model=nerf --yaml=nerf_llff --name=<NAME> --data.scene=<SCENE>
  python3 evaluate.py --group=<GROUP> --model=nerf --yaml=nerf_llff --name=<NAME> --data.scene=<SCENE> --resume
  ```
  A video `vis.mp4` will also be created to visualize the optimization process.

---------------------------------------------------------------------------------------






