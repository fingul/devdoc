# ssh-copy-id

    brew install ssh-copy-id

    ssh-copy-id `HOST-NAME`

# no passwd

    sudo echo "$USER ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers

# ohmyzsh

    sudo apt-get install -y openssh-server git zsh

    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"


## SSH server enable / disable password authentication

    sudo su -
    wget -q --no-check-certificate https://raw.githubusercontent.com/panticz/scripts/master/disable_ssh_password_authentication.sh -O - | bash -
    exit

        http://www.panticz.de/SSH-server-enable-disable-password-authentication

        #!/bin/bash

        sed -i 's|[#]*PasswordAuthentication yes|PasswordAuthentication no|g' /etc/ssh/sshd_config
        sed -i 's|UsePAM yes|UsePAM no|g' /etc/ssh/sshd_config
        service ssh restart

# install ubuntu make & pycharm,webstorm,...

    sudo add-apt-repository -y ppa:ubuntu-desktop/ubuntu-make
    sudo apt-get -y update
    sudo apt-get install -y ubuntu-make

    umake ide visual-studio-code
    umake ide webstorm
    umake ide pycharm-professional
    umake ide idea-ultimate
            
# hangul

    기본으로 설치시 English만 설치되었다고 가정하고 한글 설치와 한영 전환 설정하는 것을 어떻게 하는지 알아보자.

    한글 설치

    sudo apt-get install -y fcitx-hangul
    System Settings > Language Support를 실행해서 아직 완전히 설치되지 않다고 표시되는데 잠시 기다려서 모두 설치한다.
    Keyboard input method system:을 ibus가 아닌 fcitx로 변경한다.
    재부팅한다.
    AllSettings > Keyboard > Shortcuts Tab > Typing을 선택한다.
    Switch to Next source, Switch to Previous sourc, Compose Key, Alternative Characters Key를 모두 Disabled로 선택한다. Disabled로 선택하기 위해서는 backspace를 누르면 된다.
    Compose Key의 Disabled를 길게 눌러 Right Alt를 선택한다.
    Switch to next source는 한영키를 눌러 Multikey를 선택한다. 반드시 Compose Key 설정이 먼저되어야 Multikey를 선택할 수 있다.
    AllSetting 윈도우를 닫고 상단 메뉴바 오른쪽의 입력기 선택하는 것을 본다. 키보드 표시가 된 것이 fcitx이다. fcitx아이콘을 눌러서 Configure Current Input Method를 선택한다.
    Keyboard-English(US)가 있다면 +를 눌러 Hangul을 추가한다. (Uncheck “Only Show Current Language”). Korean이 아닌 Hangul이여야 한다.
    Global Config tab에서 Trigger Input Method는 한/영키를 눌러 Multikey로 설정(왼쪽 오른쪽 모두)하고 Extrakey for trigger input method는 Disabled로 설정한다. (Mac에서는 command key이므로 대신 shift+space를 선택한다.)
    Global Config tab에서 Program > Share State Among Window > All을 선택한다.
    테스트
    log out을 한후 다시 log in을 한다.
    한글/영어가 한영키로 전환되는지 확인한다.
    
# dropbox

   cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
   ~/.dropbox-dist/dropboxd

# google drive

<http://www.omgubuntu.co.uk/2016/08/use-google-drive-ubuntu-16-04-linux-desktops>

    sudo apt install -y gnome-control-center gnome-online-accounts    

# 로그인 할 때 keyring 물어보는것 비활성화 

How can I stop being prompted to unlock the 'default' keyring on boot?

    <http://askubuntu.com/questions/867/how-can-i-stop-being-prompted-to-unlock-the-default-keyring-on-boot/875#875>
    Open Applications -> Accessories -> Password and Encryption Keys
    Right-click on the "login" keyring
    Select "Change password"
    Enter your old password and leave the new password blank
    Press ok, read the security warning, think about it and if you still want to get rid of this dialog, choose "use unsafe storage".

