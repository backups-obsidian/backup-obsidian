---
created: 2022-05-09 19:06
updated: 2022-05-11 23:51
---
---
**Links**: [[300 home]]

---
```bash
sudo apt install neovim
```
- Once installed you can use neovim using `nvim`
- Location of config folder: `~/.config/nvim`. If either `.config` or `nvim` folder is not present then create them.
- Config file: `~/.config/nvim/init.vim`
- For using plugins we will have to use a plugin manager. [junegunn/vim-plug: Minimalist Vim Plugin Manager (github.com)](https://github.com/junegunn/vim-plug)
	- In the readme section find the script to run for neovim.
```vim
call plug#begin()
" use single quotes only
Plug 'github link of plugin' 
call plug#end()
```
- To install the plugin we need to do `:PlugInstall`
