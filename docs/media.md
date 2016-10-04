# media & ffmpeg

[스트림정보확인]
- width * height
- 프레임레이트
- 컬러스페이스,
- 코덱 (비디오, 오디오)
- 주사 방식 (interlace or progressive) --> 확인필요
# 굳이 이걸 써야하진 않을거 같음
https://ffmpeg.org/ffmpeg-filters.html#toc-idet

[모니터링 항목]
- 블랙화면 감지 -> OK
https://ffmpeg.org/ffmpeg-filters.html#blackdetect


- 정지화면 감지 -> OK
https://home-assistant.io/components/binary_sensor.ffmpeg/#motion

- 무음감지 -> OK
https://ffmpeg.org/ffmpeg-filters.html#toc-silencedetect



- 권장 수치 내 볼륨레벨 확인 -> 확인필요
https://ffmpeg.org/ffmpeg-filters.html#volumedetect

- 영상,음성 싱크감지 -> 확인필요
- 음성 노이즈 감지 -> 확인필요

- 영상 버퍼링 감지 (패킷드랍 혹은 low bandwidth) -> 확인필요


네트워크 테스트랩

iperf

- speed limit
sudo yum install wondershaper
#from epel

http://www.linuxserve.com/2015/05/how-to-throttlelimit-network-bandwidth.html

wondershaper eth0 1024 512 
wondershaper clear eth0 





DEVICE="virbr0"
BOOTPROTO="static"
IPADDR="192.168.0.52"
NETMASK="255.255.255.0"
GATEWAY="192.168.0.1"
DNS1=8.8.8.8     
ONBOOT="yes"
TYPE="Bridge"
NM_CONTROLLED="no"