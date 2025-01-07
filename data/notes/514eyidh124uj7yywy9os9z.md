
My machine setup preferences.

## Programs

1. [Steermouse](https://plentycom.jp/en/steermouse/) - to set up mouse hot keys
2. [Rectangle](https://rectangleapp.com/) - Mac window snapping
3. [kitty](https://sw.kovidgoyal.net/kitty/) - better terminal
4. [bat](https://github.com/sharkdp/bat) - instead of `cat` for syntax highlighting and pretty print

5. [tmux](https://github.com/tmux/tmux/wiki) - terminal multiplexer
6. [vscode](https://code.visualstudio.com/) - for most languages and frameworks unless I need a really smart IDE then I would use intellij
7. [oh-my-zsh](https://ohmyz.sh/) - zsh config manager
8. [jq](https://stedolan.github.io/jq/) (optional, I only use this sometimes) - pretty printing json usually to pipe curl output

## Configuration files

### vim

```bash
filetype plugin indent on  " Load plugins according to detected filetype.
syntax on                  " Enable syntax highlighting.

colorscheme desert
set autoindent             " Indent according to previous line.
set expandtab              " Use spaces instead of tabs.
set softtabstop =4         " Tab key indents by 4 spaces.
set shiftwidth  =4         " >> indents by 4 spaces.
set shiftround             " >> indents to next multiple of 'shiftwidth'.
set number
set listchars=eol:¬,tab:>·,trail:~,extends:>,precedes:<
set list
set showmode               " Show current mode in command-line.

set incsearch              " Highlight while searching with / or ?.
set hlsearch               " Keep matches highlighted.

set cursorline             " Find the current line quickly.
```

## tmux

```bash
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix

# split panes using | and -
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %

# reload config file (change file location to your the tmux.conf you want to use)
bind r source-file ~/.tmux.conf

# Enable mouse mode (tmux 2.1 and above)
set -g mouse on

set -g history-limit 5000

set -g default-terminal "screen-256color"

```

## zhrc

```bash
# keep most of the file with some changes/ additions

ZSH_THEME="alanpeabody"

plugins=(
    git
     zsh-autosuggestions
)

## command line prompt -
## shows username, path and git branch details
parse_git_branch() {
    git branch 2> /dev/null | sed -n -e 's/^\* \(.*\)/[\1]/p'
}
COLOR_DEF='%f'
COLOR_USR='%F{243}'
COLOR_DIR='%F{197}'
COLOR_GIT='%F{39}'
NEWLINE=$'\n'
setopt PROMPT_SUBST
export PROMPT='${COLOR_USR}%n ${COLOR_DIR}%d ${COLOR_GIT}$(parse_git_branch)${COLOR_DEF}${NEWLINE}%% '

## default editor
export EDITOR=vim

# kitty - Fix issues with terminal navigation in tmux
bindkey "\e[1;3D" backward-word # ⌥←
bindkey "\e[1;3C" forward-word # ⌥→


# for JQ extention if using -  "null" is hard to see so change the colour
export JQ_COLORS='0;31:0;39:0;39:0;39:0;32:1;39:1;39'
```
