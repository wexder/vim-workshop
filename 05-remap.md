# Key remapping

One of the best features of vim is how easy it is to create custom keymaps and shorcuts. In "lua/cfg" create "remap.lua" and import it in "init.lua".
First lines will setup our "leader".
```lua
vim.g.mapleader = ' '
vim.g.maplocalleader = ' '

```
Leader is sort of our prefix for custom mappings and can be any key. But most people prefer <Space>.
We can set mapping in different modes.

Let's start with something easy.
```lua
vim.keymap.set("n", "<C-d>", "<C-d>zz")
vim.keymap.set("n", "<C-u>", "<C-u>zz")
```
We are saying that in "normal" mode we want to map the `<C-d>` and remap it to `<C-d>` which not only moves our cursor page down, but also will center the screen to that line.
The same with `<C-u>`.
Ok, so can we really remap anything ? Yes.
```lua
vim.keymap.set("n", "j", "<Up>")
vim.keymap.set("n", "k", "<Down>")
```
Let's say we want to change the direction in which default keymaps move up and down. We can do that.

It's annoying to type `:Ex` every time we want to open the explorer. Let's remap it.
```lua
vim.keymap.set("n", "<leader>e", ":Ex<cr>")
```

Other useful key mapping are for better window navigation.
```
vim.keymap.set("n", "<c-j>", "<c-w>j")
vim.keymap.set("n", "<c-k>", "<c-w>k")
vim.keymap.set("n", "<c-h>", "<c-w>h")
vim.keymap.set("n", "<c-l>", "<c-w>l")
```

But we can truly remap anything anywhere, we will see more remapping later.
