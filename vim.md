## vim

#### Buffers

###### List buffers
    :ls

###### Show open buffers
    :buffers

###### Switch to buffer 1
    :b1

###### Switch to the next buffer
    :bn

###### Switch to the previous buffer
    :bp


###### Delete the current buffer
    :bd


###### Delete the current buffer (without saving changes)
    :bd!


## Windows

###### Open a new window
    :new

###### Open a new window with a particular file
    :new filename


###### Close a window/split
control+w, q

###### Open a new window, but with the same file as the other buffer
  ```:split```

or:

  ````:vsplit```


## Tabs
###### Create a new tab
    :tabnew


###### Create a new tab, open a file
    :tabnew filename.txt


###### Open files in individual tabs
    vim -p file1 file2 file3


###### Move tab to position n
    :tabm n


###### Switch to next tab
    :tabn


###### Switch to previous tab
    :tabp


###### Switch to next tab (normal mode)
    gt - Next tab


###### Switch to previous tab (normal mode)
    gT - Previous tab


#### Command Mode commands
###### Create a new buffer:
    :e filename


###### Move to the next buffer:
    :bn


###### Move to the previous buffer:
    :bp


###### Delete a buffer:
    :bd


#### Normal Mode commands


###### Show position and status
ctrl-G


###### Move to the end of the file
    G


####### Move to the beginning of the file
    gg


###### Move to the beginning of the paragraph
{


###### Open a line one line below, enter insert mode
    o


###### Open a line one line above, enter insert mode
    O


###### Move to the end of the paragraph:
}


###### Move to the beginning of the sentence:
(


###### Move to the end of the sentence:
)


###### Move to the beginning of the line:
0


###### Move to the beginning of the next word:
w


###### Move to the beginning of the previous word:
b


###### Move to the beginning of the current word:
e


###### Replace a single character with <x>
r<x>


###### Move to first declaration of an item
gd



###### Replace text (but prompt each time)
    :%s/old/new/gc


###### Delete from the cursor to the next word
    dw

###### Delete from the cursor to the end of the line
    d$


###### Delete the current line
    cc


###### Delete from the cursor to the next word
    ce


###### Delete from the cursor to the end of the line
    c$


###### Delete everything in single quotes
    ci'


###### Delete everything in double quotes
    ci"


###### Execute a shell command
    :! <command>


#### Searching

###### Conduct a search
    /


###### Search backwards
Use ? instead of /


###### Repeat the last search
Use ?? or //


###### Move to next search result:
    n


###### Move to previous search result:
    N


###### Find matching parentheses or brackets
    %


#### Tips & Tricks


###### Go to a file
Highlight file and type gf


###### Open a file in a new window
    CTRL-w,f


###### Open a file in a new tab
    CTRL-w,gf


###### Move to a specific line
    501G


###### Run a command multiple times in command mode
Place a number in front of the command. For example:
  ```64dd```


###### Sort lines alphabetically:
	1. v for visual select
	2. down arrow to highlight lines
	3. :sort ui


###### Insert output of a command into the file
    `:r! pwd`


###### Insert existing file
    `:r /etc/passwd`


###### Useful submodules:
    $ git submodule add https://github.com/tpope/vim-pathogen.git vim/bundle/pathogen
    $ git submodule add https://github.com/scrooloose/syntastic vim/bundle/syntastic
    $ git submodule add https://github.com/scrooloose/nerdtree.git vim/bundle/nerdtree
