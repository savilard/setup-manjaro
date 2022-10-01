# Setup manjaro for python dev

<!-- TOC -->
* [Setup manjaro for python dev](#setup-manjaro-for-python-dev)
  * [Update system](#update-system)
  * [Oh my zsh](#oh-my-zsh)
  * [1Password](#1password)
  * [Poetry](#poetry)
  * [Git](#git)
  * [Neovim](#neovim)
  * [Tmux](#tmux)
  * [Google chrome](#google-chrome)
  * [Python](#python)
  * [Docker](#docker)
  * [Docker compose](#docker-compose)
  * [Podman](#podman)
  * [Postgresql](#postgresql)
  * [Ripgrep](#ripgrep)
  * [VSCode](#vscode)
  * [Bat](#bat)
  * [Fira-code font](#fira-code-font)
<!-- TOC -->

## Update system
```shell
sudo pacman -Syu
```

## [Oh my zsh](https://ohmyz.sh/)
```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
```
Set ZSH_THEME="spaceship" in your .zshrc.
Add zsh-autosuggestions and zsh-syntax-highlighting plugins in your .zshrc. 

## 1Password
```shell
curl -sS https://downloads.1password.com/linux/keys/1password.asc | gpg --import
git clone https://aur.archlinux.org/1password.git
cd 1password
makepkg -si
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
  
* With 1Password
  * https://blog.1password.com/1password-ssh-agent/
  * https://developer.1password.com/docs/ssh/get-started
  * https://blog.1password.com/git-commit-signing/


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

## Fira-code font
```shell
sudo pacman -S ttf-fira-code
```