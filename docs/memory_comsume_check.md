ffmpeg -y -re -i Sintel.2010.1080p.mkv -vcodec copy -acodec aac -ac 2 -f flv rtmp://1:1@192.168.0.51/live/xxx
ffmpeg -y -re -i Sintel.2010.720p.mkv -vcodec copy -acodec aac -ac 2 -f flv rtmp://1:1@192.168.0.51/live/xxx

vlc  --vout dummy --aout dummy  rtmp://192.168.0.51:1935/live/xxx
vlc  --vout dummy --aout dummy http://192.168.0.51:1935/live/xxx/playlist.m3u8

yum install -y smem
watch "smem -k"

500MB / 300MB

PSS 값을 측정


- 1080p 기준 채널 당 : 500MB (VLC 기준 170MB)
- 720p 기준 채널 당 : 300MB (VLC 기준 100MB)

- 배경 자료

<http://ecogeo.tistory.com/255>

        USS와 PSS

        VSS나 RSS보다 조금 더 의미있는 수치는 USS와 PSS인데, procrank 명령어로 구할 수 있다. 

        USS(Unique Set Size) : 프로세스만의 고유한 페이지 수. 공유되지 않는 프로세스에 private한 메모리 크기이다.
        PSS(Proportional Set Size) : USS + (공유 페이지 / 공유하는 프로세스 수). 즉, 프로세스 고유 메모리 사용량 + 하나의 프로세스가 차지하는 공유 메모리 비율이다. 만약 A프로세스가 6MB 메모리를 사용하고 그 중 2MB가 그 프로세스의 고유 영역이라면, 나머지 4MB는 공유 메모리이다. 4MB의 공유메모리를 4개의 프로세스가 공유하고 있다면 PSS는 2MB + (4MB/4) = 3MB가 된다.
        PSS는 공유되는 페이지를 공유 프로세스의 수로 나누어서 좀더 정확한 메모리 사용량을 파악할 수 있게 해준다. 이게 프로세스가 사용하는 실제 메모리 크기에 가장 근접한 값이라고 볼 수 있다. 

