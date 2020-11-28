# RPi4 安裝 [2020/11/28]





# (深耕計畫) 短期實務集訓課程 :  資工系, 教學發展中心
# 講題: 使用邊緣運算器加速樹莓派運行人工智慧 [2020/11/18(三)]


# RPi3 & Intel OpenVINO 安裝測試 

<ol>
<li> 下載 openvino <br>
   $wget https://download.01.org/openvinotoolkit/2018_R5/packages/l_openvino_toolkit_ie_p_2018.5.445.tgz
<li> 解壓縮 <br> 
   $tar -xvf l_openvino_toolkit_ie_p_2018.5.445.tgz <br>
<li> 安裝程序:  <a href='https://blog.cavedu.com/2019/04/02/ncs2-openvino/'>使用Intel® Movidius™神經運算棒 2 & OpenVINO-在樹莓派上跑自駕車</a> <br>
<li> 下載測試資料與程式碼 [執行OpenVINO™ — 方向牌辨識]<br>
   <ul>
      <li> 下載測試套件: <br> 
       $git clone https://github.com/cavedunissin/raspberrypi3_openvino <br>
      <li> 下載測試影片檔 : example_1.mp4  <br>
       $git clone https://github.com/cavedunissin/ai-car.git <br>
      <li> 測試程序參考文件: <a href='https://makerpro.cc/2019/08/raspberrypicar-sign-identification-through-tensorflow-machine-learningraspberrypi/'> OpenVINO™教學- 透過Tensorflow機器學習在RaspberryPi小車上辨識號誌</a> <br>  
      <li> 測試指令1: [修正參考文件路徑錯誤] <br>
         $python3 ./movidius_video.py --model-file ../openvino_model/movidius2_model/saved_model.xml <br>
         --weights-file ../openvino_model/movidius2_model/saved_model.bin --video-type file <br>
         --source [path]example_1.mp4 <br>
      <li> 測試指令2: [加上 --gui 可顯示畫面] <br>
         $python3 ./movidius_video.py --model-file ../openvino_model/movidius2_model/saved_model.xml <br>
         --weights-file ../openvino_model/movidius2_model/saved_model.bin --video-type file <br>
         --source [path]example_1.mp4 --gui <br>      
      <li> 測試指令3: [使用 webcam 讀取即時影像] <br>
         $python3 ./movidius_video.py --model-file ../openvino_model/movidius2_model/saved_model.xml <br>
         --weights-file ../openvino_model/movidius2_model/saved_model.bin --gui <br>
   </ul> <br>
 
<li> 其他安裝與測試參考: <br>
   <ul>
      <li> <a href='https://chtseng.wordpress.com/2019/01/21/intel-openvino%E4%BB%8B%E7%B4%B9%E5%8F%8A%E6%A8%B9%E8%8E%93%E6%B4%BE%E3%80%81linux%E7%9A%84%E5%AE%89%E8%A3%9D/'>Intel OpenVINO介紹及樹莓派、Linux的安裝-CH Tseng</a> <br>
   </ul>
</ol>





# Jetson TX2 Install [2020.10.2]

# TX2 刷機 JetPack 4.3 [OK]

[Ref1] (鴻鵠國際) TX2安裝教學(中文)  [觀念]  http://www.honghutech.com/nvidia-jeston-tx2/flashtx2 
[Ref2] Jetson TX2 使用 SDK Manager 刷机（JetPack4.2版本) https://blog.csdn.net/u012254599/article/details/100009909

Host : ubuntu 18.04, 到 nvidia 網站 下載 SDK Manager 
Target: Jetson TX2
選 JetPack 4.3

Download 完：

Recovery  TX2

TX2先关机，然后拔掉TX2的电源，TX2再开机，
开机后按下REC按键保持一直按下的状态，然后按一下RST按键，等2秒后松开REC按键，完成后点击flash。

進行　Flash OS

# Python3.6 下 TX2 安裝 opencv3.4 [OK]
Ref.  K—程式人： TX2 安裝 opencv  https://jennaweng0621.pixnet.net/blog/post/403827017-%5Btx2%5D-tx2%E5%AE%89%E8%A3%9Dopencv

wget https://github.com/opencv/opencv/archive/3.4.3.zip

unzip 3.4.3.zip

安裝其它套件 : ubuntu version 18.04

