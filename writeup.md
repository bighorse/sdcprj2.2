[//]: # (Image References)

[RMSE1]: ./img/RMSE1.png
[RMSE2]: ./img/RMSE2.png
[RMSE3]: ./img/RMSE3.png
[RMSE4]: ./img/RMSE4.png

# Writeup: Track 3D-Objects Over Time

### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

FILTER: 

According to the previous EKF exercise, it is easy to implement the Filter class, and the final RMSE average is 0.32. In this part, I encountered a small problem. I did not find the matrix formulas of F and Q of 6D. I deduced one based on the 4D matrix formula, and the effect looks pretty good. I also tried to adjust the process noise covariance Q, when it is a zero matrix, the mean value of RMSE is 0.35. ![RMSE1]

TRACK MANAGEMENT: 

I increase or decrease track.score in units of 1./params.window, and I can observe the state change process from "initialized" to "tentative" and then to "confirmed". The average RMSE is 0.78, not good.![RMSE2]

ASSOCIATION: 

Initialization is fast. The recognition of vehicles in the "confirmed" state is stable and accurate. A few "ghost tracks" were found, but at most progressed to "tentative" status and then deleted. The final RMSE average are all good as well. ![RMSE3]

CAMERA FUSION: 

Referring to the algorithm of liDar, I implemented a 2D's R matrix for the initialization of the measurement of the Camera, and the effect seems to be OK. After adding Camera, "ghost tracks" disappear completely, and vehicles in the distance can also be recognized (up to "tentative" state at most). The final RMSE average is great! ![RMSE4]
My tracking results movie(./my_tracking_results.avi):
https://github.com/bighorse/sdcprj2.2/blob/ce81636d6c8ce3af22fe793cbf99f7dab99454d1/my_tracking_results.avi

### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 

Obtaining 3D point clouds through liDar, and then applying the mature Computer Vision pre-trained model, can achieve very accurate recognition of large objects such as vehicles, and its effect is better than 2D image recognition. However, liDar is not good at recognizing small objects and details of objects, such as speed limit signs, traffic lights, etc. Camera-based image recognition technology is better in these aspects.

When working on this project, I found that the misidentification problems of Camera and LiDar are different. Camera easily misidentifies buildings as vehicles, while LiDar easily misidentifies shrubs on the side of the road as vehicles. When the fusion algorithm is adopted, the problem of misidentification is perfectly solved. Therefore, I think that instead of trying to improve the accuracy of the image recognition model, it is easier and better to use sensor fusion.

### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?

The sensor fusion system requires multiple sensors, including lidar, camera, etc., and there are more than one, so the cost will be high. In addition, because the image recognition models of lidar and camera need to be inferred separately, when doing this project, I feel that the program is very complicated, and the requirements for computing performance are also very high.

### 4. Can you think of ways to improve your tracking results in the future?

* Learn the fpn_resnet models, then improve the recognition accuracy by adjusting the parameters.
* Fine-tune the parameters in misc/params.py, then check the effect by RMSE.
* Implement a more advanced data association, e.g. Global Nearest Neighbor (GNN) or Joint Probabilistic Data Association (JPDA).