# Network
## Bootup hangs on network initialization
Use managed network to solve this problem. 

On default the server network setting put network interface on un-managed mode.
file : /etc/NetworkManager/NetworkManger.conf
    Changes : `managed=false` to `managed=false`
or remove all network interface from /etc/network/interfaces file.


# System 
## Boot to terminal
For OS that has systemd installed (for example ubuntu 16.04 LTS)
	``` bash
    sudo systemctl set-default multi-user.target # to terminal 
    sudo systemctl set-default graphical.target  # to gui
	```
For old grub system
	Modify /etc/default/grub
	``` 
	GRUB_CMDLINE_LINUX="text"
	GRUB_TERMINAL=console
	```
	Then sudo update-grub



