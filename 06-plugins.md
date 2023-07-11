# Plugins

The exciting part starts now. *Plugins*.... 

We will separate our plugin config to new file. Let's create "packer.lua". 
Packer is the de facto standard package manager for neovim. Even tho there's new kid on the block called "lazy.nvim".
For this tutorial we will be using Packer.
Of course we need to download the packer to use it. Here's [link](https://github.com/wbthomason/packer.nvim#quickstart) for it.
Either yank it and paste into the browser, or put your cursor over it and use `gx`. Now follow the instructions.

After we have installed packer we can start adding packages.

Packer packages are added inside the packer startup function using the provided "use" function.
```lua
return require('packer').startup(function(use)
end)
```

First we need to get rid of this ugly color scheme. Personally I like the onedark theme, let's add it.
```lua
    use {
        'navarasu/onedark.nvim',
    }
```
After you add this to you packer, save the file and with `:so` "source" the file.
This will effectively load this file into nvim config and we don't have to exit and enter nvim.
Note: This does not always work.
Packer does not automatically download our plugins, we need to tell it to do so with `:PackerSync`.
Packages are just git repositories so packer will clone and setup them for us.

But wait. The theme didn't change.
Well that's because we didn't setup our plugin. Oh boy, so many steps, but don't worry we are almost there.

Remember "after/plugin" folder, this is where is comes into play.
Let's create new file in there called "theme.lua" and setup our plugin. With most plugins you have to require it and call "setup".
```lua
require("onedark").setup({
    transparent = true, -- Show/hide background
})
```
So again save `:w` and source `:so` and??? Nothing....
Setting color scheme requires one more step.
```lua
require("onedark").load()
```
So now ? Yes. Our theme loaded. But wait how I'm supposed to know all of this?
You don't, nvim plugins are usually really well documented. Just take the plugin, you imported, prefix it with "github.com"
and voila, readme tells you everything you need to know.

Let's speed up a little bit.
```lua 
    use {
        'nvim-telescope/telescope.nvim', tag = '0.1.2',
        -- or                            , branch = '0.1.x',
        requires = { { 'nvim-lua/plenary.nvim' } }
    }
```
The best plugin for interactive search loved by almost all nvim users.
```lua
local builtin = require('telescope.builtin')

vim.keymap.set('n', '<leader>pf', builtin.find_files, {})
vim.keymap.set('n', '<leader>f', builtin.git_files, {})
vim.keymap.set('n', '<leader>ps', function()
    builtin.grep_string({ search = vim.fn.input("Grep > ") })
end)
vim.keymap.set('n', '<leader>st', builtin.live_grep, {})
vim.keymap.set('n', '<leader>b', builtin.buffers, {})
```
We setup some handy remaps, to help us find things easier.

Our editor has nice color scheme but still the code highlighting sucks.
Luckly treesitter, is our friend.
```lua
    use('nvim-treesitter/nvim-treesitter', { run = ':TSUpdate' })
    use('nvim-treesitter/playground')
    use { -- Additional text objects via treesitter
        'nvim-treesitter/nvim-treesitter-textobjects',
        after = 'nvim-treesitter',
    }
```
All of these plugins help nvim with highlighting, of course we will need to set it up.
```lua
require 'nvim-treesitter.configs'.setup {
    -- A list of parser names, or "all"
    ensure_installed = { "javascript", "typescript", "c", "lua", "rust", "go" },

    -- Install parsers synchronously (only applied to `ensure_installed`)
    sync_install = false,

    -- Automatically install missing parsers when entering buffer
    -- Recommendation: set to false if you don't have `tree-sitter` CLI installed locally
    auto_install = true,

    highlight = {
        -- `false` will disable the whole extension
        enable = true,
        -- Setting this to true will run `:h syntax` and tree-sitter at the same time.
        -- Set this to `true` if you depend on 'syntax' being enabled (like for indentation).
        -- Using this option may slow down your editor, and you may see some duplicate highlights.
        -- Instead of true it can also be a list of languages
        additional_vim_regex_highlighting = false,
    },
}
```

Last plugin we will show is the tree navigation.
```lua
    use {
        'nvim-tree/nvim-tree.lua',
        requires = {
            'nvim-tree/nvim-web-devicons', -- optional, for file icons
        },
        tag = 'nightly',                   -- optional, updated every week. (see issue #1193)
    }

```
With simple configuration.
```lua
require("nvim-tree").setup({})
```
This plugin has many configurations, but I'm trying to stop using it. It's more effective to just search for files with
telescope then trying to find them in tree view. Anyway you can open it with `:NvimTreeToggle` and you can create remaps
for it like.

```lua
vim.keymap.set('n', '<leader>e', "<CMD>NvimTreeToggle<CR>")
```


There is many many more plugins we can explore but let's move to lsp.
