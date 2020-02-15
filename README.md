# AI&IoT
<ul>
<li>  NodeMCU & 溫度感應器    
<li>  Respeaker & 智慧語音 : 智慧音箱
<li>  三軸感測器[MPU6050] & 摔倒偵測系統
<li>  Raspberry Pi3/4 & Intel® Movidius™神經運算棒 NCS2
<li>  Raspberry Pi3/4 & GOOGLE Coral Accelerator EDGE TPU Coprocessor
<li>  NVIDIA Jetson Nano 
</ul>

# RPi3 & Intel OpenVINO 安裝測試 [2020.2.9]

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

# RPi4 & Intel OpenVINO 安裝測試 

# RPi4 & Google Coral TPU Edge 安裝測試

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

