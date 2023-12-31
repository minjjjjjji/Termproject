# Welcome to our OSS Termproject
This repository is made for termproject "Open source SW".

---

# Project Overview
This project provides a functionality to **detect eyes and mouth on a snowman's face template and seamlessly blend these facial features with another image.** 
The project is primarily developed using **dlib, OpenCV, Numpy, and imutils** packages.

---

# Demo or Example Images/Videos

result

<img width="510" alt="result" src="https://github.com/minjjjjjji/Termproject/assets/144930775/d2486fd0-42c3-4279-a2f1-735e3e12b205">


mouth and eyes

<img width="196" alt="mouth" src="https://github.com/minjjjjjji/Termproject/assets/144930775/57c0b447-e034-451c-82de-5802c353ee62">

<img width="184" alt="eye1" src="https://github.com/minjjjjjji/Termproject/assets/144930775/e05c4009-cddb-47e1-897f-c051464a9acf">

<img width="194" alt="eye2" src="https://github.com/minjjjjjji/Termproject/assets/144930775/d67530db-4e29-4ca8-b53e-af6f6416d6ea">


face 

<img width="252" alt="face" src="https://github.com/minjjjjjji/Termproject/assets/144930775/f9b5acb5-f25c-4c39-b5ad-faa15e907757">

---

# Used Packages and Versions

1. dlib(19.24.2): **pip install dlib**

2. OpenCV(4.8.1.78): **pip install opencv-python**

3. Numpy(1.26.2): **pip install numpy**

4. imutils(0.5.4): **pip install imutils**

---

# Execution Instructions

1. Install Libraries: Install the required packages using the following commands:
```sh
pip install dlib opencv-python numpy imutils
```
2. Download Project: Clone or download the project.

3. Run the Code: Execute the following code to test the project:

---

# Explain some codes about **python landmarks.py**

#### Initalizing the face detector from dlib
```sh
face_det = dlib.get_frontal_face_detector()
```
#### Loading the facial landmarks predictor model
```sh
landmark_model = dlib.shape_predictor("shape_predictor_68_face_landmarks.dat")
```
#### Defining constants for different facial regions
```sh
ALL = list(range(0, 68))
RIGHT_EYEBROW = list(range(17, 22))
LEFT_EYEBROW = list(range(22, 27))
RIGHT_EYE = list(range(36, 42))
LEFT_EYE = list(range(42, 48))
NOSE = list(range(27, 36))
MOUTH_OUTLINE = list(range(48, 61))
MOUTH_INNER = list(range(61, 68))
JAWLINE = list(range(0, 17))
index = ALL
```
#### Extracting landmark points and convert them to a NumPy array
```sh
 lm_point = []
for p in lm.parts():
   lm_point.append([p.x, p.y])
lm_point = np.array(lm_point)
```
#### Drawing circles at each landmark point on the original image
```sh
for p in lm_point:
    cv.circle(src, (p[0], p[1]), radius=2, color=(255, 0, 0), thickness=2)
```
#### Displaying the result image with landmarks
```sh
 cv.imshow("result", src)
 ```
#### Waiting for a key press and close the display window
```sh
cv.waitKey()
cv.destroyAllWindows()
```

---

# Explain some codes about **python snowman.py**

#### Loading and resizing the snowman image
```sh
snowman_img = cv2.imread('snowman.jpg')
snowman_img = cv2.resize(snowman_img, dsize=(512, 512))
```

#### Initializing face detector and shape predictor
```sh
detector = dlib.get_frontal_face_detector()
predictor = dlib.shape_predictor('shape_predictor_68_face_landmarks.dat')
```
#### Checking if faces are detected
```sh
if len(faces) > 0:
    face = faces[0]
```

#### Extracting face region
```sh
x1, y1, x2, y2 = face.left(), face.top(), face.right(), face.bottom()
face_img = img[y1:y2, x1:x2].copy()
```
#### Predicting facial landmarks
```sh
shape = predictor(img, face)
shape = face_utils.shape_to_np(shape)
```
#### Drawing circles on the facial landmarks
```sh
for p in shape:
    cv2.circle(face_img, center=(p[0] - x1, p[1] - y1), radius=2, color=255, thickness=-1)
```
---

# References

1. https://blog.naver.com/juachef/222982605787
2. https://bkshin.tistory.com/entry/OpenCV-9-이미지-연산

