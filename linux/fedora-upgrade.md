---
title: "Fedora Upgrades"
date: 2022-10-01
tags: ["linux"]
image: "/images/placeholder.png"
---

# Fedora Upgrades

Following [Fedora Docs' _DNF System Upgrade_](https://docs.fedoraproject.org/en-US/quick-docs/dnf-system-upgrade/) works reasonably well.

Here are how I resolve a few issues I run into every time I upgrade.


## _"The password you use to log in to your computer no longer matches that of your login keyring."_

With _Automatic Login,_ the error message above appears e.g. when
[using GNOME Tweaks to auto-start Brave](https://github.com/vorburger/vorburger-dotfiles-bin-etc#on-fedora-workstation).

Work around it by using the _Passwords and Keys_ (Seahorse) app to delete the _Brave Safe Storage_.
This will break Brave's Saved Passwords and Sync; to fix that, go to `brave://sync-internals` to _Disable Sync (Clear Data),_
close Brave, and set up Sync again.


## GPG with YubiKey

<!-- https://github.com/vorburger/p#troubleshooting -->

    $ gpg --card-status
    gpg: selecting card failed: No such device
    gpg: OpenPGP card not available: No such device

This can be fixed with [a ~/.gnupg/scdaemon.conf](https://github.com/vorburger/vorburger-dotfiles-bin-etc/blob/46ae683dac91e1b4c0b0a66fdf2b2adc81848578/dotfiles/.gnupg/scdaemon.conf#L1).

PS: Earlier versions of this post recommended to do `sudo pkill gpg-agent && sudo systemctl restart pcscd` (manually, or via a `/etc/udev/rules.d/` rule; possibly also a [70-u2f.rules](https://github.com/Yubico/libfido2/blob/main/udev/70-u2f.rules)), or to [use `sudo dnf remove opensc`](https://bugzilla.redhat.com/show_bug.cgi?id=1893131) (but that may break other functionality). These were all wrong workarounds, and the `scdaemon.conf` is the recommended solution.
