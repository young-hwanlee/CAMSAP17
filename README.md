# Predicting Voltage Stability Margin via Learning Stability Region Boundary
Published in: 2017 IEEE 7th International Workshop on Computational Advances in Multi-Sensor Adaptive Processing (CAMSAP). For more information, please refer to the paper.

## Abstract
Preventing voltage collapse is critical for the reliable operation of the power grid. In this paper, the voltage stability margin, which is deﬁned as the distance from a given power proﬁle to the boundary of the stability region, is efﬁciently estimated using a data-driven machine learning approach. The key idea is to train a neural network classiﬁer to learn the boundary of the potentially nonconvex stability region, and exploit the resulting score metric as the regressor for stability margin prediction. No particular loading direction is assumed, but rather the minimum distance to the boundary along all possible directions is captured. The training samples are generated from both continuation and semideﬁnite relaxation power ﬂow methods. The performance and computational advantage of the proposed approach are veriﬁed by numerical experiments.

## Neural Network Architecture
<img width="576" alt="NN" src="https://user-images.githubusercontent.com/67979833/87262631-ab7e5100-c488-11ea-97a3-c010d1108dc2.png">

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

## Results
<img width="576" alt="marginfit" src="https://user-images.githubusercontent.com/67979833/87262637-b0db9b80-c488-11ea-911c-9b6f5bcca91d.png">
