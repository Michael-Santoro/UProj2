# Final Writeup: Sensor Fusion and Object Tracking
**Michael Santoro**

## Tracking
The first step to this final project is to implement EKF (Extended Kalman Filter).
There are two pieces of information that are essential to the functions that were coded in the filters.py file. The first being the 3D state transition equation, shown below:

$$\begin{pmatrix} 
P_x \\ 
P_y \\ 
P_z \\ 
v_x \\ 
v_y \\ 
v_z \end{pmatrix}=
\begin{pmatrix} 
1 & 0 & 0 & \Delta t & 0 & 0 \\
0 & 1 & 0 & 0 & \Delta t & 0 \\ 
0 & 0 & 1 & 0 & 0 & \Delta t \\
0 & 0 & 0 & 1 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 1 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 \end{pmatrix}*
\begin{pmatrix} 
P_x \\ 
P_y \\ 
P_z \\ 
v_x \\ 
v_y \\ 
v_z \end{pmatrix} + 
\begin{pmatrix} 
v_{px} \\ 
v_{py} \\ 
v_{pz} \\ 
v_{vx} \\ 
v_{vy} \\ 
v_{vz} \end{pmatrix}
$$


$$
\textbf{F}(\Delta t) = \begin{pmatrix} 
1 & 0 & 0 & \Delta t & 0 & 0 \\
0 & 1 & 0 & 0 & \Delta t & 0 \\ 
0 & 0 & 1 & 0 & 0 & \Delta t \\
0 & 0 & 0 & 1 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 1 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 \end{pmatrix}
$$

The second being the covariance matrix below.
Discrtizing this continous model leads to a formula for $\textbf{Q}$ depending on $\Delta t$ as follows:

$$
\textbf{Q}(\Delta t) = \int_{0}^{\Delta t}\textbf{F}(t)\textbf{Q}\textbf{F}(t)^T
$$

$$
 \int_{0}^{\Delta t}\begin{pmatrix} 
1 & 0 & 0 & t & 0 & 0 \\
0 & 1 & 0 & 0 & t & 0 \\ 
0 & 0 & 1 & 0 & 0 &  t \\
0 & 0 & 0 & 1 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 1 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 1 \end{pmatrix}*
\begin{pmatrix} 
0 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & q & 0 & 0 \\ 
0 & 0 & 0 & 0 & q & 0 \\ 
0 & 0 & 0 & 0 & 0 & q \end{pmatrix}*
\begin{pmatrix} 
1 & 0 & 0 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 0 & 1 & 0 & 0 & 0 \\
t & 0 & 0 & 1 & 0 & 0 \\ 
0 & t & 0 & 0 & 1 & 0 \\ 
0 & 0 & t & 0 & 0 & 1 \end{pmatrix}dt
$$

$$
 \int_{0}^{\Delta t}\begin{pmatrix} 
q t^2 & 0 & 0 & qt & 0 & 0 \\
0 &  q t^2 & 0 & 0 & qt & 0 \\ 
0 & 0 & q t^2 & 0 & 0 &  qt \\
qt & 0 & 0 & q & 0 & 0 \\ 
0 & qt & 0 & 0 & q & 0 \\ 
0 & 0 & qt & 0 & 0 & q \end{pmatrix}dt
$$

$$
\textbf{Q} = \begin{pmatrix} 
\frac{(\Delta t)^3 q}{3} & 0 & 0 & \frac{(\Delta t)^2 q}{2} & 0 & 0 \\
0 &  \frac{(\Delta t)^3 q}{3} & 0 & 0 & \frac{(\Delta t)^2 q}{2} & 0 \\ 
0 & 0 & \frac{(\Delta t)^3 q}{3} & 0 & 0 &  \frac{(\Delta t)^2 q}{2} \\
\frac{(\Delta t)^2 q}{2} & 0 & 0 & \Delta tq & 0 & 0 \\ 
0 & \frac{(\Delta t)^2 q}{2} & 0 & 0 & \Delta tq & 0 \\ 
0 & 0 & \frac{(\Delta t)^2 q}{2} & 0 & 0 & \Delta tq \end{pmatrix}
$$

After these matricies had been defined, the linear algebra equations for the predict and update functions were used to complete the position (x) and prediction (P) from the track.

<img width="928" alt="image" src="https://user-images.githubusercontent.com/74157573/184032845-d3705cfe-0c21-4347-91b2-49a25f741462.png">

<img width="902" alt="image" src="https://user-images.githubusercontent.com/74157573/184033038-6fd7d144-6ec3-48cc-84d2-525e9ab43b7a.png">

## Track Management

This step was primarily to complete the track management class and the track class. There is code related to updating track scores and deleting unassociated tracks based on conditions.

<img width="901" alt="image" src="https://user-images.githubusercontent.com/74157573/184042500-9bd4b76e-0421-438c-b590-6f3a8efdf797.png">

## Data Association
This step is the big connecting part of the project where tracks are managed in the association matrix. This was a challenge for me since I forgot to update the get_closest association function.

<img width="906" alt="image" src="https://user-images.githubusercontent.com/74157573/184042975-a40176fc-b75a-49b7-9798-1d261db7a514.png">


<img width="907" alt="image" src="https://user-images.githubusercontent.com/74157573/184043188-1cd6eaa2-58ab-4864-bc6f-3ae3e92581c8.png">

## Sensor Fusion
Up to this point we had just been working with Lidar data since in someways the location has an accuarate depiction in space (ex. x,y,z) in this step we included the camera data. This required a bit more complex math from the camera data. Finally, putting including a combination of both sensors greatly reduced the error rate, as seen in the graph below.

<img width="1618" alt="image" src="https://user-images.githubusercontent.com/74157573/184266477-45d213c6-70fe-4b52-8757-9cf41fe45013.png">

## Review Questions
1. Write a short recap of the four tracking steps and what you implemented there (EKF, track management, data association, camera-lidar sensor fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?</br>
</tab></tab>***See the above sections for a short recap. I would say the association was the most difficult as the matrix needs to managed appropiately.***

1. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)?</br>
</tab></tab>***Yes, in theory data from two sensors should allow us to complete updates more frequently, since we will always have a sensor to update our predictions. This was seen in the low RMSE scores.***

1. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?</br>
</tab></tab>***If a car were to pull out infront of the self driving car, I would be concerened about the time that it takes to do all the proceccing to find the object and press the brakes. Yes, in the project frames were displayed in slower than real time. There coulc be some delay do to the computer displaying images, but there would be a concern that we are adding to much latency.***

1. Can you think of ways to improve your tracking results in the future?</br>
</tab></tab>***Yes if there was other camera and lidar sensors offset of the vieichles sensor, this would give us different perspective and could improve results.***
