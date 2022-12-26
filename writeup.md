[//]: # (Image References)

[RMSE1]: ./img/RMSE1.png
[RMSE2]: ./img/RMSE2.png

# Writeup: Track 3D-Objects Over Time

Please use this starter template to answer the following questions:

### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

FILTER: 根据之前的EKF练习，很容易就实现了Filter class，最终得到的RMSE平均值是0.32。我还尝试了调整process noise covariance Q，当其为零矩阵时，RMSE的平均值是0.35. ![RMSE1]

TRACK MANAGEMENT: 我以1./params.window为单位进行track.score的增减，可以观察到从"initialized"到"tentative"，再到"confirmed"的状态变化过程。有个疑问，manage_tracks方法中的meas_list一直为空，导致track.score不减少，不知道是否正常？By the way, RMSE的平均值是0.78. ![RMSE2]

### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 


### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?


### 4. Can you think of ways to improve your tracking results in the future?

