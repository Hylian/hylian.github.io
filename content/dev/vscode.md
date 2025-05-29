+++
title="VS Code for Hopeless Vim Users"
date=2023-02-19
transparent=true
+++

## Why VS Code?

### You Can Still Use Neovim

The neovim extension runs an actual neovim instance! With your nvim config! Since it's an actual neovim instance, you'll never run into weird edge cases of specific vim features that haven't been implemented.

### It's Configurable

The VS Code defaults did not work for me at all, but there's a good amount of configurability. Combined with the neovim plugin, it's possible to tinker your way into a cozy environment.

### Remote Workflow

After switching to a remote server workflow, vim in a ssh session felt like a chore. Input latency was noticeably worse, launching new sessions in i3/sway was slower, and I didn't want to live inside of a tmux session. VS Code Remote hides the latency with local buffers, and is able to resume sessions from a broken SSH connection.

### Language Server Support

coc.nvim is great and all, but VS Code's out-of-box Language Server support is really well integrated. Displaying type annotations in-line, symbol/outline search, type documentation, renaming, completion- it all *Just Works(tm)*. Really nice, especially when writing C++ or Rust.

### Diff/Merge Tooling

Even after lots of tinkering with plugins, using Vim for diffs and merges always felt clunky to me. VS Code's side-by-side view is super nice, and can be used as your git difftool and merge tool. Just clicking a button to revert a single line/hunk or accept both changes in a merge is really refreshing.

### Easy Splits

Being a GUI editor, panes and splits feel a lot more freeform than in Vim. You can easily move editors between split panes, create new ones, and create tabs within a pane.

### Remote Terminal

The terminal is nice to have in a VS Code Remote session. It might not be `$YOUR_FAVORITE_TERMINAL_EMULATOR`, but it's perfectly serviceable.

## Getting Started

### Install VS Code

Install VS Code on your server and local machine.

### Install Neovim Extension

https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim

The plugin requires neovim v0.8.0 or greater. If your distro's repo does not have a recent neovim version, install the appimage release manually:

```
mkdir -p $HOME/.local/bin
wget https://github.com/neovim/neovim/releases/download/stable/nvim.appimage -O $HOME/.local/bin/nvim
chmod u+x $HOME/.local/bin/nvim
```

## Configure Neovim 

Spend some time reading through the README for the extension, it's very thorough.

### Extension Configuration

Open User Settings (`Ctrl+Shift+P > "Open User Settings`):

```
Neovim Executable Paths: Linux: ~/.local/bin/nvim
```

Make sure you add the following to `settings.json` (Ctrl+Shift+P > "Open User Settings (JSON)"):

```
"extensions.experimental.affinity": {
    "asvetliakov.vscode-neovim": 1
},
```

### `init.vim` Configuration

The extension will use the same `init.vim` configuration as your regular neovim instance. This means that you will need to modify your config to exclude nvim plugin loading when in VS Code, and can also bind specific keybinds for VS Code only.

You can do this by wrapping lines in this if statement:

```
if !exists('g:vscode')
  ...
endif
```

I highly recommend gating loading of your neovim plugins and lua scripts when in vscode mode.

You can also invoke VS Code commands and set them to keybinds:

```
nmap { :call VSCodeCall('workbench.action.showAllSymbols')<CR>
```

However, note that the bindings in VS Code can take precedence over the neovim ones, and you should read on to the Keybindings section before going to town with your binds.

## Keybindings

VS Code has a robust, if overly complex, system for setting keybindings. They can be configured via the GUI or JSON:

```
Ctrl + Shift + P > Open Keyboard Shortcuts
Ctrl + Shift + P > Open Keyboard Shortcuts (JSON)
```

There is a huge pile of default bindings that are generally focused on chords or function keys. Deleting bad default binds and creating your own is key to a cozy experience. Every time a keybind doesn't do what you want, or you want to do something with a keybind, I recommend spending a minute to open up the shortcut editor and configuring it. It took me a couple weeks to finally get all the keybinds to what I want.

The keybindings set in VS Code will always take precedence over keybindings set in neovim. 

Most of the following sections will focus on keybindings that I found useful. My bindings are weird and for my Ergodox setup, but will hopefully be useful as a starting point for your config.

### When Clauses

https://code.visualstudio.com/api/references/when-clause-contexts

VS Code has a lot of different modalities, with different types of panes that can be visible and focused on. To deal with this, keybindings evaluate `when clause` expressions to only apply in certain contexts. You could have a single key combination that has multiple bindings depending on what is focused or even visible on the screen.

#### Neovim When Clauses

The Neovim extension exposes `when clause` contexts that can be used for keybinds. These are very useful for creating bindings that only run when neovim is in `NORMAL` mode.

