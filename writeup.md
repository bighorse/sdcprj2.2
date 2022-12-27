[//]: # (Image References)

[RMSE1]: ./img/RMSE1.png
[RMSE2]: ./img/RMSE2.png
[RMSE3]: ./img/RMSE3.png
[RMSE4]: ./img/RMSE4.png

# Writeup: Track 3D-Objects Over Time

Please use this starter template to answer the following questions:

### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

FILTER: 根据之前的EKF练习，很容易就实现了Filter class，最终得到的RMSE平均值是0.32。我还尝试了调整process noise covariance Q，当其为零矩阵时，RMSE的平均值是0.35. ![RMSE1]

TRACK MANAGEMENT: 我以1./params.window为单位进行track.score的增减，可以观察到从"initialized"到"tentative"，再到"confirmed"的状态变化过程。这部分遇到个小问题，没有找到6D的F和Q的矩阵公式。我根据4D公式推演了一个，效果看起来还不错，RMSE的平均值是0.78. ![RMSE2]

ASSOCIATION: 初始化很快。对"confirmed"状态的车辆的识别很稳定，也很准确。发现了一些“ghost tracks”，但是最多发展到"tentative"状态，然后就被删除。最终的RMSE平均值也都很好。 ![RMSE3]

CAMERA FUSION: 我参考liDar的算法，为Camera的measurement初始化实现了2D的R矩阵，效果似乎还可以。加上Camera之后，“ghost tracks”彻底消失，较远处的车辆也能识别出来了（最多发展到"tentative"状态）。最终的RMSE平均值非常棒！ ![RMSE4]

### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 


### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?


### 4. Can you think of ways to improve your tracking results in the future?

