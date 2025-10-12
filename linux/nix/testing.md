# NixOS Testing

I've continued to dabble with NixOS [since attending NixCon 2025](../../conferences/NixCon-2025.md).

Today I finally got around to learning how to do testing of NixOS configurations; and it's actually pretty cool!!

[First install `nix`](https://github.com/vorburger/LearningLinux/blob/7d6819e4bef64352c34669e0ae2a4b2e4868473a/nix/docs/install.md), if you haven't already.
Then, [as explored in my `LearningLinux` repo here](https://github.com/vorburger/LearningLinux/tree/7d6819e4bef64352c34669e0ae2a4b2e4868473a/nix/os/tests),
put this into a `hello.nix` file:

```nix
{ pkgs, ... }:
{
  environment.systemPackages = with pkgs; [
    hello
  ];
}
```

and then this into a `test.nix` file:

```nix
{
  nodes = {
    machine1 = { pkgs, ... }: { };
    machine2 = { pkgs, ... }: { };
    machine3 = import ./hello.nix;
  };

  testScript = ''
    start_all()
    for m in [machine1, machine2, machine3]:
      m.systemctl("start network-online.target")
      m.wait_for_unit("network-online.target")

    machine1.succeed("ping -c 1 machine2")
    machine2.succeed("ping -c 1 machine1")

    machine3.succeed("hello")
    machine2.fail("hello")
  '';
}
```

and then put this into a `flake.nix` file:

```nix
{ inputs.nixpkgs.url = "github:nixos/nixpkgs?ref=nixos-unstable";
  outputs =
    { self, nixpkgs }: {
      checks.x86_64-linux.default = nixpkgs.legacyPackages.x86_64-linux.testers.runNixOSTest ./test.nix;
    };
}
```

then run this:

```sh
nix flake check
```

and, just like that, you just built and started 3 virtual machines (VMs) using QEMU, had 2 of them with default NixOS ping each other,
and installed and ran [`hello`](https://search.nixos.org/packages?channel=unstable&show=hello&query=hello) on the 3rd one - in ~8s!! (On my computer; on 2nd and subsequent runs, 1st is slower - YMMV.)

Next up, I'll go learn more about how to refactor my aforementioned repo, which is still a bit of a mess,
into a _"single `flake.nix` 'mono-repo'"_ of a gazillion small focused and thus easier to read clean _"modules"._
Apparently [`flake-parts.modules`](https://flake.parts/options/flake-parts-modules.html) is the way to go for that;
and if you marry this with [`vic/import-tree`](https://github.com/vic/import-tree) then you can reach
_"[dendritic](https://github.com/mightyiam/dendritic)"_ Nirvana Nix heaven! 😃

And then I would like to (re-re-)install bazillions of actual completely empty bare-metal machines with NixOS, too, not just VMs.
(I want to plug a single USB stick into a machine, and have it install specific custom NixOS on the machine from that stick, based
on some matched Host ID of that machine's configuration in said Git repo - and completely 100% headless unattended only, of course.
I'm not really sure exactly how to do that just yet, but I'll figure it out - given time.)