eg. `editorTextFocus && neovim.init && neovim.mode == 'normal'`

#### Useful When Clauses

Clause                                     | Description
------                                     | -----------
editorFocus                                | Focus is on a text editor
editorTextFocus                            | Text in an editor has focus
inputFocus                                 | Any text input has focus (including GUI menus)
listFocus                                  | Focus is on a GUI list
findWidgetVisible                          | Find widget is visible
terminalFocus                              | Terminal is focused
searchViewletVisible                       | Search viewlet is visible (side pane search)
sideBarVisible                             | Sidebar is visible
sideBarFocus                               | Sidebar is focused
focusedView                                | Currently focused view
neovim.init                                | Neovim is initialized
neovim.mode                                | The current vim mode
activeViewlet == 'workbench.view.explorer' | Explorer is visible in the side pane
activeViewlet == 'workbench.view.search'   | Search is visible in the side pane

### Useful Keybindings

#### Navigate Panes

Use `Alt + h/j/k/l` to navigate between any panes on the screen. You can go between side pane, editors, and terminal with the same binds.

```
  {
    "key": "alt+h",
    "command": "workbench.action.navigateLeft"
  },
  {
    "key": "alt+l",
    "command": "workbench.action.navigateRight"
  },
  {
    "key": "alt+k",
    "command": "workbench.action.navigateUp"
  },
  {
    "key": "alt+j",
    "command": "workbench.action.navigateDown"
  },
```

#### Move an Editor

Use `Ctrl + h/j/k/l` to move an editor. If an editor group exists in the move location, it will turn into a tab in the group. If there is no group, a new split will be created.

```
  {
    "key": "ctrl+k",
    "command": "workbench.action.moveEditorToAboveGroup",
    "when": "editorFocus && !inQuickOpen && !listFocus && focusedView != 'workbench.view.search'"
  },
  {
    "key": "ctrl+j",
    "command": "workbench.action.moveEditorToBelowGroup",
    "when": "editorFocus && !inQuickOpen && !listFocus && focusedView != 'workbench.view.search'"
  },
  {
    "key": "ctrl+h",
    "command": "workbench.action.moveEditorToLeftGroup",
    "when": "editorFocus && !inQuickOpen && !listFocus && focusedView != 'workbench.view.search'"
  },
  {
    "key": "ctrl+l",
    "command": "workbench.action.moveEditorToRightGroup",
    "when": "editorFocus && !inQuickOpen && !listFocus && focusedView != 'workbench.view.search'"
  },
```

#### Switch Tabs

Change tabs with `Shift + h/j/k/l` in `NORMAL` mode.

```
  {
    "key": "shift+j",
    "command": "workbench.action.nextEditorInGroup",
    "when": "editorFocus && neovim.mode == 'normal'"
  },
  {
    "key": "shift+k",
    "command": "workbench.action.previousEditorInGroup",
    "when": "editorFocus && neovim.mode == 'normal'"
  },
  {
    "key": "shift+h",
    "command": "workbench.action.previousEditorInGroup",
    "when": "editorFocus && neovim.mode == 'normal'"
  },
  {
    "key": "shift+l",
    "command": "workbench.action.nextEditorInGroup",
    "when": "editorFocus && neovim.mode == 'normal'"
  },
```

#### Move Tab

Move tab ordering within its editor group with `Ctrl + Shift + h/j/k/l`.

```
  {
    "key": "ctrl+shift+j",
    "command": "-workbench.action.search.toggleQueryDetails",
    "when": "inSearchEditor || searchViewletFocus"
  },
    {
    "key": "ctrl+shift+k",
    "command": "search.action.focusPreviousSearchResult",
    "when": "hasSearchResult && activeViewlet == 'workbench.view.search'"
  },
    {
    "key": "ctrl+shift+h",
    "command": "workbench.action.moveEditorLeftInGroup",
    "when": "editorFocus && neovim.mode == 'normal'"
  },
    {
    "key": "ctrl+shift+l",
    "command": "workbench.action.moveEditorRightInGroup",
    "when": "editorFocus && neovim.mode == 'normal'"
  },
```

#### Toggle Terminal

Press `Ctrl + ]` to toggle terminal visibility.

```
  {
    "key": "ctrl+]",
    "command": "workbench.action.terminal.toggleTerminal"
  },
```

#### Toggle Terminal Maximization

Press `Ctrl + f` to maximize terminal pane when focused.

```
  {
    "key": "ctrl+f",
    "command": "workbench.action.toggleMaximizedPanel",
    "when": "terminalFocus"
  },
```

#### Terminal Key Passthrough

Pass-through certain keybinds to the terminal to ensure they aren't grabbed by other keybinds.

