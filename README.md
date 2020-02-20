No models are currently in this project go to https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md 
to download models.

## For ssd_mobilenet_v1_coco 
*after adding .xml and creating a cvs out of it*

code to create tfrecords
```
python generate_tfrecord.py --csv_input=data/train_labels.csv --output_path=data/train.record --image_dir=images/

python generate_tfrecord.py --csv_input=data/test_labels.csv --output_path=data/test.record --image_dir=images/
```

in config file make sure 
fine_tune_checkpoint is path to model.ckpt on local machine
input_path for training and test is correct for local machine 
labal_map_path is correct for local machine for both training and test 

To train model
```
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/ssd_mobilenet_v1_pets.config
```

to export model

```
python export_inference_graph.py \
    --input_type image_tensor \
    --pipeline_config_path training/ssd_mobilenet_v1.config \
    --trained_checkpoint_prefix training/model.ckpt-10XXX \ 
    --output_directory sodacan_inference_graph
```

Run object_live_test.py to test model in webcam 
