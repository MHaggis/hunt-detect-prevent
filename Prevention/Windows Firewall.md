# Microsoft Windows Firewall

## Resources
https://isc.sans.edu/diary/21829

**netsh block verclsid**

    netsh advfirewall firewall add rule name "Block Egress Verclsid" dir=out program="c:\windows\syswow64\verclsid.exe" enable=yes action=block profile=any
