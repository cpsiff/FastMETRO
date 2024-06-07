# Attempt 1 (FastMETRO) (exactly same as in instructions) - installation went ok

## Create a conda environment, activate the environment and install PyTorch via conda
conda create --name FastMETRO python=3.8
conda activate FastMETRO
conda install pytorch==1.8.0 torchvision==0.9.0 cudatoolkit=11.1 -c pytorch -c conda-forge

## Install FastMETRO
git clone --recursive https://github.com/postech-ami/FastMETRO.git
cd FastMETRO
python setup.py build develop

## Install requirements
pip install -r requirements.txt

## Install manopth
pip install ./manopth/.

## To run hand mesh reconstruction
python ./src/tools/end2end_inference_handmesh.py --resume_checkpoint ./models/fastmetro_checkpoint/FastMETRO-L-H64_freihand_state_dict.bin --image_file_or_path ./demo/hand

I commented out line 33 in end2end_inference_handmesh.py b/c we don't want to use opendr anyway:
```
# from src.utils.renderer_opendr import OpenDR_Renderer, visualize_reconstruction_opendr
```

Now I get the error "cannot import name "bool" from "numpy"". Coming from import chumpy. Same shit as HandOccNet

Ran `pip install git+https://github.com/mattloper/chumpy` at recommendation of https://github.com/mattloper/chumpy/issues/55. Error gone

now running demo code seems to work:
```bash
python ./src/tools/end2end_inference_handmesh.py --resume_checkpoint ./models/fastmetro_checkpoint/FastMETRO-L-H64_freihand_state_dict.bin --image_file_or_path ./demo/hand
```

how to run my_demo code:
```bash
python ./src/tools/my_demo.py --resume_checkpoint ./models/fastmetro_checkpoint/FastMETRO-L-H64_freihand_state_dict.bin --output_dir output/my_demo
```