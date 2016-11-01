#gpmidi/centos-6.4
---
비고 : 6.4 제외

gpmidi/centos-6.3
gpmidi/centos-6.5
centos:6.6
centos:6.7
centos:6.8
centos:7.0.1406
centos:7.1.1503
centos:7.2.1511


-DASH : http://192.168.0.51:1935/vod/mp4:sample.mp4/manifest.mpd
=> VLC는 원래 안됨
-HLS : http://192.168.0.51:1935/vod/mp4:sample.mp4/playlist.m3u8
-RTMP : rtmp://192.168.0.51:1935/vod/mp4:sample.mp4

--------    

#버전 확인
echo $(rpm -q --whatprovides redhat-release)
> centos-release-6-3.el6.centos.9.x86_64

rpm -q --qf "%{VERSION}" $(rpm -q --whatprovides redhat-release)

# run vlc as root (not recommend)

sed -i 's/geteuid/getppid/' /usr/bin/vlc

# VLC INSTALL

    docker run -it centos:7 bash
    docker run -it centos:6 bash

    yum -y install yum-utils epel-release

    # for fix centos @6.3
    # Error: Cannot retrieve metalink for repository: epel. Please verify its path and try again 

    rpm -Uvh http://li.nux.ro/download/nux/dextop/el6/x86_64/nux-dextop-release-0-2.el6.nux.noarch.rpm

    rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
    
    yum --disablerepo=epel -y update  ca-certificates

    yumdownloader --resolve vlc
    yum -y --nogpgcheck localinstall *.rpm

    # for fix
    # @centos6 - D-Bus library appears to be incorrectly set up; failed to read
    #
    service messagebus start


