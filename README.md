# Windows Embedded inspection
the other day i saw a funny thing, a gate at the train station got restarted, and all of a sudden:
![[Pasted image 20250730184209.png]]
this image is being popped
so that made me think, first of all why windows, other then user friendly i do not see any positive thing about running those machines on windows, and second of all, is that a hacker "wet dream?", so of course i had to find a version of it online and try to see what can i do with it
# Links:
took an iso image from here: https://archive.org/details/windows-10-15035-surface-rt-08-01-2024-15-23-54
am not going to upload it to the web because its 2.3Gb and github will be mad.
# Tools I Will Use
1. wsl - windows subsystem linux, i dont like virtual machines, but VM can work here as well :)
2. VMware workstation - i need a way to run this windows version
3. nmap - network mapping tool
4. probably much more, but i will state it and say where you can get them :)

# Starting The VM
so hopefully it will go plug and play, but because its for real time, it may have some hardware related interrupts that we will need to patch, lets see:
![[Pasted image 20250730195328.png]]
![[Pasted image 20250730195352.png]]
that doen't look good......
lets open the ISO using 7zip
![[Pasted image 20250730195434.png]]
we do have boot, interesting, lets see if someone tried to run this thing using vmware somewhere in the world
so i didn't find anyone who ran this exact machine, but i looked at the settings and saw this important settings in the -> Edit virtual machine settings
![[Pasted image 20250730200327.png]]
this can be a good check to see if this is related, and on the same way, lets save the logs :)
now, lets go to Hardware -> CD/DVD, click on advanced, and enable Legacy Emulation for testing:
![[Pasted image 20250730200443.png]]
now when we try to load the machine:
![[Pasted image 20250730200511.png]]
still no luck......
interestingly enough, when restarting the machine and pressing quickly on the F2 key, we can get to a boot menu, and then go to setup -> boot from file, lets see if that one gives us any progress :)
![[Pasted image 20250730200749.png]]
after trying every single file, nothing worked....
lets see if there is anything interesting in the logs
```
2025-07-30T17:06:28.627Z In(05) vmx USB: Connecting device desc:name:Virtual\ Bluetooth\ Adapter vid:0e0f pid:0008 speed:full family:wireless,bluetooth deviceType:virtual-bluetooth info:0000001 version:4 id:0x700000010e0f0008
2025-07-30T17:06:28.627Z Wa(03) vmx Bluetooth-Win32: ERROR retrieving local radio info: No more data is available
2025-07-30T17:06:28.627Z Wa(03) vmx Bluetooth host backend not available.
```
i saw this a lot of times, maybe its some other device its trying to add or something, lets delete everything we do not need for the base :)
which leaves us with the following settings:
![[Pasted image 20250730201210.png]]
let see
we still crash on the begining:
![[Pasted image 20250730201337.png]]
ok, lets go back to the options advanced and return it to bios
ok that takes us back to CDBOOT: Couldn't find BOOTMGR
this gives me an idea, what if i will burn one of my flash drives as a bootable device with the ISO of the RT-OS, and will let it load it at the beginning, lets see :)