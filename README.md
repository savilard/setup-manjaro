# Setup manjaro

<!-- TOC -->
* [Setup manjaro](#setup-manjaro)
  * [Update system](#update-system)
  * [Kitty](#kitty)
  * [Oh my zsh](#oh-my-zsh)
  * [1Password](#1password)
  * [Python](#python)
  * [Pyenv](#pyenv)
  * [IPython](#ipython)
  * [Poetry](#poetry)
  * [Git](#git)
  * [Neovim](#neovim)
  * [Tmux](#tmux)
  * [Google chrome](#google-chrome)
  * [Docker](#docker)
  * [Docker compose](#docker-compose)
  * [Podman](#podman)
  * [Lazydocker](#lazydocker)
  * [Minikube](#minikube)
  * [Kubectl](#kubectl)
  * [Postgresql](#postgresql)
  * [Ripgrep](#ripgrep)
  * [VSCodium](#vscodium)
  * [Postman](#postman)
  * [Bat](#bat)
  * [Exa](#exa)
  * [Fira-code font](#fira-code-font)
  * [Pipx](#pipx)
  * [VirtualBox](#virtualbox)
  * [Zoom](#zoom)
  * [Telegram](#telegram)
  * [Slack](#slack)
<!-- TOC -->

## Update system
```shell
sudo pacman -Syu
```

## Kitty
```shell
sudo pacman -S kitty
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

## Python
```shell
mv Downloads/Python-3.10.7.tar.xz . 
tar -xvf Python-3.10.7.tar.xz
cd Python-3.10.7 
/configure --prefix=/home/{username}/.python3.10 --enable-optimizations
make
sudo make altinstall
echo 'export PATH=/home/{username}/.python3.10/bin:$PATH' >> ~/.zshrc
```

## Pyenv
```shell
 git clone https://github.com/pyenv/pyenv.git ~/.pyenv
 cd ~/.pyenv && src/configure && make -C src
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

## IPython
```shell
sudo pacman -S ipython
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
  * https://github.blog/changelog/2022-08-23-ssh-commit-verification-now-supported/


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
sudo pacman -S podman-compose
```

## [Lazydocker](https://github.com/jesseduffield/lazydocker)
```shell
yay -S lazydocker
```

## Minikube
```shell
sudo pacman -S minikube
or
go get github.com/jesseduffield/lazydocker
```

## Kubectl
```shell
sudo pacman -S kubectl
```

## [Postgresql](https://www.postgresql.org/)
```shell
sudo pacman -S postgresql
```

## [Ripgrep](https://github.com/BurntSushi/ripgrep)
```shell
sudo pacman -S ripgrep
```

## VSCodium
```shell
flatpak install flathub com.vscodium.codium
```

## Postman
```shell
flatpak install flathub com.getpostman.Postman
```

## [Bat](https://github.com/sharkdp/bat)
```shell
sudo pacman -S bat
```

## [Exa](https://github.com/ogham/exa)
```shell
sudo pacman -S exa
```

## Fira-code font
```shell
sudo pacman -S ttf-fira-code
```

## Pipx
```shell
sudo pacman -S python-pipx
```

## VirtualBox
To install VirtualBox, you need to install the packages virtualbox and linux*-virtualbox-host-modules. 
The latter must match the version of the kernel you are running. To list what kernels is installed use mhwd (example)

```shell
$ mhwd-kernel -li

Currently running: 5.4.0-1-MANJARO (linux54)
The following kernels are installed in your system:
   * linux54
```
To install VirtualBox and the kernel modules for your installed kernel enter the following command in the terminal:

```shell
$ sudo pacman -Syu virtualbox linux54-virtualbox-host-modules
```
Once the installation has completed, it will then be necessary to add the VirtualBox Module to your kernel. 
The easy way is to simply reboot your system. Otherwise, to start using VirtualBox immediately, enter the following command:

```shell
$ sudo vboxreload
```

## Zoom
```shell
flatpak install flathub us.zoom.Zoom
```

## Telegram
```shell
flatpak install flathub org.telegram.desktop
```

## Slack
```shell
flatpak install flathub com.slack.Slack
```