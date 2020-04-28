# About

Installs Perforce 2019.1 server. Tested with Ubuntu 18.04 & Debian 10 (powered by DigitalOcean) .
All perforce files will be in /home/perforce

Created to be used with UE4 projects.
Full version available at:

https://allarsblog.com/2014/09/24/setup-perforce-digital/

https://allarsblog.com/2017/04/05/populating-perforce-with-an-unreal-engine-source-build/

# Usage

In shell, run the following commands in your terminal. You don't need to download this repo, that is what the first line in the following code does.

NOTE: If you want to use encrypted SSL perforce server, use SSL version of following script.

Non-SSL

```shell
wget https://raw.githubusercontent.com/Skylonxe/linux-perforce-installer/master/install-perforce
chmod +x install-perforce
sudo ./install-perforce
```

SSL

```shell
wget https://raw.githubusercontent.com/Skylonxe/linux-perforce-installer/master/install-perforce-ssl
chmod +x install-perforce-ssl
sudo ./install-perforce-ssl
```

You will be asked to create a password and user details for a new unprivileged system user named `perforce`. You generally will never need to ever log into your server with this user, but I still suggest a password you won't lose. This is *not* a Perforce user, this is a Linux/Ubuntu user for the server only. You will create your Perforce user when you connect for the first time.

Afterwards, the server will restart and you should then be able to connect to your Perforce server. If you are using SSL server, you will need to connect to host using format ssl:serverIPorDomain:port (examples: ssl:example.com:1666, ssl:192.168.1.1:166)
        
# Optional security and ease of use client steps (User's computer which has P4V client installed)

1. Set password security level in P4V admin tool 'Tools > Administration > Administration > Password Security Level', confirm superuser dialog if needed
2. Apply environment settings in P4V 'Connection > Environment Settings > OK'
3. Run cmd, cd .../path/... into your local perforce depot and execute following commands
```
p4 configure set dm.user.noautocreate=2    // disable unauthorized user creation (so users need to be created manually by admin)
p4 configure set run.users.authorize=1     // disable unauthorized viewing of your Perforce user list
p4 configure set dm.keys.hide=2            // disable unauthorized viewing of your Perforce config settings
```
4. Set type map with command: 
```p4 typemap```
, copy there content from typemap file from this repo
5. Copy .p4ignore file from this repo into your workspace
6. Enable .p4ignore use with command: 
```p4 set P4IGNORE=.p4ignore```
7. Add whole project in P4V (initial commit) : Right click root folder in Workspace tab and choose Mark for Add


