doesn't have many packages... :( 
Use [Devbox](obsidian://open?vault=Notes&file=Devbox) instead?
## Install 
create /nix directory
`chown` to my user
run install script
```shell
sh <(curl -L https://nixos.org/nix/install) --no-daemon
```

Test it with
```shell
nix-env -i hello && which hello && hello
```

