# rsync Android to WSL 2
* How to rsync an Android 10 mobile phone to Windows Subsystem for Linux 2.
* In this tutorial an Android 10 mobile phone and Windows 10 Pro 10.0.19041 Build 19041 with WSL2 and Debian 10 is beign used.
   * At least enabling SSH might be different between WSL1 and WSL2.
   * Instructions should be combatible with Ubuntu.
* There might be some packages missing from the instructions which have been installed previously and have been omitted from installation instructions by mistake.

## Windows 10
### Enable WSL2
* https://docs.microsoft.com/en-us/windows/wsl/install-win10
### Install Debian
* Install Debian from Microsoft Store
### Open SSH port in Windows
1. Hit Windows key and search for "Windows Defender Firewall with Advanced Security" and open it.
1. Click on **Inbound Rules**
1. On the right side *Actions* click **New Rule...**
1. Select:
    * **Port**
    * **TCP**
    * Specific local ports: **2222**
    * Allow the connection
    * When does this rule apply?: **Check all boxes**
    
* The opening of firewall could have been done also via Administrator Command Prompt with command:

        netsh advfirewall firewall add rule name="SSH allow 2222 for WSL2" dir=in action=allow protocol=TCP localport=2222

## Configuring Debian WSL
1. Install required packages
   * rsync is required
   * openssh-server is required
   * vim is text editor that was used, but one can use what ever text editor they want. vim is powerful tool to when mastered, but learning curve can be steep. **nano** is easy to use for beginners.
   * man is just nice to have as one can check manual with the program, with command **man rsync** one can see how to use rsync

         sudo apt-get update & upgrade
         sudo apt-get install rsync openssh-server vim man

 1. Create folder for rsyncing
 
         # If one wants to create in home folder
         mkdir ~/rsync_phone
      
### Configuring SSH server
1. Edit with vim/nano/etc **/etc/ssh/sshd_config**

        ... settings above ...
        Port 222
        # AddressFamily any
        ListenAddress 0.0.0.0
        #ListenAddress ::        
        ... settings below ...

        # Uncomment line below, so one can authenticate with password. 
        #PasswordAuthentication yes
        ... settings below ...
1. Restart SSH

        sudo service ssh restart
1. Check your WSL IP, this is different than your Windows 10 IP.

        ip address show
        # short form
        ip a s
        
        # The output should be something like
        1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
            link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
            inet 127.0.0.1/8 scope host lo
               valid_lft forever preferred_lft forever
            inet6 ::1/128 scope host
               valid_lft forever preferred_lft forever
        2: bond0: <BROADCAST,MULTICAST,MASTER> mtu 1500 qdisc noop state DOWN group default qlen 1000
            link/ether f6:00:95:54:0b:71 brd ff:ff:ff:ff:ff:ff
        3: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000
            link/ether 6b:43:68:32:13:f7 brd ff:ff:ff:ff:ff:ff
        4: sit0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
            link/sit 0.0.0.0 brd 0.0.0.0
        5: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
            link/ether 00:16:5d:eb:2b:25 brd ff:ff:ff:ff:ff:ff
            inet 172.24.116.31/20 brd 172.24.127.255 scope global eth0
               valid_lft forever preferred_lft forever
            inet6 fe80::215:5dff:feea:2b15/64 scope link
               valid_lft forever preferred_lft forever
    * So the NIC (Network Interface Card) is **eth0** and IP is **172.24.116.31**.

## Windows 10 Configuring PortProxy
* One needs to configure Windows 10 to forward port 2222 to the WSL.
1. Open Command Promt as an Administrator and run command below with the IP that was checked above.

        netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=2222 connectaddress=172.24.116.31 connectport=2222
        
        # One can check the portproxy settings with command:
        netsh interface portproxy show v4tov4
        
        # portproxy settings can be removed with command:
        netsh int portproxy reset all
        
1. Check your Windows IP

        # Run in Command Prompt / PowerShell
        ipconfig

        # There should be long output, but check for Wi-Fi or LAN adapter.
        # In below one can see that Wi-Fi adapter is using IP 192.168.2.3.

        Wireless LAN adapter Wi-Fi:

        Connection-specific DNS Suffix  . :
        Link-local IPv6 Address . . . . . : fe80::9876:edc8:2b95:b08%6
        IPv4 Address. . . . . . . . . . . : 192.168.2.3
        Subnet Mask . . . . . . . . . . . : 255.255.255.0
        Default Gateway . . . . . . . . . : 192.168.2.1
        
        # WSL Virtua Adapter is shown as:
        Ethernet adapter vEthernet (WSL):

        Connection-specific DNS Suffix  . :
        Link-local IPv6 Address . . . . . : fe81::89f2:a4b7:8fa:2c7b%53
        IPv4 Address. . . . . . . . . . . : 172.24.116.1
        Subnet Mask . . . . . . . . . . . : 255.255.240.0
        Default Gateway . . . . . . . . . :
   
## Android 10
1. Install Termux application from Google Play Store.
    * No phone rooting is required.
1. Install required software in Termux

        pkg update
        pkg install rsync openssh

1. Enable access to phone's storage by executing command in Termux:

        termux-setup-storage
    * Now there should be symlinks to phone's storage in ~/storage/
    * Check more details from https://wiki.termux.com/wiki/Internal_and_external_storage

1. Try to SSH from the phone to WSL Debian
    * In Termux run command
    
          ssh -p 2222 user@192.168.2.3
          # You should be prompted for password.

   * If connecting with SSH worked, proceed to next step.     

### rsync via ssh
* SSH needs to be used with rsync, so that the data is encrypted during transfer. Rsync itself doesn't encrypt data during transfer.
* Use command below to rsync whole internal storage DCIM directory. DCIM directory is the directory where camera pictures or videos are stored by default.
** Note that option **-a** doesn't work as it copies symlinks as they are and not the content.

      rsync -rktvh --progress -e "ssh -p 2222" ~/storage/dcim user@192.168.2.3:~/rsync_phone/
      
      # In this case rsync is used in this manner:
      rsync [OPTION...] SRC... [USER@]HOST:DEST
      
      # Explanations for rsync options.
      # These explanations are from rsync man page. Run command "man rsync" to see more options (only works if "man" package is installed).
      -r          recursive
      -k          transform symlink dir on receiver as dir
          Option -K skipped symlink dir completely with message "skipping non-regular file "dcim"
          -K          treat symlinked dir on receiver as dir
      -t          preserve modification times
      -v          increase verbosity
      -h          output numbers in a human-readable format
      --progress  show progress during transfer
      
      -e          specify the remote shell to use
      
* If the rsync is successfull, the last 2 lines after running rsync should be something like:

      sent x.y bytes received x.y bytes x.y bytes/sec
      total size is x.y speedup is 1.00
