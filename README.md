# Real Time Traffic Monitoring using Road Side Digital Camera
Due to the rise of private vehicles (e.g., car) makes road traffic more congested. To resolve this complex situation without manual road traffic monitoring, computer vision takes place. The dedicated road surveillance cameras and sensors are used as helping devices. Both
are costly. However, we are using the road side digital camera for road
traffic monitoring. Our research work mainly focused on vehicle detec-
tion along with the speed estimation and license plate detection with
the same camera in this article. The proposed method uses neural net-
work techniques Faster R-CNN for speed estimation, and for license plate
detection we use easy optical character recognition (OCR) system to ex-
tract the alphanumeric characters. Here we trained and tested our model
on 3 different scenarios and over 30 vehicles and get a result of 93.7%
accuracy for speed estimation and 87.5% on license plate detection.

## Proposed Methodology
To prepare a cost-effective road traffic monitoring system, a single-camera
is used for three different tasks 

**(i)** car object detection and classification,

**(ii)** speed estimation, and license plate number detection.

Algorithm 1 depicts how the roadside camera could estimate speed and
license plate detection is done. Here the user needs to give the input video
with the focal length adjusted. We first identify the key frames using
the entropy of the frames. If the frame is a key frame then process the
frame and do the following sub-actions. Firstly, detect the car object and
classify whether static or dynamic. Secondly, for each vehicle detected
estimate the speed, and thirdly, detect the license plate number for that
vehicle. The detailed explanation of above 3 sub-actions are explained in
detail in the below paragraphs.

<img src="https://github.com/geekymonk123/Real-time-traffic-monitoring-system/blob/main/Algorithm.jpg" alt="MLBC">

**Object Detection:**

It detects the car object from each frame by using a
pre-trained Faster RCNN model on the car object. Here it takes an input
image then it resized, and normalizes the image i.e. adjusting the pixel
values and transforming the image to a tensor then it infers the tensor
form to detect the object along with the bounding box. The formula is
shown in equation 1.

Normalized_image = (I − mean) ÷ std               (1)

