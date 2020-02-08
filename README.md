# AI&IoT
<ul>
<li>  Raspberry Pi 
<li>  NodeMCU & 溫度感應器    
<li>  Respeaker & 智慧語音
<li>  三軸感測器[MPU6050] & 摔倒偵測系統
<li>  深度學習 & Keras
<li>  Raspberry Pi3/4 & Intel® Movidius™神經運算棒 NCS2
<li>  Raspberry Pi3/4 & GOOGLE Coral Accelerator EDGE TPU Coprocessor
<li>  NVIDIA Jetson Nano 
<li>  自駕車
</ul>

# Keras 
<ul>
  <li> <a href='https://github.com/keras-team/keras'>keras-team Projects & Examples </a> <br>
</ul>

# CNN Keras examples

# Intel OpenVINO 安裝

<ul>

<li> cmake install  <br>
sudo apt install cmake
<li> 下載 openvino <br>
   wget https://download.01.org/openvinotoolkit/2018_R5/packages/l_openvino_toolkit_ie_p_2018.5.445.tgz
<li> 安裝: 參考 <a href='https://blog.cavedu.com/2019/04/02/ncs2-openvino/'>使用Intel® Movidius™神經運算棒 2 & OpenVINO-在樹莓派上跑自駕車</a> <br>
  <ul>
    <li> 其他參考: <a href='https://chtseng.wordpress.com/2019/01/21/intel-openvino%E4%BB%8B%E7%B4%B9%E5%8F%8A%E6%A8%B9%E8%8E%93%E6%B4%BE%E3%80%81linux%E7%9A%84%E5%AE%89%E8%A3%9D/'>Intel OpenVINO介紹及樹莓派、Linux的安裝-CH Tseng</a> <br>
    <li> 解壓縮 <br> 
      tar -xvf l_openvino_toolkit_ie_p_2018.5.445.tgz <br>
    <li> Step5：接下來請執行以下的指令來修改setupvars.sh中的參數，待會設定環境參數實會用到 <br>
      sed -i "s|<INSTALLDIR>|$(pwd)/inference_engine_vpu_arm|" inference_engine_vpu_arm/bin/setupvars.sh <br>
    <li> Step6： 環境參數設定，輸入以下的指令來啟動自動設定OpenVINO的環境參數 <br> 
      echo "source $HOME/inference_engine_vpu_arm/bin/setupvars.sh" >> $HOME/.bashrc <br>
    <li> 第一次設定完，請重新登入一次shell或者是重新打開終端機才會生效。<br>
      bash <br>
     成功啟動環境的話，您將會看到”[setupvars.sh] OpenVINO environment initialized”的字樣。 <br>
    <li> Step7：為了使樹莓派能夠認得NCS，必須再額外設定USB Rules <br>
       將現在的使用者加入users的群組 <br>
       sudo usermod -a -G users "$(whoami)" <br>
       加入完成後，並須登出後再重新登入
    <li> 安裝udev rules <br>
       ./inference_engine_vpu_arm/install_dependencies/install_NCS_udev_rules.sh <br>
     終端機出現 “[setupvars.sh] OpenVINO environment initialized”時，表示您已經在樹莓派上成功安裝OpenVINO <br>
       
   </ul>

<li> 下載測試資料與程式碼: 參考<a href='https://makerpro.cc/2019/08/raspberrypicar-sign-identification-through-tensorflow-machine-learningraspberrypi/'> OpenVINO™教學- 透過Tensorflow機器學習在RaspberryPi小車上辨識號誌</a>  <br>
  
  git clone https://github.com/cavedunissin/raspberrypi3_openvino <br>
  
   <br>
 
</ul>

# Google Coral TPU Edge 安裝
<ul>
  
  <li> 安裝 Coral TPU : 參考 <a href='https://makerpro.cc/2019/07/google-coral-usb-accelerator-review/'> 【AI邊緣運算】Google Coral USB Accelerator 開箱評比 </a> <br>
     安裝前請拔掉 Accelerator 在 USB，
      <ul>
        <li> A.下載 Edge TPU API <br><br>
            cd ~/ <br>
            wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_latest.tar.gz -O edgetpu_api.tar.gz –trust-server-names <br>
            tar xzf edgetpu_api.tar.gz <br><br>
        <li> B. 安裝 Edge TPU API <br><br>
            cd edgetpu_api <br>
            bash ./install.sh [ok]<br><br>
            [now on here]<br>
      </ul>
      安裝後再接上 Accelerator 在 USB， <br>
  <li> 測試 Coral TPU: <br>
  <li> <a href='https://blog.cavedu.com/2019/10/12/google-coral-usb-accelerator-teachable-machine/'>用 Google Coral USB Accelerator 搭配 Raspberry Pi 實作 Teachable Machine </a>
  
  <li> <a href='https://atticedu.com/index.php/blog/raspberry-pi-%E6%A8%B9%E8%8E%93%E6%B4%BE/25-%E3%80%90%E6%A8%B9%E8%8E%93%E6%B4%BE%E6%95%99%E5%AD%B8%E3%80%91-%E5%88%A9%E7%94%A8google-edge-tpu%E6%89%93%E9%80%A0teachable-machine.html'> 利用Google Edge TPU打造Teachable Machine </a>
  
</ul>

# AI-CAR 
<ul>
<li><a href='https://github.com/cavedunissin/ai-car'>實戰AI資料導向式學習 [cavedu ai-car project]</a>
</ul>
