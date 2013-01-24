# git-gutter.el

## Introduction
`git-gutter.el` is port of [GitGutter](https://github.com/jisaacks/GitGutter)
which is a plugin of Sublime Text2.


If you use fringe style(not linum style), please see [git-gutter-fringe](https://github.com/syohex/emacs-git-gutter-fringe)


## Screenshot

![git-gutter.el](https://github.com/syohex/emacs-git-gutter/raw/master/image/git-gutter1.png)


## Requirements

* Emacs 24 or higher


## Basic Usage

`git-gutter.el` provides following commands.

Show changes from last commit

    M-x git-gutter

Clear changes

    M-x git-gutter:clear

Toggle git-gutter

    M-x git-gutter:toggle


## Sample Configuration

```` elisp
(require 'git-gutter)

;; bind git-gutter toggle command
(global-set-key (kbd "C-x C-g") 'git-gutter:toggle)

;; Update changes information after save buffer
(add-hook 'after-save-hook
          (lambda ()
            (when (zerop (call-process-shell-command "git rev-parse --show-toplevel"))
              (git-gutter))))
````


## Customize

You can change the signs and those faces.

```` elisp
(setq git-gutter:modified-sign "  ") ;; two space
(setq git-gutter:added-sign "++")    ;; multiple character is OK
(setq git-gutter:deleted-sign "--")

(set-face-background 'git-gutter:modified "purple") ;; background color
(set-face-foreground 'git-gutter:added "green")
(set-face-foreground 'git-gutter:deleted "red")
````

### Screenshot of above customization

![git-gutter-multichar](https://github.com/syohex/emacs-git-gutter/raw/master/image/git-gutter-multichar.png)


### Using full width characters

Emacs has `char-width` function which returns character width.
`git-gutter.el` uses it for calculating character length of the signs.
But `char-width` does not work for some full-width characters.
So you should explicitly specify window width, if you use full-width
character.

```` elisp
(setq git-gutter:window-width 2)
(setq git-gutter:modified-sign "☁")
(setq git-gutter:added-sign "☀")
(setq git-gutter:deleted-sign "☂")
````

### Screenshot of above customization
![git-gutter-fullwidth](https://github.com/syohex/emacs-git-gutter/raw/master/image/git-gutter-fullwidth.png)


## Implement your own git-gutter

You can create your own git-gutter to implement 2 functions.

### view function

View function view diff informations to current buffer.
View function takes list of diff informations(`diffinfos`). `diffinfos`
are list of plist(`diffinfo`) and `diffinfo` has property `:type`,
`:start-line`, `:end-line`. `:type` is `'added` or `'deleted` or `'modified`.
`:added` and `'modified` have `:start-line` and `':end-line` property.
`:deleted` has only `:start-line` property.

Set view function variable `git-gutter:view-diff-function`.


### clear function

Clear function clears diff informations.
Clear function takes no arguments.

Set clear function variable `git-gutter:view-diff-function`.

If you are interested in implement your git-gutter,
please see example, [git-gutter-fringe](https://github.com/syohex/emacs-git-gutter-fringe).
