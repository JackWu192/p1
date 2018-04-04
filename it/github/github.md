#ssh connection
Most resources from internet tells to use ssh-agent, actually you don't. 
	1. Create key-pairs by using ssh-keygen, on ~/.ssh/ direcotory
	2. Modify the mode of private key to 400. According to web, github requires this, otherwise a fail on link to 
		show unclear permission denying.
	2. Upload public key to profile on github
	3. Modify the config in ~/.ssh to add
	``` shell
		HOST github.com github gh    	# list all alias you need, but github.com must be in the list, 
						# cause git default to use that one for remote line.
			user git
			HostName github.com	# All alias in HOST line will map to this host.
			IdentityFile = ~/.ssh/id_rsa_github
			
	   

