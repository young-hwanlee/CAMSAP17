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
<td> Power profiles in a nonconvex stability region </td>
<td> Sampling method </td>
</tr>
<tr>
<td><img width="576" alt="feasible" src="https://user-images.githubusercontent.com/67979833/87262623-a5887000-c488-11ea-9b56-5a2e06d7a154.png">
<td><img width="576" alt="sampling_for_distance" src="https://user-images.githubusercontent.com/67979833/87262622-a3261600-c488-11ea-979d-7f15b1196154.png">
</tr>
</table>

The samples were generated using MATPOWER package [1]. The sampling method is as follows: 
### 1. Sample Generation for Learning the Stability Boundary
> 1. A random power profile vector 's' was generated, including the real and reactive powers for the loads and the real powers for the generators. (To do this, the power factor for each load bus was uniformly sampled in the interval [0.4,1], so that the average power factor can be 0.7. Then, the reactive power demands were adjusted to yield the sampled power factors. The load buses with real or reactive power demands equl to 0 were ignored.) 
> 2. Based on the sampled power profile, two boundary points were computed; using the continuation power flow for the feasible boundary points 's(η_c)' and the SDP relaxation-based power flow for the infeasible boundary points 's(η_s)'. 

### 2. Sample Generation for Learning the Minimum Distance from an Operating Point to the Stability Boundary
> 1. A feasible power profile was picked from the data set already generated above. 
> 2. A profile 's_1' was obtained by shrinking the profile by a random amount (new base profile). 
> 3. Another feasible power profile 's_2' was similarly obtained.  
> 4. Then, the continuation power flow method was used to obtain a boundary point 's_1 + η(s_2 - s_1)' (new target profile). 
> 5. The profile 's_1' and the minimum distance '||η^* (s_2 - s_1)|| were recorded after performing the 3~4 steps N times, where η^* = arg min η.

## Results
### 1. Learning Stability Boundary
Based on the feasible and infeasible data points, a neural network with one hidden layer is trained for a binary classifier. The trained neural network achieves an testing classification accuracy of 99.9%.

### 2. Predicting Stability Margin
With the trained binary classifier, the scores computed at the output layer is used to fit a predictor of the voltage stability margin. A scatter plot of score-margin pairs and the fitted function are plotted below. The fitted linear function achieves an R-squared measure of 0.71, indicating reasonably good performance as follows:  
<img width="576" alt="marginfit" src="https://user-images.githubusercontent.com/67979833/87262637-b0db9b80-c488-11ea-911c-9b6f5bcca91d.png">

## References
[1] R. D. Zimmerman, C. E. Murillo-Snchez, and R. J. Thomas, “MATPOWER: Steady-state operations, planning and analysis tools for power systems research and education,” IEEE Trans. Power Syst., vol. 26, no. 1, pp. 12–19, Feb. 2011.
