# Pass through" a physical disk in Virtual Machine Manager

Here is how to "pass through" an actual physical disk from a Linux (workstation) host into a (Linux) virtual machine, using the [Virtual Machine Manager](https://virt-manager.org/) (VMM) UI with click-click.

One reason why one might want to do this could be e.g. to explore running [TrueNAS](https://www.truenas.com) in a VM.

## Steps

1. Open VM's settings via menu _Edit > Virtual Machine Details_

1. Click _Add Hardware_ (lower left)

1. Use _Storage_ section of _Add New Virtual Hardware_

1. Choose _Select or create custom storage_ (instead of _Create a disk image for the virtual machine)_

1. In the textbox after the _Manage_ button (do NOT click), simply fill in the `/dev/disk/by-id/...` path
   (of whatever disk you want to pass through, obviously). Do NOT use e.g. `/dev/sda1` by its corresponding ID;
   use `ls -l /dev/disk/by-id/` to see which is which.

1. As _Device type:_ use _Disk device_

1. As _Bus type:_ use _SATA_ (typically)

1. Click Finish

1. Start the VM

1. Guest should now see the disk!

VMM is of course based on `libvirt`, for `qemu`, so the same is also possible by editing XML with `virsh edit`; it would look something this:

```xml
<disk type="block" device="disk">
  <driver name="qemu" type="raw" cache="none" io="native" discard="unmap"/>
  <source dev="/dev/disk/by-id/ata-ST8000AS0002-1NA17Z_Z840N805"/>
  <target dev="sda" bus="sata"/>
  <address type="drive" controller="0" bus="0" target="0" unit="0"/>
</disk>
```

<!--
1. Click _Manage_ to _Locate or create storage volume_

1. Click `+` (lower left) to open the _Add a New Storage Pool_ UI

1. Choose _Type:_ of `disk:` Physical Disk Device

1. Leave _Format:_ to `auto`

1. Click _Browse_ of _Source Path_ and choose e.g. `/dev/disk/by-id/...` (of whatever disk you want to pass through, obviously).
   Do NOT use e.g. `/dev/sda1` by its corresponding ID; use `ls -l /dev/disk/by-id/` to see which is which.

1. Change _Name:_ from `pool` to e.g. the Serial Number (S/N or SN) of your disk

1. Change from the _Details_ to the _XML_ tab

1. Change `<format type="auto"/>` to `<format type="gpt"/>`

1. Click _Finish_ in the _Add a New Storage Pool_ UI

1. Pick that new _Physical Disk Device_ in the now displayed _Locate or create storage volume_

1. Pick the (only) _Volume_ shown. If there is none, format your disk and create a single new partition on it.

1. Click `+` _Create new volume_

1. Change _Name:_ from `vol` to e.g. `vol_` followed by the Serial Number (S/N or SN) of your disk

1. Increase the _Storage Volume Quota_ to its _available space_

1. Click _Choose Volume_

1. Back in the _Add New Virtual Hardware_ change (e.g.) `/dev/sda1` to (e.g.) `/dev/disk/by-partuuid/cc2a7b07-6252-493b-829d-8dbdfb75d72d`;
   use `ls -l /dev/disk/by-partuuid/` to see which is which.

## XML

VMM is of course based on `libvirt`, for `qemu`, so the same is also possible by editing XML with `virsh edit`; it would like something like this:

```xml
<pool type="disk">
  <name>Z840N805</name>
  <uuid>5bf94484-a5b6-4f30-bdfd-5b0d945f58a2</uuid>
  <capacity unit="bytes">8001563205120</capacity>
  <allocation unit="bytes">8001561821184</allocation>
  <available unit="bytes">1366528</available>
  <source>
    <device path="/dev/disk/by-id/ata-ST8000AS0002-1NA17Z_Z840N805">
      <freeExtent start="17408" end="1048576"/>
      <freeExtent start="8001562869760" end="8001563205120"/>
    </device>
    <format type="gpt"/>
  </source>
  <target>
    <path>/dev</path>
  </target>
</pool>
```

## Troubleshooting

### Format of device '...' does not match the expected format 'dos'

```
Traceback (most recent call last):
  File "/usr/share/virt-manager/virtManager/asyncjob.py", line 72, in cb_wrapper
    callback(asyncjob, *args, **kwargs)
  File "/usr/share/virt-manager/virtManager/createpool.py", line 343, in _async_pool_create
    poolobj = pool.install(create=True, meter=meter, build=build)
              ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/share/virt-manager/virtinst/storage.py", line 415, in install
    raise RuntimeError(errmsg)
RuntimeError: Could not start storage pool: Requested operation is not valid: Format of device '/dev/sda1' does not match the expected format 'dos'
```

This should be solved by completely wiping the disk and creating a GPT partition table (e.g. using _Format_ of GNOME's _Disks_ UI tool)
and using `<format type="gpt"/>` instead of `<format type="auto"/>`, as described above.

### Error: You requested a partition from ... to ... (sectors ...). The closest location we can manage is ... to ... (sectors ...).

```
Error creating vol: Couldn't create storage volume 'vol_Z840N805': 'internal error: Child process (parted /dev/disk/by-id/ata-ST8000AS0002-1NA17Z_Z840N805 mkpart --script primary 17408B 8001524089855B) unexpected exit status 1: Error: You requested a partition from 17.4kB to 8002GB (sectors 34..15627976737).
The closest location we can manage is 1049kB to 8002GB (sectors 2048..15627976737).
'

Traceback (most recent call last):
  File "/usr/share/virt-manager/virtManager/asyncjob.py", line 72, in cb_wrapper
    callback(asyncjob, *args, **kwargs)
  File "/usr/share/virt-manager/virtManager/createvol.py", line 314, in _async_vol_create
    vol.install(meter=meter)
  File "/usr/share/virt-manager/virtinst/storage.py", line 707, in install
    raise RuntimeError(msg) from None
RuntimeError: Couldn't create storage volume 'vol_Z840N805': 'internal error: Child process (parted /dev/disk/by-id/ata-ST8000AS0002-1NA17Z_Z840N805 mkpart --script primary 17408B 8001524089855B) unexpected exit status 1: Error: You requested a partition from 17.4kB to 8002GB (sectors 34..15627976737).
The closest location we can manage is 1049kB to 8002GB (sectors 2048..15627976737).
'
```

This can be solved by creating a partition in the new disk. It can of type _Other_ and _No filesystem_ e.g. using GNOME's _Disks_ UI tool.
-->
