MediaPipe Face Detection
--
MediaPipe Face Detection is an ultrafast face detection solution that comes with 6 landmarks and multi-
face support. It is based on [BlazeFace](https://arxiv.org/abs/1907.05047), a lightweight and well-performing face detector tailored for
mobile GPU inference. The detector’s super-realtime performance enables it to be applied to any live 
viewfinder experience that requires an accurate facial region of interest as an input for other task-
specific models, such as 3D facial keypoint or geometry estimation (e.g., [MediaPipe Face Mesh](https://google.github.io/mediapipe/solutions/face_mesh.html)), facial
features or expression classification, and face region segmentation. BlazeFace uses a lightweight feature
extraction network inspired by, but distinct from [MobileNetV1/V2](https://ai.googleblog.com/2018/04/mobilenetv2-next-generation-of-on.html), a GPU-friendly anchor scheme modified
from [Single Shot MultiBox Detector (SSD)](https://arxiv.org/abs/1512.02325), and an improved tie resolution strategy alternative to 
non-maximum suppression. For more information about BlazeFace, please see the Resources section.

### Configuration Options
*(Naming style and availability may differ slightly across platforms/languages.)*

- MODEL_SELECTION *(Default is 0)*\
An integer index `0` or `1`. Use 0 to select a **short-range model** that works best for faces within 2 meters
from the camera, and 1 for a **full-range model** best for faces within 5 meters. For the full-range option,
a sparse model is used for its improved inference speed. Please refer to the [model cards](https://google.github.io/mediapipe/solutions/models.html#face_detection) for details.

- MIN_DETECTION_CONFIDENCE *(Default is 0.5)*\
Minimum confidence value `([0.0, 1.0])` from the face detection model for the detection to be considered successful.

### Output
*(Naming style may differ slightly across platforms/languages.)*
- DETECTIONS\
Collection of detected faces, where each face is represented as a detection proto message that contains
a **bounding box** and **6 key points** (right eye, left eye, nose tip, mouth center, right ear tragion, and left
ear tragion).The bounding box is composed of `xmin` and `width` (both normalized to `[0.0, 1.0]` by the image width)
and `ymin` and `height` (both normalized to `[0.0, 1.0]` by the image height). Each key point is composed of `x` and `y`,
which are normalized to `[0.0, 1.0]` by the image width and height respectively.

### API
For the tutorial of how to use API in different language please follow the example and instruction on [Mediapipe official website](https://google.github.io/mediapipe/solutions/face_detection#resources)
#### Python API
```
import cv2
import mediapipe as mp
mp_face_detection = mp.solutions.face_detection
mp_drawing = mp.solutions.drawing_utils

# For static images:
IMAGE_FILES = []
with mp_face_detection.FaceDetection(
    model_selection=1, min_detection_confidence=0.5) as face_detection:
  for idx, file in enumerate(IMAGE_FILES):
    image = cv2.imread(file)
    # Convert the BGR image to RGB and process it with MediaPipe Face Detection.
    results = face_detection.process(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))

    # Draw face detections of each face.
    if not results.detections:
      continue
    annotated_image = image.copy()
    for detection in results.detections:
      print('Nose tip:')
      print(mp_face_detection.get_key_point(
          detection, mp_face_detection.FaceKeyPoint.NOSE_TIP))
      mp_drawing.draw_detection(annotated_image, detection)
    cv2.imwrite('/tmp/annotated_image' + str(idx) + '.png', annotated_image)

# For webcam input:
cap = cv2.VideoCapture(0)
with mp_face_detection.FaceDetection(
    model_selection=0, min_detection_confidence=0.5) as face_detection:
  while cap.isOpened():
    success, image = cap.read()
    if not success:
      print("Ignoring empty camera frame.")
      # If loading a video, use 'break' instead of 'continue'.
      continue

    # To improve performance, optionally mark the image as not writeable to
    # pass by reference.
    image.flags.writeable = False
    image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    results = face_detection.process(image)

    # Draw the face detection annotations on the image.
    image.flags.writeable = True
    image = cv2.cvtColor(image, cv2.COLOR_RGB2BGR)
    if results.detections:
      for detection in results.detections:
        mp_drawing.draw_detection(image, detection)
    # Flip the image horizontally for a selfie-view display.
    cv2.imshow('MediaPipe Face Detection', cv2.flip(image, 1))
    if cv2.waitKey(5) & 0xFF == 27:
      break
cap.release()
```

or you can visit Kazuhito00 github [Kazuhito00 github](https://github.com/Kazuhito00/mediapipe-python-sample) for more MediaPipe Python example.
*e.g.,*
```
python3 sample_hand.py
```

Reference
--
- Google github. Mediapipe. https://google.github.io/mediapipe/solutions/face_detection
- MediaPipe Python example. Kazuhito00 github. https://github.com/Kazuhito00/mediapipe-python-sample
