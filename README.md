# Human-Pose-Estimation-101


# Table of Contents
- [Basics](#basics)
- [Loss](#loss)
- [Evaluation metrics](#evaluation-metrics)
  - [PCP](#percentage-of-correct-parts---pcp)
  - [PCK](#percentage-of-correct-key-points---pck)
  - [PDJ](#percentage-of-detected-joints---pdj)
  - [MPJPE](#mean-per-joint-position-error---mpjpe)
  - [AUC](#auc)
 - [Important applications](#important-applications)
 - [Extra](#Informative-roadmap-on-2d-human-pose-estimation-research)

# Basics

## Human Pose estimation
- Defined as the problem of localisation of human joints (or) keypoints
- A rigid body consists of joints and rigit parts. A body with strong articulation is a body with strong contortion. 
- Pose estimation is the search for a specific pose in space of all articulated poses
- Number of keypoints varies with dataset -  LSP has 14, MPII has 16, Human3.6 has 16
- Classifed into 2D  and 3D pose estimation
  - __2D Pose estimation__
  - Estimate a 2D pose (x,y) coordinates for each joint in pixel space from a RGB image
  - __3D pose estimation__
  - Estimate a 3D pose (x,y,z) coordinates in metric space from a RGB image, or in previous works, data from a RGB-D sensor.    (However, research in the past few years is heavily focussed on generating 3D poses from 2D images / 2D videos)

## Loss
- Most commonly used loss function - Mean squared loss function (Least squares loss)
- This is a regression problem. The model will try to regress to the the correct coordinates, i.e move to the ground truth coordinatate’s in small incremeents. The model is trained to output continuous coordinates using a Mean squared loss function

## Evaluation metrics

### Percentage of Correct Parts - PCP
- A limb is considered detected and a correct part if the distance between the two predicted joint locations and the true limb joint locations is at most half of the limb length (PCP at 0.5 )
- Measures detection rate of limbs
- Cons - penalizes shorter limbs
- __Calculation__
  - For a specific part, PCP = (No. of correct parts for entire dataset) / (No. of total parts for entire dataset)
  - Take a dataset with 10 images and 1 pose per image. Each pose has 8 parts - ( upper arm, lower arm, upper leg, lower leg ) x2
  - No of upper arms = 10 * 2 = 20
  - No of lower arms = 20
  - No of lower legs = No of upper legs = 20
  - If upper arm is detected correct for 17  out of the 20 upper arms i.e 17 ( 10 right arms and 7 left) → PCP = 17/20 = 85% 
- Higher the better 

### Percentage of Correct Key-points - PCK
- Detected joint is considered correct if the distance between the predicted and the true joint is within a certain threshold (threshold varies)
- PCKh@0.5 is when the threshold = 50% of the head bone link
- PCK@0.2 == Distance between predicted and true joint < 0.2 * torso diameter 
- Sometimes 150 mm is taken as the threshold
- Head, shoulder, Elbow, Wrist, Hip, Knee, Ankle → Keypoints 
- PCK is used for 2D and 3D (PCK3D)
- Higher the better

### Percentage of detected joints - PDJ
- Detected joint is considered correct if the distance between the predicted and the true joint is within a certain fraction of the torso diameter
- Alleviates the shorter limb problem since shorter limbs have smaller torsos
- PDJ at 0.2 → Distance between predicted and true join < 0.2 * torso diameter
- Typically used for 2D Pose Estimation
- Higher the better

### Mean Per Joint Position Error - MPJPE
- Per joint position error = Euclidean distance between Ground truth and Prediction for a joint
- Mean per joint position error = Mean of per joint position error for all k joints (Typically, k = 16)
- Calculated after aligning the root joints (typically the pelvis) of the estimated and groundtruth 3D pose. 
- __PA MPJPE__
  - Procrustes analysis MPJPE. 
  - MPJPE calculated after the estimated 3D pose is aligned to the groundtruth by the [Procrustes method](https://www.coursera.org/lecture/robotics-perception/pose-from-3d-point-correspondences-the-procrustes-problem-X22IH)
  - Procrustes method is simply a similarity transformation
- Lower the better
- Used for 3D pose estimation

<!-- ## AUC
https://medium.com/greyatom/lets-learn-about-auc-roc-curve-4a94b4d88152
https://www.robots.ox.ac.uk/~vgg/publications/2012/Jammalamadaka12a/jammalamadaka12a.pdf --> 

## Important Applications
- Activity recognition
- Human-Computer Interaction
- Virtual Reality
- Augmented Reality
- Amazon Go presents an important domain for the application of human pose estimation. Cameras track and recognize people and their actions, for which pose estimation is an important component. Entities relying on services that track and measure human activities rely heavily on human pose estimation

## Informative roadmap on 2D Human pose estimation research
- [Presentation by Wei Yang](https://www.slideshare.net/plutoyang/mmlab-seminar-2016-deep-learning-for-human-pose-estimation)
