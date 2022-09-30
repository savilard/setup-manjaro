# Setup manjaro for python dev

## [Poetry](https://python-poetry.org/docs/#installation)
```shell
curl -sSL https://install.python-poetry.org | python3 -
mkdir $ZSH_CUSTOM/plugins/poetry
poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry
poetry config virtualenvs.in-project true
```
You must then add poetry to your plugins array in ~/.zshrc:


## Git

### Base
```shell
git config --global user.name "Your name here"
git config --global user.email "your_email@example.com"
```

### PGP
```shell
gpg --full-generate-key
gpg --armor --export
gpg --list-secret-keys --keyid-format LONG
git config --global user.signingkey
git config --global commit.gpgsign true
```

### SSH
```shell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
sudo dnf install xclip
xclip -sel clip < ~/.ssh/id_rsa.pub
```