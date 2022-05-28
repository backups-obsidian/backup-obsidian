---
created: 2022-05-09 19:06
updated: 2022-05-28 08:39
---
---
**Links**: [[300 home]]

---
## Installing neovim
```bash
cd ~/Downloads
curl -L https://github.com/neovim/neovim/releases/latest/download/nvim.appimage -o nvim
chmod u+x nvim

# doing ./nvim should start a nvim 
./nvim

# which nvim won't work since we haven't added it to path
# adding nvim to path
sudo mv nvim /usr/local/bin
```
- Don't use apt for installing neovim since the versions are pretty old.
- Best part of using app images is that you don't need dependencies everything is packaged into the app image.

```bash
brew install neovim
```

- [Installing Neovim · neovim/neovim Wiki (github.com)](https://github.com/neovim/neovim/wiki/Installing-Neovim)

## Zshrc configuration
```bash
alias vim='nvim'

# if applications like github try to editor then it will default to nvim
export EDITOR='nvim' 
```

## Neovim Configuration (vim)
- Creating the config folder: `mkdir -p .config/nvim`
- Config file: `~/.config/nvim/init.vim`. This is equivalent to `.vimrc` file in vim.

## Plugins
- For using plugins we will have to use a plugin manager. [junegunn/vim-plug: Minimalist Vim Plugin Manager (github.com)](https://github.com/junegunn/vim-plug)

### Vim plug installation
```bash
mkdir -p ~/.config/nvim/autoload
curl https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim -o ~/.config/nvim/autoload/plug.vim
```

- We can also install it using the sh script given in the readme of the GitHub repository but it adds the `plug.vim`script to `~/.local/share`. I prefer to keep it in the nvim folder so that it is easy to sync using GitHub.

### Adding plugins using vim plug
```vim
" specifying the location for storing all the plugins
" this directory will be created by vim plug
call plug#begin('~/.config/nvim/plugged') 

" use single quotes only
Plug 'github link of plugin' 

call plug#end()
```
- We put all the plugins between plug begin and end.
- To install the plugin we need to do `:PlugInstall`
- *Don't commit the plugged directory to GitHub*. So whenever you clone your settings to a new system and do a `:PlugInstall` it will download the latest versions of the plugin.

### Useful Plugins
- `vim-fugitive` : for git integration
- `coc` : completion
	- You will have to do a specific `coc-intall` for the language server you want.

## Tips
- Once the plugin manager is set you can use tab for autocompletion while typing out commands.
- Use a particular theme: `:colorscheme gruvbox`

## Neovim configuration (lua)
- We can use *modules* in lua which this means we will not end up with large configuration files.
- We use the `require` function to load the different modules in lua. 
- So the base directory will have a `init.lua` file which will load all the modules.
- All the modules must be inside the `~/.config/nvim/lua` folder. For example we can have a settings folder inside lua folder. We will need a `init.lua` file in all the subfolders.


## Miscellaneous
- `:so %` after saving the file to source it.

## Options
- `:help options`
- [Nvim documentation: options (neovim.io)](https://neovim.io/doc/user/options.html)

## Plugins 
- We will be using packer for our plugins
- Packer is also written in lua