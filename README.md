# About

Installs Perforce 2019.1 server. Tested with Ubuntu 18.04 (powered by DigitalOcean).
All perforce files will be in /home/perforce

Created to be used with UE4 projects.

# Usage

In shell, run the following commands in your terminal. You don't need to download this repo, that is what the first line in the following code does.

```shell
wget https://raw.githubusercontent.com/Skylonxe/linux-perforce-installer/master/install-perforce
chmod +x install-perforce
sudo ./install-perforce
```

You will be asked to create a password and user details for a new unprivileged system user named `perforce`. You generally will never need to ever log into your server with this user, but I still suggest a password you won't lose. This is *not* a Perforce user, this is a Linux/Ubuntu user for the server only. You will create your Perforce user when you connect for the first time.

Afterwards, the server will restart and you should then be able to connect to your Perforce server.

# Security

The created server will have default Perforce installation settings. This means anyone who connects to your server can create a user account without authorization. After you create your first user, you should close this security hole by using the following `p4` command from your Perforce Client.

        p4 configure set dm.user.noautocreate=2
        
# Full client steps

1. Set password security level in admin tool
2. Apply environment settings in perforce client
3. Run:
p4 configure set dm.user.noautocreate=2
p4 configure set run.users.authorize=1    
p4 configure set dm.keys.hide=2
4. Set type map: p4 typemap, copy there content from typemap file
5. Copy .p4ignore file to workspace
6. cd to workspace and set .p4ignore: p4 set P4IGNORE=.p4ignore
7. Add whole project
