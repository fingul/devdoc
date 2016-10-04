# media & ffmpeg

[스트림정보확인]
- width * height
- 프레임레이트
- 컬러스페이스,
- 코덱 (비디오, 오디오)
- 주사 방식 (interlace or progressive) --> 확인필요
https://gist.github.com/aktau/6660848

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


- 영상 버퍼링 감지 (패킷드랍 혹은 low bandwidth) -> 확인필요
- 영상,음성 싱크감지 -> 확인필요
- 음성 노이즈 감지 -> 확인필요
==> 

네트워크 테스트랩

iperf

- speed limit
sudo yum install wondershaper
#from epel

http://www.linuxserve.com/2015/05/how-to-throttlelimit-network-bandwidth.html

wondershaper eth0 1024 512 
wondershaper clear eth0 






 1131* sudo nano /etc/sysconfig/network-scripts/ifcfg-br0
 1132* sudo service network restart
 1133* sudo wondershaper br-6c109e2ba805 10 10
 1134* chkconfig NetworkManager off
 1135* sudo chkconfig NetworkManager off
 1136* sudo service NetworkManager stop
 1137* sudo service NetworkManager status
 1138* sudo wondershaper br0 10 10
 1139* sudo service network restart
 1140* sudo wondershaper eno0 100 100
 1141* ifconfig
 1142* sudo wondershaper eno1 100 100
 1143* sudo wondershaper eno1 clear
 1144* sudo wondershaper br0 100 100
 1145  iperf -s
 1146* ip
 1147* sudo wondershaper clear
 1148* sudo wondershaper clear eno1
 1149* sudo wondershaper clear br0
 1150* sudo wondershaper br0 100 100
 1151* sudo wondershaper clear br0
 1152* ip
 1153* nmtui
 1154* sudo nmtui
 1155* chkconfig NetworkManager on
 1156* sudo chkconfig NetworkManager on
 1157* sudo service  NetworkManager start
 1158* sudo nmtui
 1159* ip
 1160* ifconfig
 1161* watch ifconfig

