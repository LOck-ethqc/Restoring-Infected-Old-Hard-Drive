# Restoring 10+ Years Old Infected Hard Drive
## Overview
This project will showcase a step-by-step exhaustive process explanation and Proof-of-Concept of how to safely handle and examine an infected external Hard Drive/USB, what safe methods should be applied to inspect its behavior to detect any malicious activity, and to recover lost data if possible.

## Story behind the infected Hard Drive
Once upon a long time—more than 10 years ago—my family, proudly, used the Hard Drive in question as the primary digital photo-collection storage of the family’s precious memories, without making a backup in case of the Drives’ failure. Never they expected, when one day the Hard Drive was plugged into our old pc, and one of the family members downloaded a malicious file—Trojan I suppose, and guess what happened next? It was infected with a virus, yay!

## Objectives
-	Inspecting the Hard Drive in an isolated environment.
-	Remove the remains of the malicious virus if any was found.
-	Make a disk image of the Hard Drive to prepare for recovery (Failed).
-	Recover as many important files as possible.

## Hurdles & Complications
-	Severe Hard Drive flapping.
-	Probability of active virus.
-	Possibility of unrecoverable files.

## Information about the Hard Drive in question
````
Brand: Samsung
Product Family: G Series
Product Name: G2 Portable 500GB
Model Name: HX-MU050DC/GB 
Serial Number: E27PJ10Z840661
````
[For more information about the Hard Drive](https://icecat.biz/en-ae/p/samsung/hx-mu050dc-gb2/g+series-external+hard+drives-hx-mu050dc-4013761.html)

![Untitled design (1)](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/e46da3ed-2b54-49f3-b4f2-4b7ecb7905cb)

## Getting Hands Dirty
### Isolation & Sandboxing
Before plugging the bad boy into my Workstation and compromising every single 0 & 1 of files that I had, one must utilize Sandboxes to isolate the Hard Drive into a safe environment. This can be accomplished in two different ways:
1) Windows Sandbox (Physical Machine).
2) VMware/VirtualBox (Virtual Machine).

Choosing the former would be more convenient and time-saving, but it is only available in Windows 10 Pro and Enterprise versions (F@K MICROSOFT!!!, this iconic line is Copyrighted by Space Force - Netflix).
Obviously, I have neither of the supported Windows versions, so I had to work with the latter choice.

Since I’m dealing with external drive, and was compelled to choose a virtual route for Sandboxing, I realized something, and asked myself, “What if I plugged the infected Hard Drive and it executed on my physical machine rather than my virtual one?”

This question had me perplexed on how to approach the dilemma. I brought a non-infected hard drive to test my theory, and I was completely right. The physical machine executed the non-infected hard drive while the virtual machine didn’t.

Why?

The virtual machine can’t recognize external devices unless there is a USB Device Filter. We must add a filter into the virtual machine to expect the external device to be executed in the virtual machine. To do that, follow the next steps accordingly:
1) Start your VM and press right-click on the USB Devices on the bar

![2](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/ba7c668c-d934-422d-b019-62f935ad764d)

3) Click on USB Settings

![3](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/2a4a073e-9270-4941-9efd-c8de9bba7508)

4) A Pop-up screen of the settings will appear, click on the top icon on the right

![4](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/ce0ba848-16c0-4d3c-96d7-7c5f501cde41)

A new USB filter will appear, ready to use!

![5](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/8c1ac8c4-e5ee-407c-8289-039892b36d9d)
> [!CAUTION]
> Make sure the box is checked!

You can edit the filter and change its characteristics, it’s up to you.

![6](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/4c1f8405-42b7-4c41-94d1-92073f28619d)

Now, let’s put what we did to the test.
I plugged in the infected Hard Drive and Voila!

![7](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/4022c54d-89e7-4c5e-a2b8-e2258aa1dd63)
The Infected Hard Drive has been isolated/sandboxed successfully!

I proceeded and opened the Drive to check its contents and what remained after the infection.

![8](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/e8ad083c-8e3d-4404-8aff-de74893715d0)

I checked each directory, and nothing suspicious or malicious was found.

Since no suspicious files nor abnormal activities were detected, I concluded that the accused Hard Disk was not guilty and was free of viruses.


### What if the Hard Disk Contained Suspicious Files?
There would be a more sophisticated and in-depth check for suspicious files using malware inspection tools, for example: VirusTotal & Hybrid Analysis.

Let’s demonstrate a real example with another external device that actually contains malicious files!

![Untitled design](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/56e70c7b-974f-42c5-802c-ebda3d6fc49e)

I repeated the same careful approach when plugging in the malicious USB.

![1 1](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/8bf0dc28-7547-46e0-b720-da2177f523ac)
![1 2](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/b3402cd6-bc31-4402-8061-d9730f4f2d86)

I checked text files and read their contents. Nothing malicious was as clear as the sky. Hence, I needed to use malware inspection tools.

I started with `acenet_client_release.exe` since it was an executable file.

