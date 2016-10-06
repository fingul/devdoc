# WOWZA & FFMPEG & RTMP

# 스트림 입력 id/pw = 1/1 로 서버에 쏜다. 


# 서버는 


- `http://qxqx.iptime.org:8088/enginemanager/` -> `Source Authentication` -> ` Add Source` 눌러서 id/pw 추가


# FFMPEG(RTMP) -> WOWZA


stream name : xxx

ffmpeg -y -re -f lavfi -i 'testsrc=size=320x240[out0];aevalsrc=sin(440*2*PI*t)[out1]' -vcodec libx264 -pix_fmt yuv420p -ac 2 -f flv rtmp://1:1@192.168.0.51/live/xxx


------------------------------


# WOWZA -> CLIENT


http://qxqx.iptime.org:8088 


MPEGDASH
http://192.168.0.51:1935/live/streamname/manifest.mpd


iOS
http://192.168.0.51:1935/live/streamname/playlist.m3u8


Android/Other
rtsp://192.168.0.51:1935/live/streamname


HLS - @VLC
http://192.168.0.51:1935/live/streamname/playlist.m3u8


## adobe rtmp

server : rtmp://192.168.0.51:1935/live
==> @ ffmpeg / vlc => rtmp://192.168.0.51:1935/live/xxx

adobe HDS
http://192.168.0.51:1935/live/streamname/manifest.f4m


----------------


# WOWZA -> FFMPEG (RTMP)


ffmpeg -i rtmp://192.168.0.51:1935/live/streamname -f null -  


# WOWZA -> FFMPEG (HLS)


ffmpeg -i http://192.168.0.51:1935/live/streamname/playlist.m3u8 -f null -  


# WOWZA -> FFMPEG (udp 모니터링 @ VLC : udp://@0.0.0.0:1234 )


ffmpeg -i http://192.168.0.51:1935/live/streamname/playlist.m3u8 -c copy -f mpegts "udp://127.0.0.1:1234?pkt_size=1316"
