# Windows Embedded inspection
the other day i saw a funny thing, a gate at the train station got restarted, and all of a sudden:
![[Pasted image 20250730184209.png]]
this image is being popped
so that made me think, first of all why windows, other then user friendly i do not see any positive thing about running those machines on windows, and second of all, is that a hacker "wet dream?", so of course i had to find a version of it online and try to see what can i do with it
# Links:
took an iso image from here: https://www.microsoft.com/en-us/download/details.aspx?id=53898
am not going to upload it to the web because its 2.3Gb and github will be mad.
(sadly its the version for IoT stuff, but i believe its close enough, the RT is a bit harder to find for free)
# Tools I Will Use
1. wsl - windows subsystem linux, i dont like virtual machines, but VM can work here as well :)
2. VMware workstation - i need a way to run this windows version
3. nmap - network mapping tool
4. probably much more, but i will state it and say where you can get them :)
# Starting The VM
it can be an easy task, basically plug and play, but because IoT usually runs on embedded stuff, it can have some random interrupts that expects return values from the hardware, so it can be hard....
lets see :)
