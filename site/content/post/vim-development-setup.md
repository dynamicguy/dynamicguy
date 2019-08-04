---
title: Vim development setup
date: 2019-08-04T17:48:27.386Z
description: Vim setup for development
image: /img/vim.png
---
Save the following contents in a bash script and execute it.
```
#!/bin/bash

mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim

if [ ! -d ~/.vim/bundle/nerdtree ]; then
    git clone https://github.com/scrooloose/nerdtree.git ~/.vim/bundle/nerdtree
fi

touch proper.vimrc

echo "filetype plugin indent on" >> proper.vimrc
echo "syntax on" >> proper.vimrc
echo "set hlsearch" >> proper.vimrc
echo "autocmd BufRead,BufNewFile *.ejs set filetype=html" >> proper.vimrc
echo "autocmd BufRead,BufNewFile *.twig set filetype=html" >> proper.vimrc
echo "" >> proper.vimrc
echo "set tabstop=4" >> proper.vimrc
echo "set softtabstop=4" >> proper.vimrc
echo "set shiftwidth=4" >> proper.vimrc
echo "set expandtab" >> proper.vimrc
echo "set autoindent" >> proper.vimrc
echo "set smarttab" >> proper.vimrc
echo "" >> proper.vimrc
echo "set splitright" >> proper.vimrc
echo "" >> proper.vimrc
echo "set foldmethod=indent" >> proper.vimrc
echo "set foldnestmax=10" >> proper.vimrc
echo "set nofoldenable" >> proper.vimrc
echo "set foldlevel=1" >> proper.vimrc
echo "" >> proper.vimrc
echo "set clipboard=unnamed" >> proper.vimrc
echo "" >> proper.vimrc
echo "vnoremap <C-r> \"hy:%s/<C-r>h//gc<left><left><left>" >> proper.vimrc
echo "" >> proper.vimrc
echo "call pathogen#infect()" >> proper.vimrc
echo "" >> proper.vimrc
echo "map <F2> :NERDTreeToggle<CR>" >> proper.vimrc
echo "map <F3> :noh<CR>" >> proper.vimrc

mv -i proper.vimrc  ~/.vimrc
rm -f proper.vimrc   
```
