# git-gutter.el

## Introduction
`git-gutter.el` is port of [GitGutter](https://github.com/jisaacks/GitGutter)
which is a plugin of Sublime Text2.


## Screenshot

### linum-mode style
![git-gutter.el](https://github.com/syohex/emacs-git-gutter/raw/master/image/git-gutter1.png)

### View git information in fringe
![git-gutter-fringe.el](https://github.com/syohex/emacs-git-gutter/raw/master/image/git-gutter-fringe.png)


## Requirements

* Emacs 24 or higher
* [fringe-helper](http://www.emacswiki.org/emacs/FringeHelper) for using `git-gutter-fringe`


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
;;(require 'git-gutter-fringe) If you use flinge version

(add-hook 'after-save-hook
          (lambda ()
            (if (zerop (call-process-shell-command "git rev-parse --show-toplevel"))
                (git-gutter))))
````
