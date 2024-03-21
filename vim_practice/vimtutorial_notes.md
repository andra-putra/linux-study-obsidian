# New things learned so far:
I - Enter at beginning of line
A - Enter at end of line
O - Enter above current line
:set number - Toggles number lines in normal vim
:set nu - Shorter for above
:set relativenumber - Number lines but relative to current cursor location
:set rnu - Shorter for above
:set mouse - Toggles mouse
:colorscheme (color here) - Changes colorscheme
w - Moves 1 word (seperated by apostrophes, etc.)
W - Moves 1 word (only seperated by space)
ci" - Replaces everything inside "
ciw - Replaces everything inside word
ci( - Replaces everything inside brackets and so on
% - Move to matching bracket, quotes, etc.
t - Move to before next input (e.g. t" moves to before next quote mark)
f - Same as above, but goes to that line
>> - Indent line
<< - De-indent line
v - Go to visual selection mode
shift + V - Go to visual line selection mode (selects whole lines)
ctrl + v - Go to visual block mode (do things with multiple lines at a time)
= - Auto indent a line (for javascript, etc.)
/ - Search (n for next result, N for prev result). To reset, just type garble in research
* - Go to next occurance of current word
Hahstag - Go to prev occurance of current word
m + any char - Make a bookmark in file
' + any char - Go to bookmark in file
zz - center this line on screen
:%s/x/y/g - Replace all instances of x in file with y
Select text + s/x/y/g - Replace instances of x inside selected with y
. - Repeats last command you did
:reg - View registers (clipboard thing)
"xp - (Replace x with register number) Pastes from register
"+p - Pastes from OS clipboard
qx - (Replace x with any key) Records a macro to x key. Stop recording by Esc + q
@x - (Replace x with any key) Executes macro bound to x key
gc - Comment out selected
gcc - Comment out line

# To make changes permanent:
Change ~/.vimrc (note: doesn't work for nvim, use ~/.config/nvim/init.vim)


# ------------ Testing Area Below ------------
Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.
Banked
| Title    | Name of Town    | Population |
|---------------- | --------------- | --------------- |
| Item1.1    | Item2.1    | Item3.1    |
| Item1.2    | Item2.2    | Item3.2    |

("Hello world I want to delete this message") Macro executed
printf("Hello world", 123, 12.7, "yeah what")
printf("Hello world")
printf("Hello world", 123, 12.7, "yeah what")
printf("Hello world", 123, 12.7, "yeah what")

