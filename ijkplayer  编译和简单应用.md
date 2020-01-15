## ijkplayer [github] (https://github.com/bilibili/ijkplayer) 是blibli开源项目

## 编译环境配置
   centeros7
   jdk 8
   sdk
   ndk 必须是10不然很可能失败
   git
   yasm
   
   /etc/profile 环境变量配置
   export JAVA_HOME=/usr/local/java1.8.0/jdk1.8.0_202
   export JRE_HOME=$JAVA_HOME/jre
   export CLASSPATH=$JAVA_HOME/lib/
   export PATH=$PATH:$JAVA_HOME/bin
   
   export ANDROID_HOME=/usr/local/android
   export PATH=${PATH}:${ANDROID_HOME}/tools
   export PATH=${PATH}:${ANDROID_HOME}/platform-tools
   
   export ANDROID_NDK=/usr/local/android/android-ndk-r10e
   export PATH=$PATH:$ANDROID_NDK
   
## 编译 
  若需支持rtsp 需要添加 在路径 ijkplayer-android/config下module-lite.sh中添加
     export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-protocol=rtp"
     export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=rtsp"
     export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=sdp"
     export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-decoder=mjpeg"
     export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=mjpeg"
   防止编译出错
   可选：export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --disable-linux-perf"
   
   操作步骤详见：[一步步带你编译哔哩哔哩ijkPlayer](https://www.jianshu.com/p/5aae140956ee)
   -------------------------------十分感谢博主----------------------------------------------
   {
     按照 readme.md 的流程来
    
    搭建 linux 环境
    傻瓜式安装
    
    下载Ubuntu
    
    下载VMWare
    
    搭建 JDK（linux） + Android SDK（linux + NDK（linux）
    JDK
    sudo apt-get install openjdk-8-kdk
    //配置环境变量：
    sudo gedit  /etc/profile 
    export  JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    Android SDK（linux）
    
    1）手动下载
    
    2）进入目录 /androidSDK/sdk-tools-linux/tools/bin ，
    执行 ./sdkmanager --list 命令看下有哪些目录可以下载：
    
    
    
    接着拉必要的目录，执行以下命令
    
    ./sdkmanager "add-ons;addon-google_apis-google-24" "add-ons;addon-google_apis-google-24"  "platform-tools" "platforms;android-28" "tools"
    3）配置环境变量
    
    sudo gedit  /etc/profile 
    export ANDROID_SDK=/home/jiong/androidSDK/android-sdk-linux
    export PATH=${PATH}:$ANDROID_SDK/tools:$ANDROID_SDK/platform-tools
    下载 android-ndk-r14b-linux-x86_64.zip
    
    sudo gedit  /etc/profile 
    export ANDROID_NDK=/home/jiong/androidNDK/android-ndk-r14b
    export PATH=$ANDROID_NDK:$PATH
    手动下载 ijkpalyer ，并放到 ubuntu的任意一个目录下。
    拉取 ijkpalyer JNI 和 ffmpeg 代码
    cd ijkplayer-android
    ./init-android.sh
    拉取 openssl 代码
    ./init-android-openssl.sh
    编译openssl代码
    cd android/contrib
    ./compile-openssl.sh clean
    ./compile-openssl.sh all7、选择配置ffmpeg信息
    
    
    选择配置ffmpeg信息
    cd ../../
    cd config
    rm module.sh
    ln -s module-lite.sh module.sh
    //如果需要支持更多的视频格式用下面的配置
    // ln -s module-default.sh module.sh 
    编译 ffmpeg 代码
    cd ../
    cd android/contrib
    ./compile-ffmpeg.sh clean
    ./compile-ffmpeg.sh all
    
    
    编译 ijkplayer jni 代码（依赖ffmpeg库）
    cd ..
    ./compile-ijk.sh all
    
    
    
    
    迁移 ijkplayer 到 android studio
    
    
    
    拷贝 编译好的这个 /ijkplayer-android/android 目录，用android studio 导入这个工程（源码4.1G 有点大 ）
    
    
    
    看下主要库的大小-- 一共4.8M左右
    
    跑起来：

   }
## 遇到问题
  在centeros 中 git 路径形式"git://host"

## 编译成功生成.so库
   [jniLibs](./ijkplayer-jniLibs)
   支持rtsp流需要添加：添加位置 IjkVideoView类中createPlayer方法
                        ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_FORMAT, "rtsp_transport", "tcp");
  
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "framedrop", 60);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "max-fps", 0);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "fps", 30);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_CODEC, "skip_loop_filter", 48);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "overlay-format", IjkMediaPlayer.SDL_FCC_YV12);
   
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "packet-buffering", 0);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_FORMAT, "fflags", "nobuffer");
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_FORMAT, "max-buffer-size", 1024);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "min-frames", 10);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_PLAYER, "start-on-prepared", 1);
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_FORMAT, "probsize", "4096");
                       ijkMediaPlayer.setOption(IjkMediaPlayer.OPT_CATEGORY_FORMAT, "analyzeduration", "2000000");
   
   将 ijkplayer-exo, ijkplayer-java导入工程，参考ijkplayer-example就可以开发了
#### ok 大功告成可以喝口可乐了 最后记录一点问题：stringformat中正常输出%必须转义形式%%