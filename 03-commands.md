# Commands

Yes you can command your editor.
With jokes aside, commands are important in vim, without them you wouldn't be able to even exit the editor.
As already said, "command" mode can be entered from "normal" mode with `:`.

To exit editor we use `q`, but before we leave it's important to safe current file with `w`. 
We can force both of these commands with `!` after the first character, like `:q!` or `:q!`.
For swift exit combination of commands can also be used `:wq`.
Opening some other file is easy with `:e` followed by path to the file we want to open.

What if we want to find some file, because we don't know how's the file called ?
No worry vim has build in file explorer with `:Explorer` or the shortcut `:Ex`.

Other useful commands are `:split` and `:vsplit` to split the current buffer.
Wait buffer ? What's that.
To put it simply vim creates in memory copy of the file and sync it only with `:w`, so the in memory copy is called buffer.
But buffers don't need to be only files, the explorer is also buffer. Or help `:help` is also buffer.
Yes there's a whole documentation right inside the editor. If you don't know how to use something just use help, like `:help :w`.

Now let's get to more powerfull commands. Probably the most used is command for substitution in the same buffer.
The base command for substitution is `s` but on it's own it's useless.
This will combine few things and then explain them. To replace the word "commands" with "funny words" we can use
`:%s/commands/funny words/g`
Ok let's break it down. The substitution command work the same way as sed linux command.
The first we need to select `:range` where we want to perform the substitution. The help command can help us 
with that `:help :range`.
The the `s` for substitution. After that we have the delimiter, we can use any simple non alphanumeric character but usually "/" is used.
Next is the pattern we want to substitu, in this case "commands" but any regexp with work, like `co\D\Da\Dds`. 
After second delimiter we have the string to be replaced with. Last delimiter delimits the flags, here are some usefull ones:
- c = Confirm each substitution
- g = Replace all occurrences in the line
- i = Ignore cases for pattern
- I = Don't ignore cases for pattern
- n = Reports number of matches, but doesn't substitute

For more about substitution `:help :s`.

We can also use the `:sort` command to sort range. Like `:'<,'>sort`.
4. Of
3. List
2. is
5. Randomness
1. This

There's probably much more usefull commands. But this is the one's I use the most.
