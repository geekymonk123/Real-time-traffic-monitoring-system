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
shown in equation.
```
Normalized_image = (I − mean) ÷ std     
```
**Object Classification:**

After detecting the car object now we have to
classify them as they are static or dynamic for static no bounding boxes
are there but for dynamic movement of the vehicles are bounded with
bounding boxes.

**Speed Estimation:**

After extracting the dynamic car object from the
background we estimate the speed of the object on each frame from a certain distance of 1km. The following process of estimating the speed of the vehicle is shown in the following.

**1.** Here we have taken the coordinates of the bounding boxes of the
object detected from the previous frame and current frame. and calculate the euclidean distance between the coordinates and return the
pixel form value for further calculation.

**2.** The returned value is not in a compatible format (i.e. pixel) so we convert it to meter. To do so, we multiply the focal length of the camera by 2 and divide it by pixel value. Here, we multiply the focal
length by 2 because it is like a scaling factor that acts as a diagonal of the bounding box and in this case, it’s assumed to be a square.

- distance(meters) ← (focallength ∗ 2) ÷ (distance_pixels)

**3.** Converting the speed from meter per second to km per hour

- speed(ms) ← distance(meters) ÷ time_dif f (sec) (3)
- speed(kmph) ← speed(ms) ∗ 3.6

Here, is the detailed analysis of how and why we use this type of calculation using equations mentioned above.

