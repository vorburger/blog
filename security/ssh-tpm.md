---
title: "SSH with private keys sealed in TPM on Fedora Linux"
date: 2025-06-19
tags: ["security"]
image: "/images/ssh-tpm.png"
---

# SSH with private keys sealed in TPM on Fedora Linux

Instead of [safely storing SSH private keys on a Yubikey](ed25519-sk.md) (if you don't have one) you might want to keep private keys sealed in TPM.

Here is how to do this on Fedora Linux using https://github.com/Foxboron/ssh-tpm-agent:

    $ sudo dnf install openssl-devel
    $ go install github.com/foxboron/ssh-tpm-agent/cmd/...@latest

    $ ~/go/bin/ssh-tpm-keygen --supported
    ecdsa bit lengths: 256 384
    rsa bit lengths: 2048

As this TPM supports ECDSA keys with 384 (but not 521) bits, so:

    $ ~/go/bin/ssh-tpm-keygen -b 384

You may want use an empty passphrase (here, only). Now let's activate this TPM SSH agent:

    $ ssh-tpm-agent --install-user-units
    $ systemctl --user enable --now ssh-tpm-agent.socket

Activate `SSH_AUTH_SOCK`, e.g. [like this](https://github.com/vorburger/vorburger-dotfiles-bin-etc/commit/e3b1757474ecad08e17c17d3043aa8a21212ec5e).

Transfer `~/.ssh/id_ecdsa.pub` to https://github.com/settings/keys, and test it:

    $ ssh git@github.com

Voilà!
