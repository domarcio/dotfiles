# dotfiles

My personal configurations for development on LINUX.

## Before

It's necessary to have already installed some things before following the steps below:

* Essentials packages for development.
* Git (installed and configure).
* TMUX.
* ZSH.

```bash
[user@pc: ~]$ sudo dnf groupinstall "Development Tools" "Development Libraries"
[user@pc: ~]$ sudo dnf install git tmux zsh autoconf

[user@pc: ~]$ [if necessary] ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "foo@bar.dev"
[user@pc: ~]$ [if necessary] eval "$(ssh-agent -s)"
[user@pc: ~]$ [if necessary] sh-add ~/.ssh/id_ed25519

[user@pc: ~]$ git config --global user.name "Marcio Vinicius"
[user@pc: ~]$ git config --global user.email "foo@bar.dev"

[user@pc: ~]$ sudo dnf install podman-docker
```

## Steps

1. Configure [tmux](#configure-tmux);
2. Install [asdf](#install-asdf);
3. Manage [asdf](#manage-asdf);
4. Install [Visual Studio Code](#visual-studio-code);
5. Install [Oh-My-ZSH](#install-oh-my-zsh);
6. Add [`.config`](.config) to the [.zsh](#append-to-zsh).

### Configure tmux

Read more: <https://github.com/gpakosz/.tmux>

```bash
[user@pc: ~]$ git clone https://github.com/gpakosz/.tmux.git
[user@pc: ~]$ ln -s -f .tmux/.tmux.conf
[user@pc: ~]$ cp .tmux/.tmux.conf.local .
```

### Install asdf

Read more: <https://asdf-vm.com/#/core-manage-asdf>

```bash
[user@pc: ~]$ git clone https://github.com/asdf-vm/asdf.git ~/.asdf
[user@pc: ~]$ cd ~/.asdf
[user@pc: ~]$ git checkout "$(git describe --abbrev=0 --tags)"
```

### Manage asdf

```bash
[user@pc: ~]$ asdf plugin-add golang https://github.com/kennyp/asdf-golang.git
[user@pc: ~]$ asdf plugin add golangci-lint https://github.com/hypnoglow/asdf-golangci-lint.git
[user@pc: ~]$ asdf install golang latest:1.16
[user@pc: ~]$ asdf install golangci-lint latest:1.40
[user@pc: ~]$ asdf global golang 1.16.4
[user@pc: ~]$ asdf global golangci-lint 1.40.1
```

### Visual Studio Code

Read more: <https://code.visualstudio.com/docs/setup/linux>

```bash
[user@pc: ~]$ sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
[user@pc: ~]$ sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
[user@pc: ~]$ sudo dnf check-update
[user@pc: ~]$ sudo dnf install code
```

Now, install Settings Sync plugin and configure it: <https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync>

### Install Oh-My-ZSH

Read more: <https://ohmyz.sh/#install>

```bash
[user@pc: ~]$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
[user@pc: ~]$ chsh -s $(which zsh)
```

### Append to .zsh

```bash
[user@pc: ~]$ echo ". \$HOME/projects/dotfiles/.config" >> .zshrc
```
