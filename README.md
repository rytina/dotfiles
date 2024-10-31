# Dotfiles Repository

This repository is intended to share my dotfiles which I created during my learnings of Linux and the GNU tools.

## Vundle Installation and Plugin Management

Vundle is a plugin manager for Vim. To install Vundle, follow these steps:

1. Open a terminal and run the following command to clone the Vundle repository:
   ```
   git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
   ```

2. Add the following lines to your `.vimrc` file to set up Vundle:
   ```
   set nocompatible              " be iMproved, required
   filetype off                  " required

   " set the runtime path to include Vundle and initialize
   set rtp+=~/.vim/bundle/Vundle.vim
   call vundle#begin()

   " let Vundle manage Vundle, required
   Plugin 'VundleVim/Vundle.vim'

   " Add your plugins here
   Plugin 'preservim/nerdtree'
   Plugin 'tpope/vim-fugitive'
   Plugin 'Konfekt/vim-wsl-copy-paste'

   call vundle#end()            " required
   filetype plugin indent on    " required
   ```

3. Save the changes to your `.vimrc` file and run the following command in Vim to install the plugins:
   ```
   :PluginInstall
   ```

## Using Autocommands

Autocommands in Vim allow you to execute commands automatically in response to specific events. Here are some examples of how to use autocommands:

1. Highlight specific words in files with a `.tid` extension:
   ```
   if has("autocmd")
     autocmd BufRead,BufNewFile *.tid syntax match InnovationGroup "\<[Ii]nnovat\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match MindfulGroup "\<[Mm]indful\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match HonorGroup "\<[Hh]onor\>"
     autocmd BufRead,BufNewFile *.tid syntax match ResponsibilityGroup "\<[Rr]esponsib\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match CultureGroup "\<[Cc]ultur\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match InspireGroup "\<[Ii]nspir\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match FulfillmentGroup "\<[Ff]ulfillment\>"
     autocmd BufRead,BufNewFile *.tid syntax match HappinessGroup "\<[Hh]appiness\>"
     autocmd BufRead,BufNewFile *.tid syntax match SuccessGroup "\<[Ss]uccess\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match LearnGroup "\<[Ll]earn\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match TrustGroup "\<[Tt]rust\w*\>"
     autocmd BufRead,BufNewFile *.tid syntax match ShareGroup "\<[Ss]hare\>"
   endif
   ```

2. Change the color of the cursor line when entering and leaving insert mode:
   ```
   if has("autocmd")
     " Change Color when entering Insert Mode
     autocmd InsertEnter * highlight  CursorLine ctermfg=NONE

     " Revert Color to default when leaving Insert Mode
     autocmd InsertLeave * highlight  CursorLine ctermfg=LightBlue
   endif
   ```

3. Set UTF-8 as the default encoding for commit messages:
   ```
   if has("autocmd")
     autocmd BufReadPre COMMIT_EDITMSG,MERGE_MSG,git-rebase-todo setlocal fileencodings=utf-8
   endif
   ```

4. Remember the positions in files with some git-specific exceptions:
   ```
   if has("autocmd")
     autocmd BufReadPost *
       \ if line("'\"") > 0 && line("'\"") <= line("$")
       \           && &filetype !~# 'commit\|gitrebase'
       \           && expand("%") !~ "ADD_EDIT.patch"
       \           && expand("%") !~ "addp-hunk-edit.diff" |
       \   exe "normal g`\"" |
       \ endif
   endif
   ```

5. Set the filetype to `diff` for files with a `.patch` extension:
   ```
   if has("autocmd")
     autocmd BufNewFile,BufRead *.patch set filetype=diff
   endif
   ```

6. Highlight trailing whitespace in diff files:
   ```
   if has("autocmd")
     autocmd Filetype diff
       \ highlight WhiteSpaceEOL ctermbg=red |
       \ match WhiteSpaceEOL /\(^+.*\)\@<=\s\+$/
   endif
   ```
