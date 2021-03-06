All Things Regarding VIM
========================

## Commands to Remember

**Formating**
```
gU                              upper case
gu                              lower case
```

**Spellchecking**
```
zg                              add word to spell file
zw                              mark word as wrong
z=                              show possible corrections
```

**Macros**
```
q<letter><commands>q            record and store at <letter>
@<letter>                       run <letter>
@@                              repeat last macro
```

**Search & Replace**
```
:%s/\s\+$//                     remove white space at end of line
/\%2c<text>                     search for <text> in the 2nd column
```

**Misc**
```
CRTL-O                          go back
CRTL-]                          go in
:set list                       show tabs etc.
:arge                           open file and add to buffer list
gf                              open file under cursor
CRTL+w up/down                  switch between split windows
```

## Config Settings

Here you find a collection of useful stuff you can add to your `.vimrc` file

```vim
" copy into system clipboard
" see: http://stackoverflow.com/questions/1620018/vi-editor-copy-all-the-lines-to-clipboard
nnoremap <C-y> "+y
vnoremap <C-y> "+y
nnoremap <C-p> "+gP
vnoremap <C-p> "+gP

" resize split windows just by + and -
nmap - <C-W>-
nmap + <C-W>+

" execute open file
nmap <leader>e :w<CR>:!./%<CR>

" highlight the word under the cursor with a different color during searching
nmap <silent> n n:call HighlightNearCursor(@/)<CR>
nmap <silent> N N:call HighlightNearCursor(@/)<CR>
function HighlightNearCursor(pattern)
    " find word under cursor and in this word the search string
    let my_pattern="/\\k*\\%#\\k*\\&".a:pattern."/"
    execute 'match Todo ' my_pattern
endfunction
autocmd CursorMoved * match None

" when editing a file, always jump to the last cursor position
autocmd BufReadPost *
\ if line("'\"") > 0 && line ("'\"") <= line("$") |
\   exe "normal g'\"" |
\ endif
```

## Per File Config

You can add vim configuration settings directly to a given file by including a
corresponding line. Most of the time this is done at the end of the file.
You have to start the line as a comment, here is an C++ example
```C
// vim:softtabstop=2:shiftwidth=2:expandtab:textwidth=80:cindent
```

## Matlab Block Comments

Matlab has the possibility to comment a whole block by
```Matlab
%{
These are all commented.
function call, for loop, everything.
%}
```

The default syntax file of vim 7 does not highlight these.
Add the following lines to $VIM/syntax/matlab.vim after `syn match
matlabComment` line
```vim
syn region  matlabBlockComment        start=+%{+    end=+%}+
HiLink      matlabBlockComment        Comment
```

## License

Creative Commons Attribution ShareAlike 3.0  
http://creativecommons.org/licenses/by-sa/3.0/
