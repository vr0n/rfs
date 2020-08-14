# Remote File System script
This is a script I use as a systemd service to connect to a remote
file system I maintain. If you use a lot of junk devices like I do,
but you want all of your devices to have access to constantly "synced"
terrabytes of storage, this might work for you too. 

Since it is not truly "syncing" but just accessing a single filesystem,
it is VERY VERY important that you have someway to back up the data
you are using. If the disk fails, all of your devices sharing this 
data lose the data.

## HALT!!!
## This script will NOT WORK with its defaults even if you set all of the variables!!!!

There are three options for running this script after the variables
have been configured (the default is **OPTION 1**):
- **OPTION 1** - Use a jumpbox and have your ~/.ssh/config setup
- **OPTION 2** - Use a jumpbox and do NOT have your ~/.ssh/config setup
- **OPTION 3** - Do not use a jumpbox (so you probably won't need ~/.ssh/config)

**OPTION 2** and **OPTION 3** should work seamlessly if you know the IP addresses
of the machines you are using. The only catch to **OPTION 2** is
that (currently) this script assumes you have the same username
for both the jumpbox and the server holding the remote file system.
(Obviously, it doesn't make a differnce for **OPTION 3** since you are
only using one machine remote machine).

## OPTION 1 setup:
**OPTION 1** is what I use because it's "cleaner" and allows me to share
the script without sharing my jumpbox's public IP address.

### Setup:
1. Have a jumpbox
2. Have a server on your local network that hosts the data you want to mount remotely
3. Get their IP address (for this example, jumpbox will be 1.1.1.1 [a public ip address] and the file server will be 192.168.0.104 [LAN IP address])
4. In your ~/.ssh/config file, you will want to add something like this:
	```
	Host rfs
		HostName 192.168.0.104
		User <your user name for the HostName machine)
		ProxyCommand ssh <username for the jumpbox>@1.1.1.1 -W %h:%p
	```
5. From the above example, if everything is setup correctly, you will be able to use **OPTION 1** to mount the remote file system locally through your jumpbox

## OPTION 2 setup:
**OPTION 2** is probably what most people are looking for (maybe I should've made it the 
default, but it's not what I use, so, ya know...)

### Setup:
1. Have a jumpbox
2. Have a server on your local network that hosts the data you want to mount remotely
3. Get their IP address (for this example, jumpbox will be 1.1.1.1 [a public ip address] and the file server will be 192.168.0.104 [LAN IP address])
4. Uncomment and edit the variables in the script as necessary (they should be clearly marked with comments)

## OPTION 3 setup:
Maybe someone will find this useful, but probably not

### Setup:
1. Have a jumpbox that also hosts the data you want to mount locally
2. Get the public IP address of the box
3. Uncomment and edit the variables in the script as necessary (they should be clearly marked with comments)

## To-Do:
- "install" script to make this a systemd service (obviously, this only works if you are using systemd)
- I should probably add the SSHPORT variable at some point just to make this a more portable script...
