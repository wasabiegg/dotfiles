This should make True Color (24-bit) and italics work in your [tmux](https://github.com/tmux/tmux/wiki) session and [vim](https://github.com/vim/vim)/[neovim](https://github.com/neovim/neovim) when using [Alacritty](https://github.com/alacritty/alacritty) (and should be compatible with any other terminal emulator, including [Kitty](https://github.com/kovidgoyal/kitty)).

## Testing colors

Running this script should look the same in tmux as without.

```shell
curl -s https://gist.githubusercontent.com/lifepillar/09a44b8cf0f9397465614e622979107f/raw/24-bit-color.sh >24-bit-color.sh
bash 24-bit-color.sh
```

![colors](https://user-images.githubusercontent.com/161548/128653955-45b190c8-a5b8-4c37-9a69-67551cd955ac.png)

## Configuration files

:warning: **IMPORTANT** :warning: _Don't_ set `$TERM` in your shell (zshrc, bashrc, etc.), but your terminal (alacritty).

### Alacritty

In `~/.config/alacritty/alacritty.yml`:

```yaml
env:
  TERM: xterm-256color
```

### tmux

In `~/.tmux.conf` (or `~/.config/tmux/tmux.conf`):

```tmux
set -g default-terminal "tmux-256color"
set -ag terminal-overrides ",xterm-256color:RGB"
```

### vim

In `~/.vimrc`:

```vim
" You might have to force true color when using regular vim inside tmux as the
" colorscheme can appear to be grayscale with "termguicolors" option enabled.
if !has('gui_running') && &term =~ '^\%(screen\|tmux\)'
  let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
  let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
endif

syntax on
set termguicolors
colorscheme yourfavcolorscheme
```

### neovim

> If you use `~/.vimrc` for your nvim configuration, use the above vim example because it's fully compatible.

In `~/.config/nvim/init.vim`

```vim
set termguicolors
colorscheme yourfavcolorscheme
```

Or `~/.config/nvim/init.lua`:

```lua
vim.o.termguicolors = true
vim.cmd'colorscheme yourfavcolorscheme'
```

## Not working correctly ?

Check out the [comments](https://gist.github.com/andersevenrud/015e61af2fd264371032763d4ed965b6#comments) below for possible solutions.

And if you found another solution I would really appreciate if you left a comment with instructions and the following information:

- OS/Distro + version
- Vim or Neovim + version
- Terminal name + version
