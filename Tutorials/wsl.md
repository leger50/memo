# WSL

Sub-Linux on Windows

## Access to windows file under WSL linux

- Script :
```shell
#!/bin/bash

PATH_WORKSPACE="/mnt/c/Users/{username}/Documents/workspaces"

sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata
cd "${PATH_WORKSPACE}"
```

## Ressources
- https://devblogs.microsoft.com/commandline/chmod-chown-wsl-improvements/