**VirusTotal Report**
![2 1](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/39878ed5-036c-4e90-93af-3ef8d30597f2)

**Hybrid Analysis Report**
![2 5](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/0fa652f2-150a-495f-afa1-278599dad19a)
![2 55](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/626f17d9-894f-4870-bcc0-9a91c1e0dfeb)

VirusTotal flagged it as "malicious", unlike Hybrid Analysis, which flagged it as "no specific threat" even though Flacon Sandbox Report had some suspicious indicators. We could say it was a tough find, but it was detected in the end.

The second file I inspected was `claw.exe`

**VirusTotal Report**
![2 2](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/0accff6b-4ebc-480b-b11a-a87d7b1862e9)

**Hybrid Analysis Report**
![2 3](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/98ff8f68-5281-4187-b7e6-50f2a1314641)
![2 4](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/a34fcb34-7ae0-45df-aa1b-7365d1fa73ea)

This time, both detected the file and flagged it as "malicious" and "suspicious" respectively.


Lastly, I found an evil file... Truly wicked and malicious, it was `yrnjc.pif`

**VirusTotal Report**
![2 6](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/05ea50ce-3660-4b20-ad36-42739ab37ec7)

**Hybrid Analysis Report**
![2 7](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/7445ed79-5ff2-47ae-8228-e2795256c9df)
![2 66](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/637e63b6-26de-4d63-9f2b-96b083d3630b)

This malware was so alarming, I actually got scared and intrigued at the same time. I went and researched about it, trying to understand it more, since it was infamous within AVs.

![2 8](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/46dbdb30-b881-4e87-ba13-af625036adbf)

Turns out the virus is called "Sality" and it is a classification for a family of malicious software that affects Windows files precisely.

The USB examined was a dump of viruses collected over the years. I don't think I will remove the infected viruses or get rid of the USB. I will keep it safe just in case I might do some reverse-engineering somewhere in the future :D

But for those who would like to take action, if malicious files were indeed detected and confirmed, before doing anything, you must understand that you must handle the malicious files carefully and DO NOT open/execute the malicious files under any circumstances. Even better, Lock the infected files in a password-protected folder just in case.

You have two choices in such a situation:
1) Deleting the malicious files directly.
2) Full Format the Hard Disk

Choosing the first choice above the second is not always as sufficient and reassuring; deleting the malicious file does not guarantee the removal of the malware. Some malware resides in the Boot Sector which makes them almost persistent even when the malicious file is deleted.They stay active in the Boot Sector waiting to be plugged into any machine to latch itself and infect the new victim.

The second choice removes the malware from its roots by deleting the files through overwriting the file sectors and the Boot Sector, so that nothing remains whatsoever. Since the Full Format overwrites all the sectors, there would be no way to recover the important personal files—not the malicious files—that were deleted. Therefore, it is recommended to extract any important files and save them in a safe place before formatting.

There is a third choice, which is Low-Level Formatting, used when dealing with advanced persistent malware where the depth of its roots resides in the firmware. It overwrites Every single area with no exclusions whatsoever.


### Creating Disk Image from The Hard Disk
I used FTK Imager to create a Disk Image but failed due to the flapping problem with the Hard Disk. The problem cause is unknown; it is either from the Hard Disk or the cable connector. Either the cable connector’s pins are worn out, or the Hard Disk slots are worn out. I suspect the Hard Disk is causing the problem due to its age.
When the cable connector’s pins are aligned and attached to the Hard Disk slots, no electrical connection is established, unless I press down on the cable head, and it still sometimes disconnects and reconnects abruptly.
I tried to hold down the cable head the whole time while trying to create the Disk Image, but because of the abrupt disconnecting, it failed. Therefore, I canceled the Disk Image copying.

### Recovering Files
To recover the deleted files, I utilized Autopsy to inspect the Hard Disk.
First, I needed to run Autopsy in Administrator mode(to be able to scan the local disk)

![13](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/c997737b-7f83-4069-9cad-1d131e147370)

Then Opened a New Case and Chose a Data Source Type

![14](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/c494ca00-891f-4d13-88fc-c35c03a56c80)
![12](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/9efc2a55-1f8d-4580-860c-fe3fffcfec2b)

I picked the Hard Disk and Ingest Modules as needed

![15](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/725c6211-637a-414a-b320-819dd2e3246d)

Autopsy started scanning the Hard Disk and greeted me with its main interface. Luckily, the virus did not overwrite the old files when they got deleted.

![9](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/46e48fa8-b025-423e-af99-898d873d5f2f)
![10](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/69cbd645-1014-4ca7-886a-4b73e3857b7d)

I found deleted files that were taken back from 2008.

![11](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/3cd6963d-72eb-401f-818a-54c2173f40dd)

I recovered what I needed, mostly old pics ;D

I’ll share one of them <3

![16](https://github.com/LOck-ethqc/Restoring-Infected-Old-Hard-Drive/assets/90512716/e720b3e8-c9b2-494f-9535-a9036a7efa73)

