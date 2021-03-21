B1: 
python partition_dataset.py -x -i ../../workspace/trainning_demo/images -r 0.1

B2:
+ train.record
python generate_tfrecord.py -x ../../workspace/trainning_demo/images/train -l ../../workspace/trainning_demo/annotations/idcard_label_map.pbtxt -o ../../workspace/trainning_demo/annotations/train.record
+ test.record
python generate_tfrecord.py -x ../../workspace/trainning_demo/images/test -l ../../workspace/trainning_demo/annotations/idcard_label_map.pbtxt -o ../../workspace/trainning_demo/annotations/test.record

B3:
python model_main_tf2.py --model_dir=models/ssd_mobilenet_v2 --pipeline_config_path=models/ssd_mobilenet_v2/pipeline.config

B4: 
python exporter_main_v2.py --input_type image_tensor --pipeline_config_path models/ssd_mobilenet_v2/pipeline.config --trained_checkpoint_dir models/ssd_mobilenet_v2 --output_directory exported-models/my_model

TensorBoard:
B1: activate Tensorflow
B2: cd workspace/trainning_demo
B3: tensorboard --logdir=models\ssd_mobilenet_v2