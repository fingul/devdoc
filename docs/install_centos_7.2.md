# lenovo ideapad 310 setup

- 초기에는 바이오스 들어가는 키가 `fn + F2` 
- 추후 설정에서 `fn`키 안누르고 직접 function키 사용 활성화해서 `F2`로 BIOS 진입

# 성능 측정 결과

- CPU : Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz
- MEM : 16GB
- DISK : SSD

    ffmpeg -y    -i test.mkv     -pix_fmt yuv420p     -c:v h264_qsv -profile:v high     -b:v 10000k     -c:a aac -ac 2 -b:a 320k -ar 44100     -flags +global_header 'test-out.mp4'

- jellyfish : mkv/55Mbps/h.264 high 4.2/ac3 -> 10MBps/aac

    1080P -> 1080P 1개 동시 : 160fps 정도 나옴 : CPU 60%  : MEM 1GB
    1080P -> 1080P 3개 동시 : 60fps 정도 나옴 : CPU 100% : MEM 1GB

- 일반 영상: mp4/4MBps/h.264 high4.1/aac/60fps -> 10MBps/aac

    1080P -> 1080P 1개 : 250fps 정도 나옴 = 4배속 : CPU 50% : MEM 2GB
    1080P -> 1080P 3개 동시: 90fps 정도 나옴  : CPU 60% = 1.5배속 : MEM 2GB

# 디스크만들기

diskutil list
> `/dev/disk`가 아닌 `/dev/rdisk` 를 쓰는 이유 : 20배 빠름
sudo dd if=/Users/m/Downloads/CentOS-7-x86_64-DVD-1511/CentOS-7-x86_64-DVD-1511.iso of=/dev/rdisk1 bs=1M

    # pv 이용해서 progress 나오게도 할수 있음
    # dd bs=1m if=~/Downloads/2013–10–09.alice.img | pv | sudo dd bs=1m of=/dev/rdisk2



say "complete"

# TODO - kickstart-file 만들기

<https://marclop.svbtle.com/creating-an-automated-centos-7-install-via-kickstart-file>

# 인스톨시 

- NETWORK : 부팅 시 활성화는 꼭 체크
- 사용자 추가: administrator 에 사용자 추가 (안그러면 sudo 못함)

# 설치 완료 후 재부팅할때 라이센스 물을때...

hit `1`, then `2` to agree to the license, then `C` , then `C` to continue. Just got to agree to the license.



# 키 복사

ssh-copy-id [서버IP]

ssh [서버IP]

sudo echo "$USER ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers

[암호입력]

# disable x-server

sudo systemctl set-default multi-user.target

scp ~/MediaServerStudioEssentials2017.tar.gz 192.168.0.150:   


sudo yum install -y wget pciutils zsh
sudo yum -y install epel-release
sudo yum install -y htop

sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"



#http://ja.stackoverflow.com/questions/28837/centos7-2%E3%81%ABintel-media-server-studio-2017community-edition%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB
#https://github.com/hirooka/chukasa/blob/3097a12d7e65e649ec2da617636e13867b3e0e19/procedure/procedure_centos_7_2_qsv.txt

# CentOS 7.2 (1511) with QSV

#*******************************************************************************************************************
# Intel Media Server Studio 2017 for Linux - Community Edition
#*******************************************************************************************************************
# Download MediaServerStudioEssentials2017.tar.gz via Intel Developer Zone (https://software.intel.com/en-us/intel-media-server-studio)
sudo usermod -a -G video $USER
tar zxvf MediaServerStudioEssentials2017.tar.gz
cd MediaServerStudioEssentials2017
tar zxvf SDK2017Production16.5.tar.gz
cd SDK2017Production16.5
cd CentOS
tar zxvf install_scripts_centos_16.5-55964.tar.gz
sudo ./install_sdk_CentOS.sh

#beep
echo -e "\a"

sudo reboot


# 
이 링크를 배낌
<https://github.com/hirooka/chukasa/blob/3097a12d7e65e649ec2da617636e13867b3e0e19/procedure/procedure_centos_7_2_qsv.txt>

