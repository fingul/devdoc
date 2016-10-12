# testsrc

    ffplay  -f lavfi -i 'testsrc=size=1920x1080:rate=25[out0];aevalsrc=sin(440*2*PI*t)*0.0[out1]' -vf "drawtext=fontfile=/Library/Fonts/Tahoma.ttf:fontsize=200:timecode='00\:00\:00\:00':rate=25:x=(w-tw)/2: y=h-(2*lh): fontcolor=white: box=1: boxcolor=0x00000099"


## todo

script로 만들어서 실행할 수 있도록

    ffmpeg `echo -y -i 0.mp4 1.mp4`
    ffmpeg $(echo -y -i 0.mp4 1.mp4)

# test pattern


<http://www.bogotobogo.com/FFMpeg/ffmpeg_video_test_patterns_src.php>
<https://trac.ffmpeg.org/wiki/FancyFilteringExamples>
    