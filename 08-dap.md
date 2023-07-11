# DAP
Second protocol we will add is debug adapter protocol. It's similar in to LSP, but adds the debugging ability.
```lua
    use { 'mfussenegger/nvim-dap' }
    use { "rcarriga/nvim-dap-ui", requires = { "mfussenegger/nvim-dap" } }
```
I personally prefer endless prints over debugging, but some people like it. So here we go.
```lua
require("dapui").setup()

local dapui = require("dapui");
local dap = require("dap");
vim.keymap.set("n", "<leader>dt", function() dapui.toggle() end, nil)
vim.keymap.set("n", "<leader>dc", function() dap.continue() end, nil)
vim.keymap.set("n", "<leader>db", function() dap.toggle_breakpoint() end, nil)

dap.adapters.delve = {
  type = 'server',
  port = '${port}',
  executable = {
    command = 'dlv',
    args = {'dap', '-l', '127.0.0.1:${port}'},
  }
}

-- https://github.com/go-delve/delve/blob/master/Documentation/usage/dlv_dap.md
dap.configurations.go = {
  {
    type = "delve",
    name = "Debug",
    request = "launch",
    program = "${file}"
  },
  {
    type = "delve",
    name = "Debug test", -- configuration for debugging test files
    request = "launch",
    mode = "test",
    program = "${file}"
  },
  -- works with go.mod packages and sub packages 
  {
    type = "delve",
    name = "Debug test (go.mod)",
    request = "launch",
    mode = "test",
    program = "./${relativeFileDirname}"
  } 
}
```

This is example of configuration for delve, the golang debugger.
