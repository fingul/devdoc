
# mac dev setup - 이건 배껴야 함!!

    <https://github.com/donnemartin/dev-setup>


# python dict tools!
- A python library for accessing and searching dictionaries via /slashed/paths ala xpath

    <https://github.com/akesterson/dpath-python>

- addict - the Python Dict that's better than heroin.
    

# controller
    
- CouchPotato : Automatic Movie Downloading via NZBs & Torrents <https://github.com/CouchPotato/CouchPotatoServer>            

# login item

- dropbox
- google drive
- vpn
- spectacle
- docker
- better touch tool
- posgresql
- Karabiner
- teamviewer
- skitch
- alfred
- istatmenu 
- fantastical


# list keep in dock installed apps

    import plistlib

    #python3
    from urllib.parse import urlparse
    #urllib.unquote(string)
    import urllib

    import subprocess
    cmd = 'defaults export com.apple.dock -'
    r = subprocess.check_output(cmd, shell=True)
    d = plistlib.loads(r)
    l = [i.get('tile-data',{}).get('file-data',{}).get('_CFURLString') for i in d.get('persistent-apps')]
    l = [urlparse(i).path for i in l]
    l = [urllib.unquote(i).path for i in l]
    print(l)


    
    #아래 파일도 작업할것!!!
    #~/Library/Preferences/com.apple.loginitems.plist