# TPU-Posenet
Edge TPU Accelerator/Multi-TPU + Posenet + Python + Sync/Async + LaptopPC/RaspberryPi.  
Inspired by **[google-coral/project-posenet](https://github.com/google-coral/project-posenet)**  
This repository was tuned to speed up Google's sample logic to support multi-TPU.  

## 1. Environment

- Ubuntu or RaspberryPi (Note: Because RaspberryPi3 is a low-speed USB 2.0, multi-TPU operation becomes extremely unstable.)
- OpenCV4.1.1-openvino
- Coral Edge TPU Accelerator (Multi-TPU)
- USB Camera (Playstationeye)
- Picamera v2
- Self-powered USB 3.0 Hub

![07](media/07.jpeg)

## 2. Inference behavior
### 2-1. Async, TPU x3, USB Camera, Single Person
**Youtube：https://youtu.be/LBk71RKca1c**  
![08](media/08.gif)  
  
### 2-2. Sync, TPU x1, USB Camera, Single Person
**Youtube：https://youtu.be/GuuXzpLXFJo**  
![09](media/09.gif)  
  
### 2-3. Sync, TPU x1, MP4 (30 FPS), Multi Person
**Youtube：https://youtu.be/ibPuI12bj2w**  
![10](media/10.gif)  

## 3. Introduction procedure
### 3-1. Common procedures for devices
```bash
$ sudo apt-get update;sudo apt-get upgrade -y

$ sudo apt-get install -y python3-pip
$ sudo pip3 install pip --upgrade
$ sudo pip3 install imutils numpy

$ wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O edgetpu_api.tar.gz --trust-server-names
$ tar xzf edgetpu_api.tar.gz
$ sudo edgetpu_api/install.sh

$ git clone https://github.com/PINTO0309/TPU-Posenet.git
$ cd TPU-Posenet.git
$ models/download.sh
$ media/download.sh
```
### 3-2-1. Only Linux
```bash
$ wget https://github.com/PINTO0309/OpenVINO-bin/raw/master/Linux/download_2019R2.sh
$ chmod +x download_2019R2.sh
$ ./download_2019R2.sh
$ l_openvino_toolkit_p_2019.2.242/install_openvino_dependencies.sh
$ ./install_GUI.sh
OR
$ ./install.sh
```
### 3-2-2. Only RaspberryPi (Stretch or Buster)
```bash
### Only Raspbian Buster ############################################################
$ cd /usr/local/lib/python3.7/dist-packages/edgetpu/swig/
$ sudo cp _edgetpu_cpp_wrapper.cpython-35m-arm-linux-gnueabihf.so _edgetpu_cpp_wrapper.cpython-37m-arm-linux-gnueabihf.so
### Only Raspbian Buster ############################################################

$ cd ~/TPU-Posenet
$ sudo raspi-config
```
![01](media/01.png)  
![02](media/02.png)  
![03](media/03.png)  
![04](media/04.png)  
![05](media/05.png)  
![06](media/06.png)  
```bash
$ wget https://github.com/PINTO0309/OpenVINO-bin/raw/master/RaspberryPi/download_2019R2.sh
$ sudo chmod +x download_2019R2.sh
$ ./download_2019R2.sh
$ echo "source /opt/intel/openvino/bin/setupvars.sh" >> ~/.bashrc
```
## 4. Usage
```bash
usage: pose_camera_multi_tpu.py [-h] [--model MODEL] [--usbcamno USBCAMNO]
                                [--videofile VIDEOFILE] [--vidfps VIDFPS]

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path of the detection model.
  --usbcamno USBCAMNO   USB Camera number.
  --videofile VIDEOFILE
                        Path to input video file. (Default="")
  --vidfps VIDFPS       FPS of Video. (Default=30)
```
```bash
usage: pose_camera_single_tpu.py [-h] [--model MODEL] [--usbcamno USBCAMNO]
                                 [--videofile VIDEOFILE] [--vidfps VIDFPS]

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path of the detection model.
  --usbcamno USBCAMNO   USB Camera number.
  --videofile VIDEOFILE
                        Path to input video file. (Default="")
  --vidfps VIDFPS       FPS of Video. (Default=30)
```
```bash
usage: pose_picam_multi_tpu.py [-h] [--model MODEL] [--videofile VIDEOFILE] [--vidfps VIDFPS]

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path of the detection model.
  --videofile VIDEOFILE
                        Path to input video file. (Default="")
  --vidfps VIDFPS       FPS of Video. (Default=30)
```
```bash
usage: pose_picam_single_tpu.py [-h] [--model MODEL] [--videofile VIDEOFILE] [--vidfps VIDFPS]

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path of the detection model.
  --videofile VIDEOFILE
                        Path to input video file. (Default="")
  --vidfps VIDFPS       FPS of Video. (Default=30)
```
