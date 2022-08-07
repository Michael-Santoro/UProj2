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

<img width="916" alt="image" src="https://user-images.githubusercontent.com/74157573/183304480-02253f9b-ff05-4524-8f91-8cdcd5bdcfb1.png">
