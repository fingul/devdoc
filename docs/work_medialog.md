#overview

rtmp -> wowza(ts) -> ts(re-mux)ts -> video server


/Applications/VLC.app/Contents/MacOS/VLC -I dummy --no-repeat --no-loop -vvv vlc://quit
/Applications/VLC.app/Contents/MacOS/VLC -I rc

alias vlc="/Applications/VLC.app/Contents/MacOS/VLC"



#!/bin/bash
a="0.mp4"

vcodec="VIDEO_CODEC" 
acodec="AUDIO_CODEC" 
bitrate="VIDEO_BITRATE" 
arate="AUDIO_BITRATE" 
ext="OUTPUT_EXT" 
mux="MUXER" 
vlc="PATH_TO_VLC" 
fmt="INPUT_EXT"


vcodec="VIDEO_CODEC" 
acodec="AUDIO_CODEC" 
bitrate="VIDEO_BITRATE" 
arate="AUDIO_BITRATE" 
ext="OUTPUT_EXT" 
mux="MUXER" 
vlc="PATH_TO_VLC" 
fmt="INPUT_EXT" 


vlc -I dummy -vvv "$a" --sout "#transcode{vcodec=$vcodec,vb=$bitrate,acodec=$acodec,ab=$arate,channels=6}:standard{mux=$mux,dst=\"$a.$ext\",access=file}" vlc://quit 


:sout=#transcode{vcodec=h264,vb=1024,acodec=mp4a,ab=192}:standard{mux=ts,dst=224.0.0.0,access=udp}


vlc -I dummy -vvv "0.mp4" vlc://quit --sout=#transcode{vcodec=h264,vb=1024,acodec=mp4a,ab=192,channels=2,deinterlace}:standard{access=file,mux=ts,dst=t.ts} 