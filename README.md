# Setup manjaro for python dev

<!-- TOC -->
* [Setup manjaro for python dev](#setup-manjaro-for-python-dev)
  * [Update system](#update-system)
  * [Poetry](#poetry)
  * [Git](#git)
  * [Neovim](#neovim)
  * [Tmux](#tmux)
  * [Google chrome](#google-chrome)
  * [Python](#python)
  * [Oh my zsh](#oh-my-zsh)
  * [Docker](#docker)
  * [Docker compose](#docker-compose)
  * [Podman](#podman)
  * [Postgresql](#postgresql)
  * [Ripgrep](#ripgrep)
  * [VSCode](#vscode)
  * [Bat](#bat)
<!-- TOC -->

## Update system
```shell
sudo pacman -Syu
```

## [Poetry](https://python-poetry.org/docs/#installation)
```shell
curl -sSL https://install.python-poetry.org | python3 -
mkdir $ZSH_CUSTOM/plugins/poetry
poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry
poetry config virtualenvs.in-project true
```
You must then add poetry to your plugins array in ~/.zshrc:

## Git
```shell
sudo pacman -S git
```
* Base
    ```shell
    git config --global user.name "Your name here"
    git config --global user.email "your_email@example.com"
    ```

* PGP
    ```shell
    gpg --full-generate-key
    gpg --armor --export
    gpg --list-secret-keys --keyid-format LONG
    git config --global user.signingkey
    git config --global commit.gpgsign true
    ```

* SSH
    ```shell
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
    sudo dnf install xclip
    xclip -sel clip < ~/.ssh/id_rsa.pub
    ```

## [Neovim](https://neovim.io/)
```shell
sudo pacman -S neovim
```

## [Tmux](https://github.com/tmux/tmux/wiki)
```shell
sudo pacman -S tmux
```

## Google chrome
```shell
pamac build google-chrome
```

## [Python](https://www.python.org)
https://www.python.org/downloads/
```shell
mv Downloads/Python-3.10.7.tar.xz . 
tar -xvf Python-3.10.7.tar.xz 
/configure --prefix=/home/savilard/.python3.10 --enable-optimizations
sudo make altinstall
nano ~/.zshrc -> add `export PATH=/home/savilard/.python3.10/bin:$PATH`
```

## [Oh my zsh](https://ohmyz.sh/)
```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
nano ~/.zshrc -> plugins=(zsh-autosuggestions zsh-syntax-highlighting)
```

## [Docker](https://www.docker.com/)
```shell
sudo pacman -S docker
sudo systemctl start docker.service
sudo systemctl enable docker.service
sudo docker version
sudo usermod -aG docker $USER
reboot
```

## [Docker compose](https://github.com/docker/compose)
```shell
sudo pacman -S docker-compose 
```

## [Podman](https://podman.io/)
```shell
sudo pacman -S podman
```

## [Postgresql](https://www.postgresql.org/)
```shell
sudo pacman -S postgresql
```

## [Ripgrep](https://github.com/BurntSushi/ripgrep)
```shell
sudo pacman -S ripgrep
```

## [VSCode](https://code.visualstudio.com/)
```shell
sudo pacman -S code
```

## [Bat](https://github.com/sharkdp/bat)
```shell
sudo pacman -S bat
```
