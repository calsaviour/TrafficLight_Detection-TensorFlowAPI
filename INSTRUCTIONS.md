### Prerequisite
1. Follow the steps ni README.md

### Download dataset and setup the directory
1. [Drive location](https://drive.google.com/file/d/0B-Eiyn-CUQtxdUZWMkFfQzdObUE/view?usp=sharing)   (This step is also in README.md)
2. Assume the tensor model project is in the home directory. unzip the  under ~/models/research/data
3. Move config folder (~/TrafficLight_Detection-TensorFlowAPI/config) to under ~/models/research/
4. Move the files label_map.pbtxt, real_data.record and sim_data.record in the directory (~/TrafficLight_Detection-TensorFlowAPI/)  to ~/models/research/



### Upgrade cudnn 6 (Perform this only if have error missig libcudnn.so.6)
1.https://developer.nvidia.com//compute/machine-learning/cudnn/secure/v6/prod/8.0_20170307/cudnn-8.0-linux-x64-v6.0-tgz
2.https://stackoverflow.com/questions/42013316/after-building-tensorflow-from-source-seeing-libcudart-so-and-libcudnn-errors/44147506#44147506

### Update tfexample.py (Perform this only if have error in step 1)
1. https://github.com/tensorflow/models/issues/2653
2. wget https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/slim/python/slim/data/tfexample_decoder.py


$ cd /usr/local/lib/python3.5/dist-packages/tensorflow/contrib/slim/python/slim/data
This might depend on the python setup. It will be different if your using Conda

$ sudo cp ./tfexample_decoder.py tfexample_decoder-backup.py
$ sudo rm ./tfexample_decoder.py
$ sudo cp /home/wpq/tfexample_decoder.py ./tfexample_decoder.py


## Run
protoc object_detection/protos/*.proto --python_out=.
export PYTHONPATH=$(which python):`pwd`:`pwd`/slim
1. python object_detection/train.py --pipeline_config_path=config/ssd_inception-traffic-udacity_sim.config --train_dir=data/sim_training_data/sim_data_capture