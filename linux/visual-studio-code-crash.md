# Visual Studio Code Crash

Recently my Visual Studio Code on Fedora Linux 41 Workstation failed to start, saying: _"The window terminated unexpectedly (reason 'launch-failed' code '159')"._

I initially attempted to solve this by starting it with `code --verbose --wait`, but that just showed some error messages which didn't mean all that much to me.

[Google Gemini](https://gemini.google.com) was kind enough to walk me through debugging this using the following steps:

1. Try `code --user-data-dir /tmp/vscode-test` ... that worked (for me) - so the "binary" was probably fine (e.g. no need to reinstall the package), but some "config" was "bad"...

1. Try `code --disable-extensions` ... that didn't help (for me) - so it's not something extensions related - phew, VSC arch is sound!

1. Try `code --disable-gpu` ... that didn't help (for me) - so it's nothing related to [my cool AMD GPU](../ml/ollama1.md) - good!

1. Try `code --ozone-platform=x11` to see if it's [Wayland](https://en.wikipedia.org/wiki/Wayland_(protocol)) related - nope!

At this point, I lost patience... given that a fresh `~/.config/Code` data directory seemed to "fix it", `mv ~/.config/Code/ ~/.config/Code.BAD` seemed the most effective way to resolve this.

I knew that I could easily "start over" because I [keep all of my global VSC Keybindings, Personal Code Snippts & Settings under version control](https://github.com/vorburger/vorburger-dotfiles-bin-etc/tree/main/dotfiles/code), and have scripts to [export](https://github.com/vorburger/vorburger-dotfiles-bin-etc/blob/main/bin/code-extensions-export.sh) and easily [re-install my VSC extensions](https://github.com/vorburger/vorburger-dotfiles-bin-etc/blob/main/bin/code-extensions-install.sh)!

It became more interesting when **it still happened!** Using Spock's 🖖 Vulcan Deduction Logic, I figured that something somewhere [in this specific version of my VSC `settings.json`](https://github.com/vorburger/vorburger-dotfiles-bin-etc/blob/7a72f6edaed99ead4924439ad28408843a7256ab/dotfiles/code/settings.json#L1) clearly, and reproducibly, caused this.

Taking a (not quite so...) random wild guess, I narrowed it down to being caused by `"workbench.productIconTheme": "adwaita"`! I added that, years ago, [based on this guide](https://github.com/piousdeer/vscode-adwaita#suggested-settings), but it looks like some recent Fedora Upgrade broke this somehow. [Removing that](https://github.com/vorburger/vorburger-dotfiles-bin-etc/commit/1ae84d495c6ebfb86d3e6875fde4dafb0ce10dff) fixed it!

PS: Filed [VSC bug #237058](https://github.com/microsoft/vscode/issues/237058) just in case VSC maintainers wanted to further debug this.