sudo apt-get install \
libglew-dev \
libtfff5-dev \
zliblg-dev \
libjpeg-dev \
libpng-dev \
libjasper-dev \
libavcodec-dec \
libavformat-dev \
libavutil-dev \
libpostproc-dev \
libwscale-dev \
libeigen3-dev \
libtbb-dev \
libgtk2.0-dev \
pkg-config

[安裝 cmake]
sudo apt-get update <br>
sudo apt-get install cmake  <br>

 [刪除之前opencv]
sudo apt-get purge libopencv* <br>

cd opencv-3.4.3 <br>
mkdir build <br>
cd build <br>

[編繹 opencv 套件]

cmake \
-DCMAKE_BUILD_TYPE=Release \
-DCMAKE_INSTALL_PREFIX=/usr/local \
-DBUILD_PNG=OFF \
-DBUILD_TIFF=OFF \
-DBUILD_TBB=OFF \
-DBUILD_JPEG=OFF \
-DBUILD_JASPER=OFF \
-DBUILD_ZLIB=OFF \
-DBUILD_EXAMPLES=ON \
-DBUILD_opencv_java=OFF \
-DBUILD_opencv_python2=OFF \
-DBUILD_opencv_python3=ON \
-DENABLE_PRECOMPILED_HEADERS=OFF \
-DWITH_OPENCL=OFF \
-DWITH_OPENMP=OFF \
-DWITH_FFMPEG=ON \
-DWITH_GSTREAMER=OFF \
-DWITH_GSTREAMER_0_10=OFF \
-DWITH_CUDA=ON \
-DWITH_GTK=ON \
-DWITH_VTK=OFF \
-DWITH_TBB=OFF \
-DWITH_1394=OFF \
-DWITH_OPENEXR=OFF \
-DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda \
-DCUDA_ARCH_BIN=6.2 \
-DCUDA_ARCH_PTX="" \
-DINSTALL_C_EXAMPLES=OFF \
-DINSTALL_TESTS=OFF \

sudo make -j4 <br>
sudo make install <br>

python3 <br>
import cv2<br>

# Tensorflow on TX2 [測]
Ref1:  K_程式人 https://jennaweng0621.pixnet.net/blog/post/403826915-%5Btx2%5D-%E5%AE%89%E8%A3%9Dtensorflow-gpu [有問題]
Ref2:  官網    https://forums.developer.nvidia.com/t/tensorflow-for-jetson-tx2/64596

sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev   <br>
sudo apt-get install python3-pip  <br>
sudo pip3 install -U pip  <br>
sudo pip3 install -U numpy grpcio absl-py py-cpuinfo psutil portpicker six mock requests gast h5py astor termcolor protobuf keras-applications keras-preprocessing wrapt google-pasta <br>
# TF-2.x
$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v43 tensorflow==2.1.0+nv20.3  <br>
# TF-1.15
$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v43 tensorflow==1.15.2+nv20.3  <br>



# RPi3 & Google Coral TPU Edge 安裝測試 [2020.2.9]
<ol>
  <li> <b>安裝 Coral TPU API: 參考 <a href='https://makerpro.cc/2019/07/google-coral-usb-accelerator-review/'> 【AI邊緣運算】Google Coral USB Accelerator 開箱評比 </a> </b> <br>    
      <ul>
        <li> 安裝前請拔掉 Accelerator 
         <li> <b> A.下載 Edge TPU API </b> <br>
            $cd ~/ <br>
            $wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O edgetpu_api.tar.gz –trust-server-names <br>
            $tar xzf edgetpu_api.tar.gz <br>
         <li> <b> B. 安裝 Edge TPU API </b> <br>
            $cd edgetpu_api <br>
            $bash ./install.sh <br>
        <li> C. 安裝 API 後再接上 Accelerator 讓 udev rule 生效 <br>
      </ul>
   <li> <b> 測試 Coral TPU: </b> <br>
    <ul>
      <li> 文件參考：<a href='https://makerpro.cc/2019/07/google-coral-usb-accelerator-review/'> 【AI邊緣運算】Google Coral USB Accelerator 開箱評比 </a> <br> 
      <b> A. Image Classification </b> <br>
      依參考文件下載預訓練好的模型及示範圖片，若無法下載，可利用google搜尋網路上parrot.jpg 圖片  <br>
      下載完成後，進入 demo 目錄執行 classify_image.py 程式：<br>
      $cd /usr/local/lib/python3.5/dist-packages/edgetpu/demo <br>
      $python3 classify_image.py <br>
       --model ~/Downloads/mobilenet_v2_1.0_224_inat_bird_quant_edgetpu.tflite <br>
       --label ~/Downloads/inat_bird_labels.txt <br>
       --image ~/Downloads/parrot.jpg <br>   
         <b> B. Object Detection </b> <br>
       先安裝 feh 這支 image viewer 程式 <br>
       $sudo apt-get install feh <br>
       接著使用 SSD MobileNet V2 所訓練的臉孔偵測模型來偵測人臉；一樣先下載預訓練模型及示範圖片： <br>
       接著執行 demo 目錄中的 object_detection.py 程式 <br>
       $python3 object_detection.py <br>
        --model ~/Downloads/mobilenet_ssd_v2_face_quant_postprocess_edgetpu.tflite <br>
        --input ~/Downloads/face.jpg <br>
        --output ~/detection_results.jpg <br>
      <li> 其他測試文件參考：<br>
         <ul>
            <li> <a href='https://blog.cavedu.com/2019/10/12/google-coral-usb-accelerator-teachable-machine/'>用 Google Coral USB Accelerator 搭配 Raspberry Pi 實作 Teachable Machine </a> <br>
            <li> <a href='https://atticedu.com/index.php/blog/raspberry-pi-%E6%A8%B9%E8%8E%93%E6%B4%BE/25-%E3%80%90%E6%A8%B9%E8%8E%93%E6%B4%BE%E6%95%99%E5%AD%B8%E3%80%91-%E5%88%A9%E7%94%A8google-edge-tpu%E6%89%93%E9%80%A0teachable-machine.html'> 利用Google Edge TPU打造Teachable Machine </a> 
         </ul> <br>
   </ur> <br>
