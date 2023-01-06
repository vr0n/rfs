# Remote File System (RFS) Script

Quick and dirty script to connect to a remote `sshfs`. Includes
the incredible ability to disconnect as well via the `close` command.

# Usage

## To Connect
```sh
./rfs <username> <remote path> <target ip> <target port> # to connect
./rfs close # to disconnect
```
