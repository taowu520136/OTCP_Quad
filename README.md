# Optimal tracking control for unknown-dynamics quadrotor with an Off-policy Reinforcement Learning(RL) algorithm
An Off-policy Reinforcement Learning Algorithm for Optimal Tracking Control Problem       
Full report: [link](https://drive.google.com/drive/folders/1LOUQExAoRkOGeKZ26fC8hELxbSGDK5ZK)
# 1. Introduction
In this project, the optimal tracking control problem (OTCP) for the quadrotor which is a highly coupling system with completely unknown dynamics is addressed based on data by introducing the reinforcement learning (RL) technique. The proposed Off-policy RL algorithm does not need any knowledge of the quadrotor model. By collecting data, which is the states and control inputs of the quadrotor system, then using an actor-critic network (NNs) to approximate the optimal controller, OTCP for the quadrotor is resolved. Finally, simulation results are provided to illustrate the effectiveness of the proposed method.

# 2. Problem Statement

![quad_schematic](https://github.com/duongdinhph/OTCP_Quad/assets/56771011/8a8c3980-18f1-42e6-90e9-5f29923f5434)   

In this section, we present the quadrotor model and the traditional control scheme. A quadrotor could be described with dynamic equations: $$m \ddot{p} = T_p R e_{3,3} - m g e_{3,3} $$

Where:   
* The position of the center of mass is $p = [p_x,p_y,p_z]^T \in \mathbb{R}^3$
* The Euler angles $\Theta = [\phi, \theta, \psi]$.
* $e_{i,j}$ is the vector which has $i$ numbers of zeros except for number 1 in the $j^{th}$ position.

# 3. RL algorithm for Optimal tracking control problem of the affine system:
* Non-linear aﬀine system:
$$\dot{X}(t) = F(X(t)) + G(X(t))u(t)$$
* The cost function:
$$V(X(t))=\int_{t}^{\infty}e^{-\lambda(\tau-t)}[X(\tau)^TQX(\tau)+u(\tau)^TRu(\tau)]d\tau$$
The Rl algorithm comprises 3 steps:
* Step 1: Init
Start with a stable control signal $u_0$ and add a noise component $u_e$ to ensure the PE condition. Collect data and determine threshold $\epsilon$
* Step 2: Policy Evaluation and Policy Improvement:
$$ V^{i+1}(X(t+\delta t)) - V^{i+1}(X(t)) =  -\int_{t}^{t+\delta t}[X(\tau)^TQX(\tau)
					+ [u^i(X(\tau))]^TRu^i(X(\tau))]d\tau + \int_{t}^{t+\delta t}\lambda V^{i+1}(X(\tau))d\tau 
					+ 2\int_{t}^{t+\delta t}[u^{i+1}(X(\tau))]^TR[u^i(X(\tau)) - u(\tau)] d\tau $$
* Step 3: Checking convergence
Stop iterating if $\| u^{i+1}-u^i \| < \epsilon$, otherwise: update $u^i = u^{i+1}$, return to step (2).



  







# 4. The proposed control scheme applied for a quadrotor:
![Quad_Control_Diagram](https://github.com/duongdinhph/OTCP_Quad/assets/56771011/306f37f3-1ca5-46a6-9e22-f797f3e7797e)
  ## 2.1. Position Controller with Off-policy RL
  
  ## 2.2. Attitude Controller with Off-policy RL
  
# 3. Simulation
![3D_tracking_skew](https://github.com/duongdinhph/OTCP_Quad/assets/56771011/5f818f3d-f018-494b-a6ec-4f97d2e55295)

Consider a quadrotor with the desired trajectory as a spiral trajectory
In the first stage, we use 2 PID controllers for both outer and inner loops to collect data for the next
stage of training to obtain the optimal controllers. Note that noises are added to the system to guarantee
the PE condition.

![xyz_wrt_ref](https://github.com/duongdinhph/OTCP_Quad/assets/56771011/be6b3386-5f5b-419b-b4d3-0e306fc9f110)

The position tracking error in this stage is illustrated in the figure above.
Then, we use the data as the input to the algorithms which are proposed in the previous section. The
convergences of the weights are shown in the figure above.
After we obtain the weights, estimated optimal controllers are applied to the object. The tracking
performance is illustrated in figure above.
# 4. Conclusion
In this project, a novel control strategy that consists of the Off-policy RL algorithm was proposed. By
collecting data to train two actor-critic networks (NNs) which aim to estimate the optimal controllers
which includes a position controller and attitude controller, this structure has the advantage of no need
of any prior information on the high coupling system. Finally, simulation results are provided to
illustrate the tracking performance of a sophisticated trajectory of the system.


