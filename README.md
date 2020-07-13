# Predicting Voltage Stability Margin via Learning Stability Region Boundary
Published in: 2017 IEEE 7th International Workshop on Computational Advances in Multi-Sensor Adaptive Processing (CAMSAP). For more information, please refer to the paper.

## Abstract
Preventing voltage collapse is critical for the reliable operation of the power grid. In this paper, the voltage stability margin, which is deﬁned as the distance from a given power proﬁle to the boundary of the stability region, is efﬁciently estimated using a data-driven machine learning approach. The key idea is to train a neural network classiﬁer to learn the boundary of the potentially nonconvex stability region, and exploit the resulting score metric as the regressor for stability margin prediction. No particular loading direction is assumed, but rather the minimum distance to the boundary along all possible directions is captured. The training samples are generated from both continuation and semideﬁnite relaxation power ﬂow methods. The performance and computational advantage of the proposed approach are veriﬁed by numerical experiments.

## Neural Network Architecture
<img width="576" alt="NN" src="https://user-images.githubusercontent.com/67979833/87262631-ab7e5100-c488-11ea-97a3-c010d1108dc2.png">
Output layer: Hinge Loss

> L = max(-xy + 1, 0) 
> where x is the score computed from the output layer, and y is the binary label {-1,1}

## Dataset
<table align='center'>
<tr align='center'>
<td> Sampling method </td>
<td> Power profiles in a nonconvex stability region </td>
</tr>
<tr>
<td><img width="576" alt="sampling_for_distance" src="https://user-images.githubusercontent.com/67979833/87262622-a3261600-c488-11ea-979d-7f15b1196154.png">
<td><img width="576" alt="feasible" src="https://user-images.githubusercontent.com/67979833/87262623-a5887000-c488-11ea-9b56-5a2e06d7a154.png">
</tr>
</table>

The samples were generated using MATPOWER package [1]. The sampling method is as follows: 
> 1. A random power profile vector 's' was generated, including the real and reactive powers for the loads and the real powers for the generators. (To do this, the power factor for each load bus was uniformly sampled in the interval [0.4,1], so that the average power factor can be 0.7. Then, the reactive power demands were adjusted to yield the sampled power factors. The load buses with real or reactive power demands equl to 0 were ignored.) 
> 2. Based on the sampled power profile, two boundary points were computed; using the continuation power flow for the feasible boundary points () and the SDP relaxation-based power flow for the infeasible boundary points. 
> 3. $\text{S}_1(N) = \sum_{p=1}^N \text{E}(p)$

## Results
<img width="576" alt="marginfit" src="https://user-images.githubusercontent.com/67979833/87262637-b0db9b80-c488-11ea-911c-9b6f5bcca91d.png">

## References
[1] R. D. Zimmerman, C. E. Murillo-Snchez, and R. J. Thomas, “MATPOWER: Steady-state operations, planning and analysis tools for power systems research and education,” IEEE Trans. Power Syst., vol. 26, no. 1, pp. 12–19, Feb. 2011.
