MediaPipe face detection on Jetson
--
## Installation
```
./install_opencv4.5.0_Jetson.sh    # it may take 2 - 3 hours
sudo apt-get install curl
git clone https://github.com/PINTO0309/mediapipe-bin
cd mediapipe-bin
./v0.8.5/numpy119x/mediapipe-0.8.5_cuda102-cp36-cp36m-linux_aarch64_numpy119x_jetsonnano_L4T32.5.1_download.sh   (這個 sh 檔會下載一些檔案)
sudo pip3 install numpy-1.19.4-cp36-none-manylinux2014_aarch64.whl
sudo pip3 install mediapipe-0.8.5_cuda102-cp36-none-linux_aarch64.whl
sudo pip3 install dataclasses
cd ~
git clone https://github.com/Kazuhito00/mediapipe-python-sample 
cd mediapipe-python-sample
```

Reference
--
- 在 Jetson Nano 上執行 Google Mediapipe，立即可用的辨識方案超好用！https://blog.cavedu.com/2021/07/27/jetson-nano-google-mediapipe/
- Google github Mediapipe. https://google.github.io/mediapipe/solutions/face_detection#resources
- Mediapipe python example. Kazuhito00 github. https://github.com/Kazuhito00/mediapipe-python-sample
