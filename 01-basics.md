# Basics

Vim is terminal text editor. It was created as clone of the "vi" editor and it stand for "Vi IMproved". 
Initially created in 1991 with latest stable release in 2022. But we are not here to talk about vim.
We want to learn how to use it.

Since everything is controlled with keyboard vim needs to distinguish between when you want to move and edit.
The three basic modes are
- Normal
- Insert
- Visual

Normal mode is for moving around the editor. For basic movements we use
- h = left
- l = right
- k = up
- j = down

But we cannot type in normal mode. For that we have to switch to the insert mode.
To do that just press `i` for "insert". This will place your cursor before the current character and you can type away.
But what if you want to type after the current character? Easy just use `a`.
You can also see you are in the `insert` mode on the bottom of the editor.

To exit the `insert` mode just press `esc`. Sorry for the mac users, we will change this later.

Now we have this annoying long strip we want to skip around to get the next section, to do this we can just press the `j` key few times.
Or we can say we want to move 20 lines down, by typing `21j`.

################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################
################################################################################################

Next mode is has three different submodes. We can nicely show the difference between then by working with this strip.
When you want to select some text in vim, you need to enter the visual mode. This is done by using the `v` key. 
But what if you want to select whole lines, you can move you cursor to the end of the line and again press `v`, or you can just use the `V`. 
The last submode for "visual" mode is the block mode, you can try it by pressing `Ctrl-V`.

Last and perhaps the most important mode is the "command" mode. We will dive in that more later, but for now you can enter "command" mode by pressing `:`.
This will create input at the bottom of the screen, where you can execute commands. For how the most important commands are 'write' and 'quit'.
But that's just too long to type, so we can just enter command 'w' to safe current buffer, and 'q' to exit the editor.
