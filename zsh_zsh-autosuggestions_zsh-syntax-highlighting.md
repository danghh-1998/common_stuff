# Install zsh, oh-my-zsh, zsh-autosuggestions & zsh-syntax-highlighting

- Install zsh

```bash
sudo apt install zsh -y
```

- Install oh-my-zsh

```bash
sudo apt install curl -y
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

- Install zsh-autosuggestions & zsh-syntax-highlighting

```bash
sudo apt install git
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
vim ~/.zshrc
```

- Find `plugins=(git)` change to `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`
- Exit vim
- Apply changes

```bash
source ~/.zshrc
```

