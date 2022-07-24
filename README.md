
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
![range_image_screenshot_24 07 2022](https://user-images.githubusercontent.com/74157573/180663252-96853d9f-7e9b-4cfb-8afe-e82d85ab5016.png)

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

1) The following is an example of a pick-up truck and a trailer next to the car with the Lidar sensor on top.
<img width="426" alt="image" src="https://user-images.githubusercontent.com/74157573/180663681-40a3651f-91b2-4d84-8ee2-fe309280355e.png">

2) The following are a couple of cars adjacent to the lidar sensor.
<img width="437" alt="image" src="https://user-images.githubusercontent.com/74157573/180663799-5de19d50-ba9c-45f6-a3f1-3162f413428b.png">

3) Here are a couple more veichles a little further away.
<img width="578" alt="image" src="https://user-images.githubusercontent.com/74157573/180663851-8e4e6488-d0cd-4948-883a-b18d677ad25c.png">

4) In this image you can actually see the mirrors of the cars so that direction of travel can be understood.
<img width="619" alt="image" src="https://user-images.githubusercontent.com/74157573/180663896-05ed875b-331c-4053-a6b7-1b0e34e7e408.png">

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








