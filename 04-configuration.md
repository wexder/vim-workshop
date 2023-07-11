# Configuration

This is where different distribution of vim differs.
Currently the most popular vim distribution is nvim. It's because of two things.
Neovim is fork of vim with better multithread support 
And latest vim version switched to completely new configuration language, but Neovim
is using the battle tested plugin/configuration language "Lua".

We will be focusing just on the Neovim Configuration.

To start we can look at where nvim looks for configuration `:h rtp`. For us is important the "$XDG_CONFIG_HOME/nvim" and  "$XDG_CONFIG_HOME/nvim/after".
They basically translate to "~/.config/nvim" and "~/.config/nvim/after". The first file nvim is looking for is the "init.lua".

As I said nvim is configured with lua and every good developer starts with hello world when
learning new language.
```lua
print("Hello nvim")
```
Now quit nvim and open it again to reload the config. You should see the text "Hello nvim" at
the bottom of the editor.

To make our configuration nicer, we can create few folders.
```tree
.
├── after
│   └── plugin
├── init.lua
├── lua
│   └── cfg
│       ├── init.lua
```

It's simple all configurations go into "lua/cfg". This will include our key remapping, plugin definitions
and of course editor configurations. "after/plugin" will contain all configurations related to plugin setup.
In "ini.lua" we have to import our "lua/cfg". To do that, add
```lua
require("cfg")
```
this imports the "lua/cfg/init.lua" file. From there we will need to add another require for each file in the "lua/cfg" directory.


First we will configure the editor, for this create "set.lua" file in "lua/cfg/set.lua" and import it. 
Some sane configurations around tab are required. If you don't agree with using tabs, just find some config that works for you.
```lua
vim.opt.tabstop = 4
vim.opt.softtabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true
vim.opt.pumheight = 20
```

It's hard to navigate with relative jumps when you don't see line numbers.
```lua
vim.opt.nu = true
vim.opt.relativenumber = true
vim.opt.wrap = false
```
Turning on the line number, and then relative numbers to make jumping around easier.
Current line number is displayed on the same line, and relative to that number of lines you have to move to get there.
Also turn of the wrapping of long lines.

```lua
vim.opt.hlsearch = false
vim.opt.incsearch = true
```
Hlsearch to turn off the highlight after search. And incsearch follow the current search pattern along the buffer.

```lua
vim.opt.scrolloff = 8
```
When scrolling is annoying to be scrolling at the edge of the screen,
with this we can configure to start scrolling before we reach the end.

Yanking is not visible by default and I prefer my yanks visible.
```lua
local highlight_group = vim.api.nvim_create_augroup('YankHighlight', { clear = true })
vim.api.nvim_create_autocmd('TextYankPost', {
    callback = function()
        vim.highlight.on_yank()
    end,
    group = highlight_group,
    pattern = '*',
})
```

Lastly to fix our clipboard issue, we tell nvim to use the OS clipboard.
```lua
vim.opt.clipboard = "unnamedplus"

```
This option uses variety of tools to operate the OS clipboard. To see all of the `:help provider-clipboard clipboard`.
