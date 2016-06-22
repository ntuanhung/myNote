1. Local Area Network : How to fix slow LAN transfer speed of files in Windows [http://www.howtosolutions.net/2013/06/fixing-slow-sending-or-receiving-of-files-through-lan-network-using-windows/]
  + Turning off "Remote Differential Compression" (WRONG WAY)
  + Disabling "TCP Auto-Tuning" (WRONG WAY)
  + Disabling "Large Send Offload (LSO)" (VERIFIED)
      Large Send Offload is a technique of improving network performance while at the same time reducing CPU overhead. Apparently it does not work very well, so it was suggested to disable it. If you would like to know about LSO, check this MSDN article from 2001.
      LSO is an option located in a Device Manager under your network adapter, so this solution requires Administrator Privileges.
      Follow these steps:
        - Open Start Menu, right-click on Computer and select Properties
        - Under Control Panel Home located on the left side of the window click on Device Manager
        - You will get a list of all devices on your machine. Expand Network Adapters.
        - Find your Network Card and double-click on it.
        - Select Advanced tab. You will get a list filled with different options.
        - Select Large Send Offload V2 (IPv4) and set the value to Disabled
        - Do the same for Large Send Offload V2 (IPv6) if it is available
        - Click OK
    After clicking OK, I tried to send a file over the LAN network. The transfer speed started very slow, but it was gradually picking up speed. I decided to restart the computer and try to send that file again and this time it worked like a charm.