```
  {
    "key": "ctrl+e",
    "command": "ctrl+e",
    "when": "terminalFocus"
  },
  {
    "key": "ctrl+t",
    "command": "ctrl+t",
    "when": "terminalFocus"
  },
  {
    "key": "ctrl+j",
    "command": "ctrl+j",
    "when": "terminalFocus"
  },
  {
    "key": "ctrl+k",
    "command": "ctrl+k",
    "when": "terminalFocus"
  },
  {
    "key": "ctrl+r",
    "command": "ctrl+r",
    "when": "terminalFocus"
  },
```

#### Toggle Sidebar

Press `Ctrl + b` for three way sidebar toggle.

 * If sidebar is hidden, show and focus it.
 * If sidebar is visible and not focused, focus it.
 * If sidebar is focused, hide it.

```
  {
    "key": "ctrl+b",
    "command": "workbench.action.focusSideBar",
    "when": "!sideBarFocus"
  },
  {
    "key": "ctrl+b",
    "command": "workbench.action.toggleSidebarVisibility"
  },
```

#### List Navigation

Navigate GUI lists with `Ctrl + j/k`.

```
  {
    "key": "ctrl+j",
    "command": "list.focusDown",
    "when": "listFocus && !inputFocus && !editorTextFocus"
  },
  {
    "key": "ctrl+k",
    "command": "list.focusUp",
    "when": "listFocus && !inputFocus && !editorTextFocus"
  },
  {
    "key": "ctrl+j",
    "command": "workbench.action.quickOpenSelectNext",
    "when": "inQuickOpen"
  },
  {
    "key": "ctrl+k",
    "command": "workbench.action.quickOpenSelectPrevious",
    "when": "inQuickOpen"
  },

```

#### Search Result Navigation

When search results are visible in the sidebar, use `Ctrl + Shift + j/k` to go between search results, even when in editor.

```  
  {
    "key": "ctrl+shift+j",
    "command": "search.action.focusNextSearchResult",
    "when": "hasSearchResult && activeViewlet == 'workbench.view.search'"
  },
  {
    "key": "ctrl+shift+k",
    "command": "search.action.focusPreviousSearchResult",
    "when": "hasSearchResult && activeViewlet == 'workbench.view.search'"
  },
```

#### Editor: Quick Open File

When in editor and `NORMAL` mode, press `'` to quick open a file via search.

```
  {
    "key": "'",
    "command": "workbench.action.quickOpen",
    "when": "editorTextFocus && neovim.init && !dirtyDiffVisible && !findWidgetVisible && !inReferenceSearchEditor && !markersNavigationVisible && !notebookCellFocused && !notificationCenterVisible && !parameterHintsVisible && !referenceSearchVisible && neovim.mode == 'normal'"
  }
```

#### Editor: Sidebar Search

When in editor and `NORMAL` mode, press `|` to open search sidebar to search for text within the project.

```
  {
    "key": "shift+\\",
    "command": "workbench.action.findInFiles",
    "when": "editorTextFocus && neovim.init && !dirtyDiffVisible && !findWidgetVisible && !inReferenceSearchEditor && !markersNavigationVisible && !notebookCellFocused && !notificationCenterVisible && !parameterHintsVisible && !referenceSearchVisible && neovim.mode == 'normal'"
  },
```

#### Editor: Search All Workspace Symbols

When in editor and `NORMAL` mode, press `{` to search all symbols in the workspace.

```
  {
    "key": "shift+[",
    "command": "workbench.action.showAllSymbols",
    "when": "editorTextFocus && neovim.init && !dirtyDiffVisible && !findWidgetVisible && !inReferenceSearchEditor && !markersNavigationVisible && !notebookCellFocused && !notificationCenterVisible && !parameterHintsVisible && !referenceSearchVisible && neovim.mode == 'normal'"
  },
```

#### Editor: Search Symbols in File (Outline)

When in editor and `NORMAL` mode, press `}` to search all symbols in the file.

```
  {
    "key": "shift+]",
    "command": "workbench.action.gotoSymbol",
    "when": "editorTextFocus && neovim.init && !textCompareEditorVIsible && !dirtyDiffVisible && !findWidgetVisible && !inReferenceSearchEditor && !markersNavigationVisible && !notebookCellFocused && !notificationCenterVisible && !parameterHintsVisible && !referenceSearchVisible && neovim.mode == 'normal'"
  },
```

#### Editor: Language Server Keybinds

```
if exists('g:vscode')
  nmap <silent> gd :call VSCodeCall('editor.action.peekDefinition')<CR>
  nmap <silent> gD :call VSCodeCall('editor.action.revealDefinition')<CR>
  nmap <silent> gr :call VSCodeCall('editor.action.referenceSearch.trigger')<CR>
  nmap <silent> gR :call VSCodeCall('references-view.findReferences')<CR>
  nmap <silent> gy :call VSCodeCall('editor.action.goToTypeDefinition')<CR>
  nmap <silent> grn :call VSCodeCall('editor.action.rename')<CR>
fi
```

