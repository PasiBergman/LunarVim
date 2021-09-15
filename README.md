![LunarVim Demo](./utils/media/lunarvim_logo_dark.png)

<div align="center"><p>
    <a href="https://github.com/lunarvim/LunarVim/releases/latest">
      <img alt="Latest release" src="https://img.shields.io/github/v/release/lunarvim/LunarVim" />
    </a>
    <a href="https://github.com/lunarvim/LunarVim/pulse">
      <img alt="Last commit" src="https://img.shields.io/github/last-commit/lunarvim/LunarVim"/>
    </a>
    <a href="https://github.com/lunarvim/LunarVim/blob/main/LICENSE">
      <img src="https://img.shields.io/github/license/lunarvim/lunarvim?style=flat-square&logo=GNU&label=License" alt="License"
    />
    <a href="https://patreon.com/chrisatmachine" title="Donate to this project using Patreon">
      <img src="https://img.shields.io/badge/patreon-donate-yellow.svg" alt="Patreon donate button" />
    </a>
    <a href="https://twitter.com/intent/follow?screen_name=chrisatmachine">
      <img src="https://img.shields.io/twitter/follow/chrisatmachine?style=social&logo=twitter" alt="follow on Twitter">
    </a>
</p>	

</div>

## Documentation

You can find all of the documentation for Lunarvim at [lunarvim.org](https://www.lunarvim.org)

## Install In One Command!

Make sure you have the release version of Neovim (0.5).

If you have previously installed LunarVim, make sure to remove `/usr/local/bin/lvim`, as we've moved the launcher to `~/.local/bin/lvim`

``` bash
bash <(curl -s https://raw.githubusercontent.com/lunarvim/lunarvim/master/utils/installer/install.sh)
```

## Install Language support

- Enter `:LspInstall` followed by `<TAB>` to see your options for LSP

- Enter `:TSInstall` followed by `<TAB>` to see your options for syntax highlighting

**NOTE** I recommend installing `lua` for autocomplete in `config.lua`


![Demo1](./utils/media/demo1.png)
![Demo2](./utils/media/demo2.png)
![Demo3](./utils/media/demo3.png)

## Configuration file

To install plugins configure LunarVim use the `config.lua` located here: `~/.config/lvim/config.lua`

Example:

```lua
-- general
lvim.format_on_save = true
lvim.colorscheme = "onedarker"

lvim.leader = "space"
-- add your own keymapping
lvim.keys.normal_mode["<C-s>"] = ":w<cr>"
-- unmap a default keymapping
-- lvim.keys.normal_mode["<C-Up>"] = ""
-- edit a default keymapping
-- lvim.keys.normal_mode["<C-q>"] = ":q<cr>"
-- set keymap with custom opts
-- lvim.keys.insert_mode["po"] = {'<ESC>', { noremap = true }}

-- Use which-key to add extra bindings with the leader-key prefix
-- lvim.builtin.which_key.mappings["P"] = { "<cmd>Telescope projects<CR>", "Projects" }

-- Configure builtin plugins
lvim.builtin.dashboard.active = true
lvim.builtin.terminal.active = true

-- Treesitter parsers change this to a table of the languages you want i.e. {"java", "python", javascript}
lvim.builtin.treesitter.ensure_installed = "maintained"
lvim.builtin.treesitter.ignore_install = { "haskell" }

-- Disable virtual text
lvim.lsp.diagnostics.virtual_text = false

-- set a formatter if you want to override the default lsp one (if it exists)
lvim.lang.python.formatters = {
  {
    exe = "black",
    args = {}
  }
}
-- set an additional linter
lvim.lang.python.linters = {
  {
    exe = "flake8",
    args = {}
  }
}


-- Additional Plugins
lvim.plugins = {
    {"lunarvim/colorschemes"},
    {"folke/tokyonight.nvim"}, {
        "ray-x/lsp_signature.nvim",
        config = function() require"lsp_signature".on_attach() end,
        event = "InsertEnter"
    }
}
```

## Updating LunarVim

In order to update you should be aware of three things `Plugins`, `LunarVim` and `Neovim`

To update plugins:

```
:PackerUpdate
```

To update LunarVim:

```bash
cd ~/.local/share/lunarvim/lvim && git pull
:PackerSync
```
## Known Issues
If you get either of the following errors
- init.lua:6: module 'bootstrap' not found:
- /home/user/.config/nvim/config.lua not found, falling back to /home/user/.config/nvim/lv-config.lua

Try the following:
```bash
which lvim
# if output is /usr/local/bin/lvim remove it
sudo rm /usr/local/bin/lvim

which lvim
# if output is ~/.local/bin/lvim, open lvim and run :PackerSync.  That should get you to a working state

# otherwise if `which lvim` returns `not found`, 
Make sure the `lvim` file exists in `~/.local/bin/lvim`.  
If the file exists,make sure `~/.local/bin` is in your PATH.  If not, [add it](https://www.lunarvim.org/02-after-install.html#add-lvim-to-path)
either reinstall again or manually add the lunarvim launcher

If the file doesn't exist, create the file
cd ~/.local/bin
touch lvim
chmod 755 lvim
```

And then add the following to the lvim file you created.  Replace all `torvalds` with your user name

```bash
#!/bin/sh

export LUNARVIM_CONFIG_DIR="${LUNARVIM_CONFIG_DIR:-/home/torvalds/.config/lvim}"
export LUNARVIM_RUNTIME_DIR="${LUNARVIM_RUNTIME_DIR:-/home/torvalds/.local/share/lunarvim}"

exec nvim -u "$LUNARVIM_RUNTIME_DIR/lvim/init.lua" "$@"

```

## Resources

- [Documentation](https://www.lunarvim.org)

- [YouTube](https://www.youtube.com/channel/UCS97tchJDq17Qms3cux8wcA)

- [Discord](https://discord.gg/Xb9B4Ny)

- [Twitter](https://twitter.com/chrisatmachine)

## Testimonials

> "I have the processing power of a potato with 4 gb of ram and LunarVim runs perfectly."
> - @juanCortelezzi, LunarVim user.

> "My minimal config with a good amount less code than LunarVim loads 40ms slower. Time to switch."
> - @mvllow, Potential LunarVim user.

<div align="center" id="madewithlua">
	
[![Lua](https://img.shields.io/badge/Made%20with%20Lua-blue.svg?style=for-the-badge&logo=lua)](#madewithlua)
	
</div>
