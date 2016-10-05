목표

--------------------------

1. ts -> 장비 입력 확인
1. winsend -> ts -> 장비 입력 확인

장비 1번 -> 직결 : 192.168.250.9 
    jnlp 받는다. -> admin/admin

--------------------------
- winsend 작업


wget -O /usr/local/lib/libebur128.so.1 "https://github.com/fingul/sffmpeg/blob/master/lib/libebur128.so.1.1.0?raw=true"
wget -O /usr/local/bin/frmxtract "https://github.com/fingul/sffmpeg/blob/master/bin/frmxtract?raw=true"
wget -O /usr/local/bin/ffmpeg "https://github.com/fingul/sffmpeg/blob/master/bin/ffmpeg?raw=true"
wget -O /usr/local/bin/ffprobe "https://github.com/fingul/sffmpeg/blob/master/bin/ffprobe?raw=true"
bash -c "chmod +x /usr/local/bin/{ffmpeg,ffprobe,frmxtract}"
bash -c "ldd /usr/local/bin/{ffmpeg,ffprobe,frmxtract}"

udp://@239.0.0.1:5000