#### Diff: Stage/Unstage

In a diff view: 

 * Select a hunk and press `Alt + s` to stage just that hunk.

 * Select a hunk and press `Alt + Shift + s` to unstage just that hunk.

 * Press `Ctrl + s` to stage the whole file.

```
  {
    "key": "alt+s",
    "command": "git.stageSelectedRanges",
    "when": "isInDiffEditor"
  },
  {
    "key": "shift+alt+s",
    "command": "git.unstageSelectedRanges",
    "when": "isInDiffEditor"
  },
  {
    "key": "ctrl+s",
    "command": "git.stage",
    "when": "isInDiffEditor"
  },
```

#### Toggle Split Width

When in a split of two editor groups, press `,` to toggle between maximizing the width of one split and evenly splitting them.

When a split is maximized, navigating to the smaller split will cause that one to become maximized instead.

In `init.vim`:

```
if exists('g:vscode')
  nnoremap , :call VSCodeCall('workbench.action.toggleEditorWidths')<CR>
endif
```

#### Toggle Zen Mode

Press `.` to toggle [Zen Mode](https://code.visualstudio.com/docs/getstarted/userinterface#_zen-mode). Zen Mode hides unnecessary UI elements and bars, only showing editors. The sidebar and terminal can still be invoked with keybinds in this mode.

In `init.vim`:

```
if exists('g:vscode')
  nnoremap . :call VSCodeCall('workbench.action.toggleZenMode')<CR>
endif
```

## Git Difftool

VS Code can be used as your difftool, even when remoted into a server.

```
~/.gitconfig:

[difftool "vscode"]
  cmd = code --wait --diff $LOCAL $REMOTE
```

You must invoke `git difftool` from the VS Code terminal for it to work properly.

## Make Doc Hover Larger

The mouse hover (also invokable with `gh`) also shows language server error output, but it's not resizable.

You can use the [Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css) extension to make this hover box a big larger with this CSS.

```
.monaco-editor .suggest-widget.docs-side {
  width: 1000px;
}

.monaco-editor .suggest-widget.docs-side > .details {
  width: 60%;
  max-height: 800px !important;
}

.monaco-editor .suggest-widget.docs-side > .tree {
  width: 30%;
  float: left;
}

.editor-widget.parameter-hints-widget.visible {
  max-height: 800px !important;
}

.monaco-editor .parameter-hints-widget > .wrapper {
  max-width: 1000px;
}

.monaco-editor .monaco-hover {
  max-width: 2000px !important;
  max-height: 800px !important;
  margin: 0;
}

.monaco-editor .monaco-hover-content {
  max-width: 2000px !important;
  max-height: 800px !important;
  margin: 0;
}
```

## Get Rid of Useless UI Elements

Elements in the sidebar and bottom bar that are annoying can be hidden by right clicking them.

## Show Line Numbers in Zen Mode

In `settings.json`: 

```
    "zenMode.hideLineNumbers": false,
```

## Workaround: Zsh Shell Breaks Due to Recursion

https://github.com/microsoft/vscode/issues/165648

Manually apply this patch to your VS Code: https://github.com/microsoft/vscode/pull/165174/files

## Extension: Docs View

[Docs View](https://marketplace.visualstudio.com/items?itemName=bierner.docs-view) is a useful extension that will show hover documentation in the Explorer sidebar panel.

## Extension: GitLens

[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) adds a bunch of fancy git features, but I mostly like it because it adds `git blame` annotations to the current editor line.

## Addendum: Wayland + Sway

I've found latency and compositing performanace with VS Code to be significantly better with Sway + Wayland over i3 + picom. If you're using Wayland, you need to launch VS Code with the proper flags to launch it with Wayland support.

```
~/.local/share/applications/code.desktop:

[Desktop Entry]
Name=Visual Studio Code
Comment=Code Editing. Redefined.
GenericName=Text Editor
Exec=/usr/share/code/code --enable-features=UseOzonePlatform --ozone-platform=wayland --unity-launch %F
Icon=com.visualstudio.code
Type=Application
StartupNotify=false
StartupWMClass=Code
Categories=TextEditor;Development;IDE;
MimeType=text/plain;inode/directory;application/x-code-workspace;
Actions=new-empty-window;
Keywords=vscode;

[Desktop Action new-empty-window]
Name=New Empty Window
Exec=/usr/share/code/code --enable-features=UseOzonePlatform --ozone-platform=wayland --new-window %F
Icon=com.visualstudio.code
```
