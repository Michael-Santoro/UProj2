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

<img width="458" alt="image" src="https://user-images.githubusercontent.com/74157573/183799002-26746339-7bcf-48eb-bcf4-a1892e3b3dec.png">


## Track Management

This step was primarily to complete the track management class and the track class. There is code related to updating track scores and deleting unassociated tracks based on conditions.

<img width="602" alt="image" src="https://user-images.githubusercontent.com/74157573/183799203-50cd4855-abb9-463e-b02b-49581ede8f7b.png">

## Data Association
This step is the big connecting part of the project where tracks are managed in the association matrix. This was a challenge for me since I forgot to update the get_closest association function.

<img width="907" alt="image" src="https://user-images.githubusercontent.com/74157573/183313057-841cb671-3218-40e9-9d8f-a89ccd9fc12d.png">

## Sensor Fusion
Up to this point we had just been working with Lidar data since in someways the location has an accuarate depiction in space (ex. x,y,z) in this step we included the camera data. This required a bit more complex math from the camera data. Finally, putting including a combination of both sensors greatly reduced the error rate, as seen in the graph below.

<img width="589" alt="image" src="https://user-images.githubusercontent.com/74157573/183795797-13ce2ae8-5b71-4584-892b-3a724a999a83.png">

