# Switching from NetworkManager to systemd-networkd on Fedora Linux 41 Workstation

## TL;DR

This blog post documents how to switch from NetworkManager to systemd-networkd on Fedora Linux 41 Workstation.

## Background

I have always been using NetworkManager on Fedora Linux Workstation. But sometimes my computer would refuse to enter suspend mode, or not work when resuming ("waking up") from suspension.

`journalctl -k` showed that it was because of: _"Freezing user space processes failed after 20.004 seconds (14 tasks refusing to freeze, wq_busy=0):"_ with all in `state:D`:

* `Task:NetworkManager`
* `task:tailscaled`
* `task:ipfs`
* `task:gnome-software`
* `task:transmission-gt`
* `task:cody-agent28067`
* `task:dnf5`
* `task:packagekit-dnf-`

These are all networking related, and the 1st likely caused the others.

Upon resume, `systemtl status NetworkManager` looks fine. But `nmcli` does not work anymore. And even `sudo killall -9 NetworkManager` does not help.

Cold reboot would fix it, of course - but PITA.

## 🐬 Flip Switch

```sh
systemctl status NetworkManager
sudo systemctl stop NetworkManager
sudo systemctl disable --now NetworkManager

systemctl status systemd-networkd
sudo systemctl enable --now systemd-networkd

networkctl
IDX LINK       TYPE     OPERATIONAL SETUP
  1 lo         loopback carrier     unmanaged
  2 enp23s0    ether    no-carrier  unmanaged
  3 eno1       ether    routable    unmanaged

networkctl status enp23s0
networkctl status eno1

ll /etc/systemd/network/

sudo bash -c "cat <<EOF >/etc/systemd/network/eno1.network
[Match]
Name=eno*

[Network]
DHCP=yes
EOF
"

sudo systemctl restart systemd-networkd

networkctl
IDX LINK       TYPE     OPERATIONAL SETUP
  1 lo         loopback carrier     unmanaged
  2 enp23s0    ether    no-carrier  unmanaged
  3 eno1       ether    routable    configurured

networkctl status eno1

sudo -K
```

## `systemd-resolved`

I didn't have to do anything about `systemd-resolved`, because this already seems to be running by default, at least on Fedora:

```sh
systemctl systemd-resolved
```

## `resolve.conf`

I didn't have to `ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf` because this already seems to be so by default, at least on Fedora:

```sh
$ ll /etc/resolv.conf
lrwxrwxrwx. root root 39 B 2023-11-01 02:09  /etc/resolv.conf ⇒ ../run/systemd/resolve/stub-resolv.conf
```

## References

* https://wiki.archlinux.org/title/NetworkManager
* https://wiki.archlinux.org/title/Systemd-networkd
* https://fedoracloud.readthedocs.io/en/latest/networkd.html
* https://linux.fernandocejas.com/docs/how-to/switch-from-network-manager-to-systemd-networkd
* https://trishnag.wordpress.com/2016/08/09/how-to-convert-networkmanager-to-networkd/
* https://www.xmodulo.com/switch-from-networkmanager-to-systemd-networkd.html
