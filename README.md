# MacOS SSH Basic Examples

## Shell commands
```sh

# find ips of other computers on the network
arp -a

# find private ip of your computer
# for wifi
ipconfig getifaddr en0

# for ethernet
ipconfig getifaddr en1

# for ethernet over thunderbolt
ipconfig getifaddr en3

# find private ip of your router
netstat -nr | grep default

# view whether inbound ssh connections are allowed
sudo systemsetup -getremotelogin

# this requires full disk access. not sure how to turn that on
# allow ssh for other computers on this network
sudo systemsetup -setremotelogin On

# disallow ssh for other computers on this network
sudo systemsetup -setremotelogin Off

# enable without requiring full disk access
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist

# disable
sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist

# show all logged in users
# yes, it's just w
# the FROM column will be empty for sessions on this computer.
# for incoming ssh connections, it will have a private IP of the connecting computer
w

# find information about the incoming ssh connections
# you should see one run by root and one run by the account the inbound ssh connection is logging in as.
# the root one is the main ssh daemon that listens for incoming connections.
# the non-root one is the incoming connection from the other computer.
ps aux | grep sshd | grep -v 'grep'

# same as above, but exclude root
ps aux | grep sshd | grep -v 'grep' | grep -v '^root'

# kill all inbound ssh connections 
# keep in mind that the daemon run by root will also disappear if no ssh connections remain
ps aux | grep sshd | grep -v 'grep' | grep -v '^root' | awk '{print $2}' | xargs kill -9

# kill a process
kill -9 $PROCESS_ID



```

