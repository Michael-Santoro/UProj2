
# SDCND : Sensor Fusion and Tracking - Mid-Term Project
**Michael Santoro**</br>
This is the project for the second course in the  [Udacity Self-Driving Car Engineer Nanodegree Program](https://www.udacity.com/course/c-plus-plus-nanodegree--nd213) : Sensor Fusion and Tracking. 

## Visualize range image channels (ID_S1_EX1) ##
The following image is obtained by modifying the following in the loop_over_dataset.py file:
```python
data_filename = 'training_segment-1005081002024129653_5313_150_5333_150_with_camera_labels.tfrecord
show_only_frames = [0, 1]
exec_data = []
exec_detection = []
exec_tracking = []
exec_visualization = ['show_range_image']
```
<img width="1278" alt="image" src="https://user-images.githubusercontent.com/74157573/181143869-a49fd1df-a5fc-48ea-9937-9e1a0d59a251.png">

## Visualize point-cloud (ID_S1_EX2) ##
The following image is obtained by modifying the following in the loop_over_dataset.py file:
```python
data_filename = '10963653239323173269_1924_000_1944_000_with_camera_labels.tfrecord'
show_only_frames = [0, 200]
exec_data = []
exec_detection = []
exec_tracking = []
exec_visualization = ['show_pcl']
```
### Find 10 examples of vehicles with varying degrees of visibility in the point-cloud
Try to identify vehicle features that appear stable in most of the inspected examples and describe them

1) The following is an example of a pick-up truck, trailer, and a person. There even appears to be a lightbar on top of the truck with box type bed.
<img width="497" alt="image" src="https://user-images.githubusercontent.com/74157573/181386372-6c973e71-1442-4ed9-8976-9d40526e7dfc.png">

2) The following is an example of a front of a car traveling in the opposite direction.
<img width="320" alt="image" src="https://user-images.githubusercontent.com/74157573/181387390-b82b219b-6eba-498f-9a63-9546b9f98b19.png">

3) Here are a couple more veichles a little further away all of which are facing toward the car with the lidar detector. We can see this from the windshield feature.
<img width="347" alt="image" src="https://user-images.githubusercontent.com/74157573/181388163-b1ad829e-c0c4-48a6-92d1-9361c3064a2a.png">

4) In this image you can actually see the mirrors of the cars so that direction of travel can be understood.
<img width="428" alt="image" src="https://user-images.githubusercontent.com/74157573/181392966-d7a15eaa-bac5-497a-90a0-ded25b529da7.png">

5) In this image we can clearly see a car going the opposite direction.
<img width="267" alt="image" src="https://user-images.githubusercontent.com/74157573/180663933-4e9489e7-12fc-440d-8656-6f6d9d081eb2.png">

6) By rotating the image in the view we can clearly see a car and a truck in this image.
<img width="314" alt="image" src="https://user-images.githubusercontent.com/74157573/180664039-100a177e-6067-4703-99bb-0ac615e00146.png">

7) Again we can see the back of some cars by rotating the point-cloud image.
<img width="131" alt="image" src="https://user-images.githubusercontent.com/74157573/180664119-5408c16b-d7ec-4813-88f9-bdb19a1427b7.png">

8) We can clearly see the windsheild and the mirrors and the lights of this car.
<img width="304" alt="image" src="https://user-images.githubusercontent.com/74157573/180664161-05aa4be9-e77c-4572-8f04-888b36874438.png">

9) We can see the backs of these cars.
<img width="321" alt="image" src="https://user-images.githubusercontent.com/74157573/180664221-1279bc49-a51e-4d02-9c8e-f4b9b6363ef4.png">

10) Another example of the back of some cars.
<img width="260" alt="image" src="https://user-images.githubusercontent.com/74157573/180664307-ec149287-ac49-45e7-80c5-ce3fee035498.png">

## Convert sensor coordinates to BEV-map coordinates (ID_S2_EX1)
The following image is obtained by modifying the following in the loop_over_dataset.py file:
```python
data_filename = '1005081002024129653_5313_150_5333_150_with_camera_labels.tfrecord'
show_only_frames = [0, 1]
exec_data = ['pcl_from_rangeimage']
exec_detection = ['bev_from_pcl']
exec_tracking = []
exec_visualization = []
```
<img width="355" alt="image" src="https://user-images.githubusercontent.com/74157573/180664498-650be03e-0256-4d14-a298-5311650c4d08.png">

## Compute intensity layer of the BEV map (ID_S2_EX2)
The following image is obtained by modifying the following in the loop_over_dataset.py file:
```python
data_filename = '1005081002024129653_5313_150_5333_150_with_camera_labels.tfrecord'
show_only_frames = [0, 1]
exec_data = ['pcl_from_rangeimage']
exec_detection = ['bev_from_pcl']
exec_tracking = []
exec_visualization = []
```

<img width="302" alt="image" src="https://user-images.githubusercontent.com/74157573/180664739-a6b29934-cd4b-40c9-9a23-2c7c990b17e6.png">

## Compute height layer of the BEV map (ID_S2_EX3)
The output of the implementation of this step was no different from the previous 2.

## Add a second model from a GitHub repo (ID_S3_EX1)
There were no visual artificats produced with this exc but the settings were as follows.
```python
data_filename = '1005081002024129653_5313_150_5333_150_with_camera_labels.tfrecord'
show_only_frames = [50, 51]
exec_data = ['pcl_from_rangeimage', 'load_image']
exec_detection = ['bev_from_pcl', 'detect_objects']
exec_tracking = []
exec_visualization = ['show_objects_in_bev_labels_in_camera']
configs_det = det.load_configs(model_name="fpn_resnet")
```

## Extract 3D bounding boxes from model response (ID_S3_EX2)
```python
data_filename = 'training_segment-1005081002024129653_5313_150_5333_150_with_camera_labels.tfrecord
show_only_frames = [50, 51]
exec_data = ['pcl_from_rangeimage', 'load_image']
exec_detection = ['bev_from_pcl', 'detect_objects']
exec_tracking = []
exec_visualization = ['show_objects_in_bev_labels_in_camera']
configs_det = det.load_configs(model_name="fpn_resnet")
```
## Compute intersection-over-union between labels and detections (ID_S4_EX1)
```python
data_filename = 'training_segment-1005081002024129653_5313_150_5333_150_with_camera_labels.tfrecord
show_only_frames = [50, 51]
exec_data = ['pcl_from_rangeimage']
exec_detection = ['bev_from_pcl', 'detect_objects', 'validate_object_labels', 'measure_detection_performance']
exec_tracking = []
exec_visualization = ['show_detection_performance']
configs_det = det.load_configs(model_name="darknet")
```

## Compute false-negatives and false-positives (ID_S4_EX2)
