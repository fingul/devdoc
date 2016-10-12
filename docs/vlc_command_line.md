# CLI Alias @ macOS

        alias vlc='/Applications/VLC.app/Contents/MacOS/VLC'
        alias vlc_dummy='/Applications/VLC.app/Contents/MacOS/VLC -I dummy'
        alias vlc_cli='/Applications/VLC.app/Contents/MacOS/VLC -I rc'

# 트랜스코딩 명렁어 와 예제들 : 중요!!

- 명령어 설명
<https://wiki.videolan.org/Documentation:Streaming_HowTo/Advanced_Streaming_Using_the_Command_Line/>

- 전체 명령어 조합
<https://wiki.videolan.org/Documentation:Streaming_HowTo/Command_Line_Examples/>

# 참고

- wiki : <http://www.videolan.org> ➜ wiki <https://wiki.videolan.org/>
- vlc announcement : https://www.jbkempf.com/blog/

# 참고 (기타)

- Livestreamer : Command-line utility that extracts streams from various services and pipes them into a video player of choice. 
<http://docs.livestreamer.io/#>

# vlc -linux
http://www.tecmint.com/install-vlc-media-player-in-rhel-centos-fedora/


- help

    vlc -H

-  debugging
    -vvv

vlc "udp://@239.0.0.1:5000" --vout dummy --aout dummy -v

vlc rtmp://192.168.0.51:1935/live/xxx --vout dummy --aout dummy -v

=> stats info is_playing

 sudo yum install -y iotop tcpdump iptraf
 sudo iptraf-ng
  sudo tcpdump
 1399  sudo yum install -y tcpdump
 1400  sudo tcpdump

# stream to memory @ player!!

- Stream to memory (smem) tutorial
<https://wiki.videolan.org/Stream_to_memory_(smem)_tutorial/>

# 문서 시작

<https://wiki.videolan.org/Documentation:Documentation/>

(<https://wiki.videolan.org> ➜ Documentation)

# libvlc 개발 가이드

<https://wiki.videolan.org/Hacker_Guide/>

# audio filter

<https://wiki.videolan.org/Hacker_Guide/Audio_Output/>

# vlc 설정 파일 위치


<http://www.videolan.org/support/faq.html#Config>

- macOS:

        ~/Library/Preferences/org.videolan.vlc

- Linux/Unix:
    
        $(HOME)/.config/vlc/vlcrc 

- Windows:

        2000/XP: %username%\Application Data\vlc\vlcrc

# 로깅

vlc 0.ts --loop --sout="#standard{mux=ts,dst=224.0.0.1:5000,access=udp}"  -vvv --logfile -         

