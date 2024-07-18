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
```
 distance(meters) ← (focallength ∗ 2) ÷ (distance_pixels)
```
**3.** Converting the speed from meter per second to km per hour
```
speed(ms) ← distance(meters) ÷ time_dif f (sec) (3)
speed(kmph) ← speed(ms) ∗ 3.6
```
Here, is the detailed analysis of how and why we use this type of calculation using equations mentioned above.

<img src="https://github.com/geekymonk123/Real-time-traffic-monitoring-system/blob/main/Speed%20estimation.png" alt="MLBC">
Fig 1. Graphical Representation of Speed Estimation

Our model is very simple to handle the situation with the help of only
camera and camera calibration settings that are only the focal length.
So, let’s explain how it does so from Figure 1 it is shown that a car object
was at position (x1,y1) and traversed to (x2,y2) at time t2. here we could
easily find the distance between the two coordinates using the Euclidean
distance. Here we calculated the distance between the coordinates in
pixel format.
Then we need to convert it to a meter to meet with the real-world scenario. To do so we adjust the camera calibration with a focal length of
1km or 1000 meters. We then use this here to calculate the distance in
meters.
The reason to use the factor 2 is the empirical adjustment of the setup to
make more accuracy while estimating the speed of the vehicle. We may assume that it’s a scaling factor of the diagonal of the bounding box of
the object to be a square for easy interpretation. Then we calculate the speed in meter per sec. here we estimate the time difference of the object
to traverse from the coordinate from(x1,y1) to (x2,y2). Then we convert it into km per hour. For that object, the following license plate number
is also detected. This is not only for a single vehicle but also for multiple vehicles.

**License Number plate Detection:** In this paragraph, we will discuss how we estimate the license number plate prediction. Here we used the
Easy OCR model rather than the Tesseract model because of its simplicity and more accurate results which is explained in result section. Here it extract the ROI(Region of Interest) from the input image and converts it to a grayscale image. Easy OCR model extracts the optical
character from the image and returns the license number as the string. For converting RGB to Gray Scale it uses the formula.
```
Igray = 0.299R + 0.587G + 0.114B
```
The returned string is verified with some constraints mentioned like
whether the length of the string is greater than 6 and it is alphanumeric
format.

## Experimental Result


