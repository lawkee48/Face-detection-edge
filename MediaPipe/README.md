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

Reference
--
- Google github. Mediapipe. https://google.github.io/mediapipe/solutions/face_detection
