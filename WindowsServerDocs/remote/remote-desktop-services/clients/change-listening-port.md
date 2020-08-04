---
title: Change the listening port in Remote Desktop
description: Learn how to change the listening port for Remote Desktop client.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
---
# Change the listening port for Remote Desktop on your computer

>Applies to: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

When you connect to a computer (either a Windows client or Windows Server) through the Remote Desktop client, the Remote Desktop feature on your computer "hears" the connection request through a defined listening port (3389 by default). You can change that listening port on Windows computers by modifying the registry.

1. Start the registry editor. (Type regedit in the Search box.)
2. Navigate to the following registry subkey:
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. Click **Edit > Modify**, and then click **Decimal**.
4. Type the new port number, and then click **OK**. 
5. Close the registry editor, and restart your computer.

The next time you connect to this computer by using the Remote Desktop connection, you must type the new port. If you're using a firewall, make sure to configure your firewall to permit connections to the new port number.

You can always check the current port through PowerShell too with below commands:

Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "PortNumber"
Ex:
PortNumber   : 3389
PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal
               Server\WinStations\RDP-Tcp
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal
               Server\WinStations
PSChildName  : RDP-Tcp
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry

You can change RDP port by executing PowerShell commands too as example shown below by adding RDP port as 3390
Add New RDP Port in Registry:
Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "PortNumber" -Value 3390
New-NetFirewallRule -DisplayName 'RDPPORTLatest' -Profile 'Public' -Direction Inbound -Action Allow -Protocol TCP -LocalPort 3390
