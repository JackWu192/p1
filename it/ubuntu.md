# Network
## Bootup hangs on network initialization
Using managed network. On default the server network setting put network interface on un-managed mode.
file : /etc/NetworkManager/NetworkManger.conf
    Changes : `managed=false` to `managed=false`
or remove all network interface from /etc/network/interfaces file.
