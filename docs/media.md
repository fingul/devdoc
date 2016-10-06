# 정지화면 감지

        import math
        import glob
        from PIL import Image
        from functools import reduce

        def image_diff(p1,p2):

            h1 = Image.open(p1).histogram()
            h2 = Image.open(p2).histogram()


            diff_squares = [(h1[i] - h2[i]) ** 2 for i in range(len(h1))]
            rms = math.sqrt(sum(diff_squares) / len(h1))

            print("p1={}, p2={}, rms={}".format(p1,p2,rms))

        
        l = glob.glob('/tmp/1/*.png')

        pairs = [  (l[n],l[n+1])  for n,i in enumerate(l) if n<len(l)-1]
        [image_diff(p1,p2) for p1,p2 in pairs]    


# 확인 사항
- stack을 바꿔야합니다. dependency가 있습니다. rpm 추가 설치 필요
- 워크로드 관련 하여 디덱트 주기 : 확인 - 대략 5초
- Intel(R) Core(TM) i5-4250U CPU @ 1.30GHz

# How to set up your own private RTMP server using nginx
<https://obsproject.com/forum/resources/how-to-set-up-your-own-private-rtmp-server-using-nginx.50/>

# rtmp 서비스 비교
<http://lpokeh.blogspot.kr/2014/07/korean-only-daumpot-afreeca-rtmp.html>

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



# 아래 두개는 vlc VU meter를 쓴다.
https://en.wikipedia.org/wiki/VU_meter
- Reference Level (typically +4dBu, valid with tones only)
- Standard Output Level (10dB above Reference, typical peak levels)
- Clip Level (6dB above Standard Output Level, "headroom" to allow for unusual conditions)[2][3]

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

