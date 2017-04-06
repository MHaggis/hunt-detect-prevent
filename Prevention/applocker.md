# Microsoft Applocker

## Resources

http://www.howtogeek.com/howto/6317/block-users-from-using-certain-applications-with-applocker/
https://github.com/iadgov/AppLocker-Guidance

**What to block**

Generally, you should also consider blocking these at your spam gateway.

    .ade, .adp, .ani, .bas, .bat, .chm, .cmd, .com, .cpl, .crt, .exe, .hlp, .ht, .hta, .inf, .ins, .isp, .jar, .job, .js, .jse, .lnk, .mda, .mdb, .mde, .mdz, .msc, .msi, .msp, .mst, .ocx, .pcd, .ps1, .reg, .scr, .sct, .shs, .svg, .url, .vb, .vbe, .vbs, .wbk, .wsc, .ws, .wsf, .wsh, .exe, .pif, .pub

**Where to block**

    <drive letter>\users\<username>\appdata

    <drive letter>\users\<username>\appdata\local

    <drive letter>\users\<username>\appdata\local\temp

    <drive letter>\users\<username>\appdata\roaming

    <drive letter>\programdata
