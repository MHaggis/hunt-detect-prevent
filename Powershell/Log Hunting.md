# The List

Source: http://909research.com/windows-log-hunting-with-powershell/

List all unique executable names recorded by Sysmon:
    Get-WinEvent -filterhashtable @{logname="Microsoft-Windows-Sysmon/Operational";id=1} | %{$_.Properties[3].Value} | sort -Unique

List all unique executable names and command lines used when starting a new process:

    Get-WinEvent -filterhashtable @{logname="Microsoft-Windows-Sysmon/Operational";id=1} | %{$_.Properties[4].Value} | sort -Unique

List domain names contacted recorded by Sysmon:

    Get-WinEvent -filterhashtable @{logname="Microsoft-Windows-Sysmon/Operational";id=3} | %{$_.Properties[14].Value}| sort -Unique

Every destination port contacted:

    Get-WinEvent -filterhashtable @{logname="Microsoft-Windows-Sysmon/Operational";id=3} | %{$_.Properties[15].Value}| sort -Unique

Hash of every executable run:

    Get-WinEvent -filterhashtable @{logname="Microsoft-Windows-Sysmon/Operational";id=1} | %{$_.Properties[11].Value}| sort -Unique

Some non-Sysmon related commands, note that proper auditing of these events must be on so the event logs are cut in the first place:

All windows security log event IDs, ranked by least frequent:

    Get-WinEvent -FilterHashtable @{logname="security"}| Group-Object id -NoElement | sort count

All usernames who have logged in:

    Get-WinEvent -FilterHashtable @{logname="security";id=4624} | %{$_.Properties[5].Value} | sort -Unique

Count of logins by username:

    Get-WinEvent -FilterHashtable @{logname="security";id=4624} | %{$_.Properties[5].Value} | group-object -noelement | sort count

All domains for accounts that have logged in:

    Get-WinEvent -FilterHashtable @{logname="security";id=4624} | %{$_.Properties[6].Value} | sort -Unique

SIDs for all accounts that have logged in:

    Get-WinEvent -FilterHashtable @{logname="security";id=4624} | %{$_.Properties[4].Value} | sort -Unique

Failed login count by username:

    Get-WinEvent -FilterHashtable @{logname="security";id=4625} | %{$_.Properties[1].Value} | Group-Object -noelement

Invalid usernames used for login attempts (looking for account guessing)

    Get-WinEvent -FilterHashtable @{logname="security";id=4776} | %{$_.Properties[1].Value} | sort -Unique

AppLocker events - List all executables and scripts that were against policy.

Use event ID 8003/8004 (audit mode/block mode) for exe and dll files:

    Get-WinEvent -FilterHashtable @{logname="Microsoft-Windows-AppLocker/EXE and DLL";id=8003} | select message.
Use event ID 8006/8007 for script or MSI files:

    Get-WinEvent -FilterHashtable @{logname="Microsoft-Windows-AppLocker/MSI and Script";id=8006} | select message