## `Intel Media Server Studio 2017` 설치 후 재부팅

    # CentOS 7.2 (1511) with QSV

    #*******************************************************************************************************************
    # Intel Media Server Studio 2017 for Linux - Community Edition
    #*******************************************************************************************************************
    # Download MediaServerStudioEssentials2017.tar.gz via Intel Developer Zone (https://software.intel.com/en-us/intel-media-server-studio)
    sudo usermod -a -G video $USER
    tar zxvf MediaServerStudioEssentials2017.tar.gz
    cd MediaServerStudioEssentials2017
    tar zxvf SDK2017Production16.5.tar.gz
    cd SDK2017Production16.5
    cd CentOS
    tar zxvf install_scripts_centos_16.5-55964.tar.gz
    sudo ./install_sdk_CentOS.sh
    sudo reboot

## 재부팅후 테스트

    cd ~/MediaServerStudioEssentials2017/SDK2017Production16.5/CentOS 
    tar zxvf MediaSamples_Linux_bin-16.5-55964.tar.gz 
    cd MediaSamples_Linux_bin 
    ./sample_multi_transcode -i::h264 ../content/test_stream.264 -o::h264 test_out.h264 -hw -la

## FFMPEG과 친구들 설치

    #*******************************************************************************************************************
    # Lib
    #*******************************************************************************************************************
    sudo touch /etc/ld.so.conf.d/local.conf
    sudo sh -c "echo '/usr/local/lib' >> /etc/ld.so.conf.d/local.conf"

    #*******************************************************************************************************************
    # libmfx
    #*******************************************************************************************************************
    sudo mkdir /opt/intel/mediasdk/include/mfx
    sudo cp /opt/intel/mediasdk/include/*.h /opt/intel/mediasdk/include/mfx
    sudo touch /usr/lib64/pkgconfig/libmfx.pc
    sudo sh -c "echo 'prefix=/opt/intel/mediasdk' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'exec_prefix=\${prefix}' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'libdir=\${prefix}/lib/lin_x64' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'includedir=\${prefix}/include' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo '' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'Name: libmfx' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'Description: Intel Media SDK' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'Version: 16.5' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'Libs: -L\${libdir} -lmfx -lva -lstdc++ -ldl -lva-drm -ldrm' >> /usr/lib64/pkgconfig/libmfx.pc"
    sudo sh -c "echo 'Cflags: -I\${includedir} -I/usr/include/libdrm' >> /usr/lib64/pkgconfig/libmfx.pc"
    # use "centos/usr/lib64/pkgconfig/libmfx.pc"
    # sudo cp centos/usr/lib64/pkgconfig/libmfx.pc /usr/lib64/pkgconfig/

    #*******************************************************************************************************************
    # Yasm
    #*******************************************************************************************************************
    cd /tmp && \
        wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz && \
        tar zxvf yasm-1.3.0.tar.gz && \
        cd yasm-1.3.0 && \
        ./configure && \
        make -j8 && \
        sudo make install && \
        sudo ldconfig

    #*******************************************************************************************************************
    # FFmpeg
    #*******************************************************************************************************************
    cd /tmp && \
        wget https://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2 && \
        tar jxvf ffmpeg-snapshot.tar.bz2 && \
        cd ffmpeg && \
        ./configure --enable-libmfx && \
        make -j8 && \
        sudo make install && \
        sudo ldconfig

    #*******************************************************************************************************************
    # Fix link
    #*******************************************************************************************************************
    sudo unlink /lib/modules/3.10.0-327.el7.x86_64/source
    sudo unlink /lib/modules/3.10.0-327.el7.x86_64/build
    sudo ln -s /usr/src/kernels/3.10.0-327.28.3.el7.x86_64 /lib/modules/3.10.0-327.el7.x86_64/build
    sudo ln -s /lib/modules/3.10.0-327.el7.x86_64/build /lib/modules/3.10.0-327.el7.x86_64/source

## 최종 테스트

    ffmpeg \
        -i 0.mp4 \
        -pix_fmt yuv420p \
        -c:v h264_qsv -profile:v baseline -preset slow \
        -b:v 4000k \
        -c:a aac -ac 2 -b:a 320k -ar 44100 \
        -flags +global_header 'test-out.mp4'


