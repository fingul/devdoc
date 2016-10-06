
# 흑백 / 정지 영상 detect 전략

N FRAME마다 이미지를 작은 사이즈로 캡춰한다.

- 흑백
  # black detect
  http://stackoverflow.com/questions/3490727/what-are-some-methods-to-analyze-image-brightness-using-python/3498247#3498247

- 정지 영상 검출

  # image difference를 구한다. (RMSE - root mean square error)
  - threshold 값보다 작으면 검출 경고, 아니면 skip   
  http://stackoverflow.com/questions/1927660/compare-two-images-the-python-linux-way/1927681#1927681

  
  <https://wiki.videolan.org/How_to_create_thumbnails/>

  vlc rtmp://192.168.0.51:1935/live/xxx --vout dummy --aout dummy --scene-format=png --video-filter=scene --scene-ratio=24 --scene-prefix=snap --scene-path=/tmp/0 


  # /Users/m/Downloads/vlc-2.2.4/modules/video_filter/scene.c

          add_string(  CFG_PREFIX "format", "png",
                      FORMAT_TEXT, FORMAT_LONGTEXT, false )
          add_integer( CFG_PREFIX "width", -1,
                      WIDTH_TEXT, WIDTH_LONGTEXT, true )
          add_integer( CFG_PREFIX "height", -1,
                      HEIGHT_TEXT, HEIGHT_LONGTEXT, true )
          add_string(  CFG_PREFIX "prefix", "scene",
                      PREFIX_TEXT, PREFIX_LONGTEXT, false )
          add_string(  CFG_PREFIX "path", NULL,
                      PATH_TEXT, PATH_LONGTEXT, false )
          add_bool(    CFG_PREFIX "replace", false,
                      REPLACE_TEXT, REPLACE_LONGTEXT, false )
   


## 구현은 아니고 요청 하는 내용 (Freeze frame detection. (tolerance to % change and duration).)
qa 가능한 factor 달라고 요청하는 내용 : [FFmpeg-user] FFplay monitoring gig.
http://lists.ffmpeg.org/pipermail/ffmpeg-user/2011-November/003285.html

# ffmpeg detect black

http://video.stackexchange.com/questions/16564/how-to-trim-out-black-frames-with-ffmpeg-on-windows

## Black and Frozen Frame Detection - Tektronix
www.tek.com/dl/2PW-24654-0.pdf

# vlc - mac

alias vlc='/Applications/VLC.app/Contents/MacOS/VLC -I rc'

# vlc -linux
http://www.tecmint.com/install-vlc-media-player-in-rhel-centos-fedora/

vlc "udp://@239.0.0.1:5000" --vout dummy --aout dummy -v

vlc rtmp://192.168.0.51:1935/live/xxx --vout dummy --aout dummy -v

=> stats info is_playing

 sudo yum install -y iotop tcpdump iptraf
 sudo iptraf-ng
  sudo tcpdump
 1399  sudo yum install -y tcpdump
 1400  sudo tcpdump

# centos7 multicast join 활성화

sudo nano /etc/sysctl.conf

  ○ cat /etc/sysctl.conf                                
  # System default settings live in /usr/lib/sysctl.d/00-system.conf.
  # To override those settings, enter new settings here, or in an /etc/sysctl.d/<name>.conf file
  #
  # For more information, see sysctl.conf(5) and sysctl.d(5).
  #net.ipv4.conf.default.rp_filter=0



  net.ipv4.conf.eno1.force_igmp_version = 2
  net.ipv4.conf.lo.force_igmp_version = 2

sudo sysctl -p

------------------




vlc -vvv "udp://@239.0.0.1:5000"

# test pattern


<http://www.bogotobogo.com/FFMpeg/ffmpeg_video_test_patterns_src.php>
<https://trac.ffmpeg.org/wiki/FancyFilteringExamples>

목표

--------------------------

- 출력의 cbr화
- 모니터링 부분

ffmpeg -y -re -f lavfi -i 'testsrc=size=1280x720[out0];aevalsrc=sin(440*2*PI*t)[out1]' -muxrate 2000k -vcodec libx264 -pix_fmt yuv420p -c:a aac -ac 2 -f mpegts "udp://239.0.0.1:5000"


ffmpeg -y -re  -f lavfi -i 'testsrc=size=1280x720:r=29.970[out0];aevalsrc=sin(440*2*PI*t)[out1]' -vcodec libx264  -pix_fmt yuv420p -c:a aac -ac 2 -muxrate 4000K  -nal-hrd cbr -f mpegts  "udp://239.0.0.1:5000?pkt_size=1316"



ffprobe "udp://239.0.0.1:5000"


--------------
#안되는것

Input #0, mpegts, from 'udp://239.0.0.1:5000':
  Duration: N/A, start: 78.686344, bitrate: N/A
  Program 1 
    Metadata:
      service_name    : Service01
      service_provider: FFmpeg
    Stream #0:0[0x100]: Video: h264 (High) ([27][0][0][0] / 0x001B), yuv420p, 1280x720 [SAR 1:1 DAR 16:9], 25 fps, 25 tbr, 90k tbn, 50 tbc
    Stream #0:1[0x101]: Audio: aac (LC) ([15][0][0][0] / 0x000F), 44100 Hz, stereo, fltp, 119 kb/s


#되는것
Input #0, mpegts, from 'udp://239.0.0.1:5000':
  Duration: N/A, start: 527.696033, bitrate: N/A
  Program 1 
    Stream #0:0[0x100], 212, 1/90000: Video: h264 (Baseline), 1 reference frame ([27][0][0][0] / 0x001B), yuv420p(tv, left), 1280x720 [SAR 1:1 DAR 16:9], 0/1, 29.97 fps, 29.97 tbr, 90k tbn, 59.94 tbc
    Stream #0:1[0x101], 305, 1/90000: Audio: aac (LC) ([15][0][0][0] / 0x000F), 44100 Hz, stereo, fltp, 121 kb/s





목표

1. ts -> 장비 입력 확인
1. winsend -> ts -> 장비 입력 확인

--------------------------
- winsend 작업


--------------------------

1. ts -> 장비 입력 확인
1. winsend -> ts -> 장비 입력 확인

장비 1번 -> 직결 : 192.168.250.9 
    jnlp 받는다. -> admin/admin
장비 3번 : 입력신호

--------------------------
- winsend 작업


wget -O /usr/local/lib/libebur128.so.1 "https://github.com/fingul/sffmpeg/blob/master/lib/libebur128.so.1.1.0?raw=true"
wget -O /usr/local/bin/frmxtract "https://github.com/fingul/sffmpeg/blob/master/bin/frmxtract?raw=true"
wget -O /usr/local/bin/ffmpeg "https://github.com/fingul/sffmpeg/blob/master/bin/ffmpeg?raw=true"
wget -O /usr/local/bin/ffprobe "https://github.com/fingul/sffmpeg/blob/master/bin/ffprobe?raw=true"
bash -c "chmod +x /usr/local/bin/{ffmpeg,ffprobe,frmxtract}"
bash -c "ldd /usr/local/bin/{ffmpeg,ffprobe,frmxtract}"

udp://@239.0.0.1:5000
--------------------------
# 기타 제안 - VLC 모니터링
<https://github.com/jaruba/node-vlc-multiscreen>

# number_of_window=4
#    12
#    34



- number_of_window: 4
- title:
  windows_no: 1
  url: udp://@1.1.1.1:5000
  time:
  static: yes       
