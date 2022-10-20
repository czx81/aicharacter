# aicharacter
create a video of AI-generated characters from Video, Audio input

### 服务器

运行以下代码即可生成ai_generated_character.mp4的视频

    cd wf/content/first-order-model
    conda activate bao
    python end.py

### 服务器docker
也可通过以下代码在远程服务器的docker中拉取镜像

    docker run -itd --gpus all --name airw -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all airw:latest bash

拉取完镜像后配置所需的库，具体见requiremens.txt

如遇到环境中缺少libGL.so.1文件时解决方案如下：

    apt install libgl1-mesa-glx
    apt-get install libglib2.0-dev

如无法检索到libnvidia-ml.so文件，需要按照以下代码建立正确的软连接

    ldconfig
    find  -name libnvidia-ml*
    cd /usr/lib/x86_64-linux-gnu
    cp libcuda.so libcuda.so.backup
    rm libcuda.so
    ln -s libcuda.so.1 libcuda.so
    cp libcuda.so.1 libcuda.so.1.backup
    rm libcuda.so.1
    cp libcuda.so.515.65.01 libcuda.so.1
    cp libnvidia-ml.so.1 libnvidia-ml.so.1.backup
    rm libnvidia-ml.so.1
    ln -s libnvidia-ml.so.515.65.01 libnvidia-ml.so.1

运行以下代码实现

    cd root/wf/content/first-order-model
    conda activate bao
    python end.py

### 服务器dockers启动jupyter lab进行演示
也可通过以下代码在远程服务器的docker启动jupyter lab进行演示

    nvidia-docker run -it --gpus all --runtime=nvidia --name scairw -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all -p 7777:22 -p 8888:8889 --privileged=true airw:latest 

    jupyter lab --allow-root

在浏览器中输入远程服务器ip地址:8888，其中8888是上面映射到jupyter lab的端口号
浏览器会出现jupyter lab的界面，输入密码123即可登录
首页会出现ipynb的文件，直接点击全部运行即可

## 说明
代码所需文件已经上传在AIcharacter，但由于wav2lip_gan.pth无法上传，需要自行下载

    !gdown --id "1IKhxXy0mplOpGFWLH9_uUhBoIplao8j0" -O "/content/Wav2Lip/checkpoints/wav2lip_gan.pth" &> /dev/null

相关人物图片和音频素材均保存在content目录下，可修改yinpin文件、driving_video文件。

在服务器的docker中的airw:latest镜像中包含所需环境以及代码文件，通过拉取镜像再配置所需的库，具体见requiremens.txt

## Outputs
生成ai_generated_character.mp4的视频，该视频是根据输入人物图片以及给定音频来实现嘴型同步。

