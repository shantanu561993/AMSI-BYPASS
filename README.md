This is a 0day vulnerability discovery for bypassing Antimalware Scan Interface (AMSI) and I will call it AMSI Write Raid, I mean why not?

Usually all the memory addresses pointing to the functions and data within the DLLs that the program depends on are inside the import address table (IAT) and they are marked as read only, so whenever you want to tamper with them, you have to use VirtualProtect api to mark the page as writable first.

And so EDR's will monitor the VirtualProtect API to see if the API call is doing something suspicious or not. 

But strangely, I discovered a writable entry that you can overwrite without the need of `VirtualProtect` API, that can bypass the whole AMSI process.

And because I am not using VirtualProtect API to change the memory protection, as it is already marked as Read/Write, it will likely bypass AV's and EDR's.

Note: Most AV's supports and uses the AMSI functionality developed by Microsoft, so bypassing AMSI => Bypasses not only defender but all of them.

Tested on win11 Build 22631 (Latest at the time of writing) and windows Preview.

