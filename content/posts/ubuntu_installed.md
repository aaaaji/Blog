---
title: "筆電 Ubuntu 安裝常用工具清單"
draft: false
date: "2020-04-03"
tags: ["ubuntu","tools"]
categories: ["技術"]
---

如標題，這邊紀錄了各種我Ubuntu筆電常安裝/常用的程式或小工具，之後累積一下應該會各自獨立寫出來
預期之後會寫個自動安裝環境工具

- 參考連結
    - [Link](https://www.twbsd.org/cht/book/ch24.htm)
    - [ubuntu auto setting參考](https://github.com/SickoOrange/UbuntuAutoScript/blob/master/setup.sh)

* Homebrew (on Linux)
    **buile-essential, curl, file, git** should been installed before install homebrew.
    ```bash=
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
    # press "Enter" to continue install
    
    test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
    test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
    test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
    echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
    # test if brew install successful
    brew install help
    ```

* Chromium
    ```bash=
    $ sudo apt install chromium-browser
    ```

* Chrome-stable
    ```bash=
    $ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
    $ sudo dpkg -i google-chrome-stable_current_amd64.deb
    ```

* git-lfs
    ```bash=
    $ sudo apt install git-lfs
    ```

* python coding
    ```bash=
    $ sudo apt install python3
    $ sudo apt install python3-pip
    $ sudo pip3 install pipenv
    $ sudo snap install code --classic
    ```

* htop
    ```bash=
    $ sudo apt install htop
    ```

* go language
    ```bash=
    $ brew install go
    ```

* hugo
    ```bash=
    $ brew install hugo
    ```

* curl
    ```bash=
    $ sudo apt install curl
    ```

* OpenVPN
    ```bash=
    $ sudo apt install network-manager-openvpn network-manager-openvpn-gnome
    $ sudo apt install openvpn-systemd-resolved
    ```
    
    * add in opvn file
        ```bash=
        script-security 2
        up /etc/openvpn/update-systemd-resolved
        down /etc/openvpn/update-systemd-resolved
        down-pre
        ```

* telegram
    ```bash=
    sudo add-apt-repository ppa:atareao/telegram
    sudo apt update && sudo apt install telegram
    
    # Chinese input error fix ,input "env QT_IM_MODULE=<輸入法>" before at EXEC 
    sudo nano ~/.local/share/applications/telegramdesktop.desktop
    Exec="env QT_IM_MODULE=<輸入法>" /opt/telegram/telegram -- %u
    ```

    ![](https://hackmd.teamt5.net/uploads/upload_35044048b204ea4adab28f017e896b46.png)

* keepass2
    ```bash=
    $ sudo apt install keepass2
    ```

- Docker
    ```bash=
    sudo apt install docker.io
    ```

    設定權限，[參考Link](https://ephrain.net/docker-%E4%BD%BF%E7%94%A8%E9%9D%9E-root-%E6%AC%8A%E9%99%90%E4%BE%86%E5%9F%B7%E8%A1%8C-docker-client/)
    ```bash=
    # 建立docker群組(有可能已經有了)
    sudo groupadd docker
    
    # 將非root帳號加入docker中
    sudo usermod -G docker -a <username>
    newgrp docker
    groups
    
    # 設定開機自動啟動&重新啟動
    sudo systemctl enable docker
    sudo systemctl restart docker
    ```
- Docker-Compose
    ```sudo apt install docker.io```

* conky
    ```bash=
    $ sudo apt install conky-all
    ```

* LinSSID
    ```bash=
    $ sudo apt install linssid
    ```

* VMware Workstation 14 Pro
    ```bash=
    官網下載
    $ sudo apt install build-essential
    $ sudo chmod 755 VMware-Workstation-Full-14.1.7-12989993.x86_64.bundle
    $ sudo ./VMware-Workstation-Full-14.1.7-12989993.x86_64.bundle
    ```

    * load vmmon kernel module failed
        ![](https://hackmd.teamt5.net/uploads/upload_48c3ff969a4997f47501d5b8ae5ade1e.png)
        
        ```bash=
        openssl req -new -x509 -newkey rsa:2048 -keyout VMW.priv -outform DER -out VMW.der -nodes -days 36500 -subj "/CN=VMware/"
        sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMW.priv ./VMW.der $(modinfo -n vmmon)
        sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMW.priv ./VMW.der $(modinfo -n vmnet)
        sudo mokutil --import VMW.der
        ```

* powerlevel 9k
    * install zsh
        ```bash=
        $ sudo apt install zsh
        # set ZSH as default login shell
        $ sudo usermod -s /usr/bin/zsh $(whoami)
        $ sudo reboot now
        ```
        ![](https://hackmd.teamt5.net/uploads/upload_c3ec225ed6d351a8746f46a0a6a6dd78.png)
        select 2 and zsh will create a new **~/.zshrc** configuration file
    * install powerline and powerline fonts
        ```bash=
        $ sudo apt install powerline fonts-powerline
        ```
    * install zsh powerlevel9k theme
        ```bash=
        $ sudo apt install zsh-theme-powerlevel9k
        $ echo "source /usr/share/powerlevel9k/powerlevel9k.zsh-theme" >> ~/.zshrc
        ```
    * install syntax highlighting
        ```bash=
        $ sudo apt install zsh-syntax-highlighting
        $ echo "source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
        ```
    * clear zsh history
        ```bash=
        $ echo "" > ~/.zsh_history & exec $SHELL -l
        ```

* dbeaver
    ```bash=
    $ sudo snap install dbeaver-ce
    ```

* FlashPlayer
    ```bash=
    $ sudo add-apt-repository "deb http://archive.canonical.com/ $(lsb_release -sc) partner"
    $ sudo apt update
    $ sudo apt install flashplugin-installer
    ```

* WINEHQ
    ```bash=
    # enable 32 bit architecture when your system is 64 bit
    $ sudo dpkg --add-architecture i386 
    
    # Download and add the repository key
    $ sudo wget -nc https://dl.winehq.org/wine-builds/winehq.key
    $ sudo apt-key add winehq.key
    
    # Add repository
    $ sudo apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main'

    $ sudo apt update
    $ sudo apt install winehq-stable --install-recommends
    ```

* Alien
    ```bash=
    $ sudo apt install alien
    ```

* ddrescueview
    ```bash=
    $ sudo apt install ddrescueview
    $ sudo apt install libcanberra-gtk-module
    ```

* smartctl
    ```bash=
    $ sudo apt install smartmontools
    ```
