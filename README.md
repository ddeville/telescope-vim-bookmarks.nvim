# telescope-vim-bookmarks.nvim

[Telescope](https://github.com/nvim-telescope/telescope.nvim) picker for the [vim-bookmarks](https://github.com/MattesGroeger/vim-bookmarks) plugin.

![](https://user-images.githubusercontent.com/13141438/117537521-c9153c00-b001-11eb-95fe-b8631a139647.png)

## Installation

Install with your favorite plugin manager and add

```lua
require('telescope').load_extension('vim_bookmarks')
```

somewhere after loading telescope.

## Usage

The extension provides two new pickers:

``` viml
" Pick from all bookmarks
:Telescope vim_bookmarks all
" Only pick from bookmarks in current file
:Telescope vim_bookmarks current_file
```

Lua equivalent:

``` lua
require('telescope').extensions.vim_bookmarks.all()
require('telescope').extensions.vim_bookmarks.current_file()
```

## Customization

Both pickers take a table of options that you can use to customize them.
Here's a list of available options along with their default values:

| Option            | Explanation                                                         | Default Value                            |
| ---               | ---                                                                 | ---                                      |
| `prompt_title`    | Title of the search prompt                                          | 'vim-bookmarks'                          |
| `attach_mappings` | See following section                                               | {}                                       |

Additionally, the table of options is passed on to your configured `qflist_previewer` and `generic_sorter` (See Telescope docs for details)

## Actions

The extension also provides custom actions for managing bookmarks:

| Action                         | Explanation
| ---                            | ---
| `delete_at_cursor`             | Deletes the bookmark at current cursor position
| `delete_selected`              | Deletes all bookmarks selected via Telescope's multi-selection
| `delete_selected_or_at_cursor` | If there's a multi selection, delete those bookmarks, otherwise delete the one at the curso position
| `delete_all`                   | Deletes all bookmarks (Same as `:BookmarkClearAll`)

For example:

```lua
local bookmark_actions = require('telescope').extensions.vim_bookmarks.actions
require('telescope').extensions.vim_bookmarks.all {
    attach_mappings = function(_, map)
        map('n', 'dd', bookmark_actions.delete_selected_or_at_cursor)

        return true
    end
}
```
