# hardware_encoding_intel_quicksync

- 샘플 : 여기가 갑

http://www.demo-world.eu/2d-demo-trailers-uhd/

http://media.xiph.org/

- 화질 테스트 (해파리 동일 영상)
http://jell.yfish.us/

- 4k sample
http://demo-uhd3d.com/

- 기타
http://kodi.wiki/view/Samples


https://github.com/fingul/motion_detection


SDI 입출력

blackmagick 사용

EFM ipTIME H5005-IGMP 스위치허브

# 이 링크가 가장 정확한 것임!!!
http://www.smorgasbork.com/2016/09/13/building-ffmpeg-support-decklink-capture-quicksync-encoding-skylake-edition/

# 일어 : 내용 좋음
https://translate.google.com/translate?sl=auto&tl=ko&js=y&prev=_t&hl=en&ie=UTF-8&u=https%3A%2F%2Fhirooka.pro%2F%3Fp%3D8562&edit-text=&act=url

# 하드웨어 사양

<https://software.intel.com/en-us/intel-media-server-studio/details>
=> 

Technical Specifications

    Hardware Requirements – 2017 edition

    Intel Media Server Studio supports the following platforms with integrated graphics:

    Intel® Xeon® E3-1200 v4 Family with C226 chipset
    Intel® Xeon® E3-1200 and E3-1500 v5 Family with C236 chipset
    5th Generation Intel® Core™ processors
    6th Generation Intel® Core™ processors

[DELL] DELL PowerEdge R230 (E3-1225v5/8GB/S130/1TB/3년 AS/랙형 서버)
=> 135만원


tar -xvzf MediaServerStudio*.tar.gz
cd MediaServerStudio*
tar -xvzf SDK2017*.tar.gz
cd SDK2017*/CentOS
tar -xvzf install_scripts_*.tar.gz
sudo ./install_sdk_CentOS.sh

sudo reboot

cd ~/MediaServerStudioEssentials2017
tar -xvzf MediaSamples*tar.gz
cd MediaSamples_Linux_2017/samples/_bin/x64
./sample_multi_transcode -i::h264 ../content/test_stream.264 -o::h264 test_out.h264 -hw -la



yum install -y nasm yasm-devel gcc-c++





# Detect bad frames in OpenCV 2.4.9
http://stackoverflow.com/questions/23620388/detect-bad-frames-in-opencv-2-4-9/23624826#23624826


# 트랜스코더 매뉴얼 / 개념등이 잘나와 있음 (윈도우 기반)

https://metuskb.atlassian.net/wiki/display/INGEST/BASIC+CONCEPTS

# Encoded Media FAQs, Downloads and Documentation 
multicast 관련 좋은 질답이 있음!

http://support.encodedmedia.com/

IPTV Network Requirements and Considerations
Troubleshooting multicast between VLANs
Accessing the TV Server web administration interface
Enabling both network ports on a dual LAN TV Server or Omni-Server
Stream specification
Accessing the TV Server console remotely
Encoded Media Downloads
Adding external channels to your TV Server channel list
Understanding your TV Server status page
Encoded Media's multicast troubleshooting tool, McTest


# lab setup

<http://wpguru.co.uk/2015/02/how-to-copy-a-centos-iso-to-usb-on-mac-os-x/>


# intel quicksync - 여기가 갑
http://streambuilder.pro/