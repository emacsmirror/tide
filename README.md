## Tide

![](https://i.imgur.com/5hPRts8.gif)

### Installation

* Install dash, flycheck and company via <kbd>M-x package-install</kbd>
* clone https://github.com/ananthakumaran/tide
* clone and build https://github.com/Microsoft/TypeScript (tested on 3d0daef8eb08104920f9272b32d414b9266a5d78)


````cl
(add-to-list 'load-path "path/to/tide/")
(require 'tide)
(add-to-list 'auto-mode-alist '("\\.ts$" . typescript-mode))
(setq tide-tsserver-executable "path/to/typescript/bin/tsserver")
(add-hook 'typescript-mode-hook
          (lambda ()
            (flycheck-mode t)
            (setq flycheck-check-syntax-automatically '(save mode-enabled))
            (company-mode-on)
            (tide-setup)
            (turn-on-eldoc-mode)))

(setq company-tooltip-align-annotations t) ;; aligns annotation to the right hand side

````

### Notes

* Make sure to add
  [tsconfig.json](https://github.com/Microsoft/TypeScript/wiki/tsconfig.json)
  in the project root folder.

* tsserver mangles output
  sometimes [issue - #2758](https://github.com/Microsoft/TypeScript/issues/2758),
  which will result in json parse error. Try node version 0.12.x if
  you get this error.


### Commands

* <kbd>M-x tide-restart-server</kbd>: Restarts tsserver. Currently tsserver doesn't
  pickup tsconfig.json file changes. This would come in handy after you
  edit tsconfig.json.

Keyboard shortcut   | Description
--------------------|----------
<kbd>C-c d</kbd>    | Show documentation for the symbol at point.
<kbd>M-.</kbd>      | Jump to the definition of the symbol at point.
<kbd>M-,</kbd>      | Return to your pre-jump position.