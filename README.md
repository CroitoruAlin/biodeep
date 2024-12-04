# Deepfake Media Generation and Detection in the Generative AI Era: A Survey and Outlook

BioDeep dataset link: https://huggingface.co/datasets/University-of-Bucharest-BioDeep/BioDeepAV

Link to our survey: https://arxiv.org/abs/2411.19537


## Experiments on BioDeepAV:

### Clone the project: 
```commandline
git lfs install
git clone --recurse-submodules https://github.com/CroitoruAlin/biodeep.git
```

1. Create conda environment:
```commandline
cd DeepfakeBench
conda create -n DeepfakeBench python=3.7.2
conda activate DeepfakeBench
sh install.sh
cd ..
```
2. Prepare the dataset
```commandline
cp -r BioDeepAV DeepfakeBench/datasets
cd DeepfakeBench
conda activate DeepfakeBench
cp ../resources/preprocess/config.yaml preprocessing/config.yaml
cp ../resources/preprocess/preprocess.py preprocessing/preprocess.py
cp ../resources/preprocess/rearrange.py preprocessing/rearrange.py
```
Download the [shape_predictor_81_face_landmarks.dat](https://github.com/SCLBD/DeepfakeBench/releases/download/v1.0.0/shape_predictor_81_face_landmarks.dat) file. Then, copy the downloaded shape_predictor_81_face_landmarks.dat file into the `./preprocessing/dlib_tools` folder. This file is necessary for Dlib's face detection functionality.
```commandline
cd preprocessing
python preprocess.py
cd ..
python preprocessing/rearrange.py
```
3. Download  from [here](https://github.com/SCLBD/DeepfakeBench/releases/tag/v1.0.1) the pretrained checkpoint that you want to use and copy our config files in the DeepfakeBench benchmark codebase:
```commandline
cp ../resources/training/test.py training/test.py
cp ../resources/training/config/test_config.yaml training/config/test_config.yaml
cp ../resources/training/config/detector/<model>.yaml training/config/detector/<model>.yaml # cp ../resources/training/config/detector/ucf.yaml training/config/detector/ucf.yaml 
```
Run the inference code with the previous downloaded checkpoint:
```commandline
python3 training/test.py --detector_path ./training/config/detector/<model>.yaml --test_dataset "BioDeepAV" --weights_path ./training/pretrained/<model>_best.pth
```
For example, if you want to use UCF you can run the following:
```commandline
python3 training/test.py --detector_path ./training/config/detector/ucf.yaml --test_dataset "BioDeepAV" --weights_path ./training/pretrained/ucf_best.pth
```

## Acknowledgements

We use the DeepfakeBench benchmark code for evaluation:

https://github.com/SCLBD/DeepfakeBench/

As real examples in our experiments we used samples from TalkingHead-1KH and HDTF:

https://github.com/tcwang0509/TalkingHead-1KH

https://github.com/universome/HDTF/tree/main
