Why this fork
=============

## Smart indentation
I strongly recomend installing the `haskell-mode` package and enabling `haskell-indent-mode` in Lean buffers. It will provide a replacement (IMHO a better one) for the "enhanced relative indent" code that I have removed from this fork.

Installation
============

Before using this major mode, you need to [install Lean 4](https://leanprover.github.io/lean4/doc/setup.html#basic-setup).

To install `lean4-mode` in Emacs with `straight.el`, you can use:
```
(use-package lean4-mode
  :straight (lean4-mode
	     :type git
	     :host github
	     :repo "leanprover/lean4-mode"
	     :files ("*.el" "data"))
  ;; to defer loading the package until required
  :commands (lean4-mode))
```

Trying It Out
=============

If things are working correctly, you should see the word ``Lean 4`` in the
Emacs mode line when you open a file with extension `.lean`. Emacs will ask you
to identify the "project" this file belongs to. If you then type
```lean
#check id
```
the word ``#check`` will be underlined, and hovering over it will show
you the type of ``id``. The mode line will show ``FlyC:0/1``, indicating
that there are no errors and one piece of information displayed.

To view the proof state, run `lean4-toggle-info` (`C-c` `C-i`). This will show the `*Lean Goals*` buffer (like the `Lean infoview` pane in VSCode) in a separate window.

Settings
========

Set these with e.g. `M-x customize-variable`.

* `lsp-headerline-breadcrumb-enable`: show a "breadcrumb bar" of namespaces and sections surrounding the current location (default: off)

Key Bindings and Commands
=========================

| Key                | Function                                                                        |
|--------------------|---------------------------------------------------------------------------------|
| <kbd>C-c C-k</kbd> | show the keystroke needed to input the symbol under the cursor                  |
| <kbd>C-c C-d</kbd> | recompile & reload imports (`lean4-refresh-file-dependencies`)                  |
| <kbd>C-c C-x</kbd> | execute Lean in stand-alone mode (`lean4-std-exe`)                              |
| <kbd>C-c C-p C-l</kbd> | builds package with lake (`lean4-lake-build`)                                   |
| <kbd>C-c C-i</kbd> | toggle info view showing goals and errors at point (`lean4-toggle-info-buffer`) |
| <kbd>C-c ! n</kbd> | flycheck: go to next error                                                      |
| <kbd>C-c ! p</kbd> | flycheck: go to previous error                                                  |

For `lsp-mode` bindings, see https://emacs-lsp.github.io/lsp-mode/page/keybindings/ (not all capabilities are supported currently).

In the default configuration, the Flycheck annotation `FlyC:n/n` indicates the
number of errors / responses from Lean; clicking on `FlyC` opens the Flycheck menu.
