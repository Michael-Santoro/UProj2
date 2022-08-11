
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
<img width="341" alt="img_5" src="https://user-images.githubusercontent.com/74157573/181825339-4b3c322d-501a-4acf-9da3-7ba2217159f9.png">

6) This is a work truck with a compressor trailer, we can see the pipe equipment above the truck.
<img width="455" alt="img_6" src="https://user-images.githubusercontent.com/74157573/181825387-0508da33-b013-41d4-89c5-deb371b1f48e.png">

7) This car is a work truck which is apparent from the light-bar on the top of the truck the big tires and the big mirrors.
<img width="395" alt="img_7" src="https://user-images.githubusercontent.com/74157573/181825427-d80c805b-f355-4c9c-8cd7-8636d9e463cb.png">

8) We can see the back of this car but the rear window.
<img width="229" alt="img_8" src="https://user-images.githubusercontent.com/74157573/181825454-34b9be8e-b03c-440e-b38e-358eec1edfca.png">

9) We can see the front of this car by the windshield and the side mirrors.
<img width="270" alt="img_9" src="https://user-images.githubusercontent.com/74157573/181825473-fb462242-1d57-49bc-bcbf-694108cc3032.png">

10) The image below shows the back of a car and some people pretty far away.
<img width="245" alt="img_10" src="https://user-images.githubusercontent.com/74157573/181825489-5f8a7171-f257-43a6-ad1d-e3dc45c69ba0.png">

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
<img width="389" alt="image" src="https://user-images.githubusercontent.com/74157573/181827458-903d5f0c-742d-4d69-b026-ff5ab3eddcd5.png">

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

<img width="226" alt="image" src="https://user-images.githubusercontent.com/74157573/181828987-043267bb-f30b-4f28-874c-808ed0604d88.png">

<img width="455" alt="image" src="https://user-images.githubusercontent.com/74157573/181829046-6cf50d4c-5253-47f3-be89-44ed318c160e.png">

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
<img width="457" alt="image" src="https://user-images.githubusercontent.com/74157573/181835123-76178b71-93d5-4036-a07f-e6fcc00f6b87.png">


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