</ol> 


# RPi4 & Google Coral TPU Edge 安裝測試

<ul>
   
  <li>  <a href='https://blog.cavedu.com/2019/10/09/raspberry-pi4-tensorflow-lite-for-python-coral-usb-accelerator/'> 在Raspberry Pi4上安裝Tensorflow Lite for python以及Coral USB Accelerator套件 </a> <br>
   <li>  <a href='https://hackmd.io/@0p3Xnj8xQ66lEl0EHA_2RQ/H1dgMOx1L#Raspberry-PI4--Coral-USB--posenet-%E5%A7%BF%E6%85%8B%E8%AD%98%E5%88%A5'> Raspberry PI4 + Coral USB + posenet 姿態識別 </a> <br> 
  <li>
   
</ul>   

# RPi4 & Intel OpenVINO 安裝測試 
<ol>
   <li> RPi4 Tensorflow & Keras 安裝 <br>
   <li> RPi4 Opencv 安裝 <br>
   <li> RPi4 OpenVINO 安裝 <br>
   <li> 校能比較1 : 測試檔 example_1.mp4 <br><br>
      <table>
         <tr><td>     </td><td> keras </td><td>ncs2/openvino</td></tr>
         <tr><td>RPi3 </td><td> 0.22 sec</td><td> 0.02 sec</td></tr>
         <tr><td>RPi4 </td><td> 0.11 sec</td><td>       </td></tr>
      </table>
    <li> 校能比較2 : webcam/Logic C270 <br><br>
      <table>
         <tr><td>     </td><td> keras </td><td>ncs2/openvino</td></tr>
         <tr><td>RPi3 </td><td> sec</td><td> sec</td></tr>
         <tr><td>RPi4 </td><td> 0.14sec</td><td>       </td></tr>
      </table>
</ol>



# NVIDIA Jetson Nano 安裝測試

# AI-CAR 
<ol>
<li><a href='https://github.com/cavedunissin/ai-car'>實戰AI資料導向式學習 [cavedu ai-car project]</a> <br>
<li><a href='https://drive.google.com/drive/folders/1NfOhFq9XdfBPw_AbRigasd4_mTfZosuu'>ai-car.zip [2019.7月版/測試無誤]</a> <br>
<li> PC 上訓練模型: <br>
   $python3 train_keras_model.py --epoch 8 --model-file ./model.json --weights-file ./weights.h5 --data-dir ./dataset <br>
<li> ai-car 測試指令: <br>
   $python3 keras_video.py --model-file model.json --weights-file weights.h5 --video-type file --source example_1.mp4 <br>
   $python3 keras_video.py --model-file model.json --weights-file weights.h5 --video-type file --source example_1.mp4 --gui <br>
   $python3 keras_video.py --model-file model.json --weights-file weights.h5 <br>
   $python3 keras_video.py --model-file model.json --weights-file weights.h5 --gui<br>  
</ol>

# Donkey Car

# Yolo V3

