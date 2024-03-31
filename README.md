# ATX form factor 80286 AT mainboard PCB Rev 1


## Current status(march 2024): This project is currently in pre-testing phase, the designs have been ordered from a PCB house.

The project consists of a ATX mainboard and a ISA memory card.

Purpose and permitted use, cautions for a potential builder of this design
This project was created for historical purposes out of love for historical computing designs and for the purpose of enabling computing enthousiasts with a sufficient level of building and troubleshooting expertise to be able to experience the technology by building and troubleshooting the hardware described in this project.

Besides the GPL3 license there are a few warnings and usage restrictions applicable:
No guarantees of function or fitness for any particular or useful purpose is given, building and using this design is at the sole responsibility of the builder.

Do not attempt this project unless you have the necessary electronics assembly expertise and experience, and know how to observe all electronics safety guidelines which are applicable.

It is not permitted to use the computer built from this design without the assumption of the possibility of loss of data or malfunction of the connected device. To be used strictly for personal hobby and experimental purposes only. No applications are permitted where failure of the device could result in damage or injury of any kind.

If you plan to use this design or any part of it in new designs, the acknowledgement of the designer and the design sources and inspirations, historical and modern, of all subparts contained within this design should be included and respected in your publication, to accredit the hard work, time and effort dedicated by the people before you who contributed to make your project possible.

No guarantee for any proper operation or suitability for any possible use or purpose is given, using the resulting hardware from this design is purely educational and experimental and not intended for serious applications. Loss of data is likely and to be expected when connecting any storage device or storage media to the resulting system from this design, or when configuring or operating any storage device or media with the system of this design.

When connecting this system to a computer network which contains stored information on it, it is at the sole responsibility and risk of the person making the connection, no guarantee is given against data loss or data corruption, malfunctions or failure of the whole computer network and/or any information contained inside it on other devices and media which are connected to the same network.

When building this project, the builder assumes personal responsibility for troubleshooting it and using the necessary care and expertise to make it function properly as defined by the design. You can email me with questions, but I will reply only if I have time and if I find the question to be valid. Which will probably also lead to an update here. I want to primarily dedicate my time to new project development, I am not able to do any user support, so that's why I provide the elaborate info here which will be expanded if needed.

# Acknowledgements

This project was inspired by:
- IBM Corporation who introduced the 16 bit AT concept after their PC and XT product lines
- concept and software of the XT-IDE universal BIOS https://www.xtideuniversalbios.org
- discussions with members of the German DOS Reloaded forum
https://dosreloaded.de/forum/thread/6811-diy-diskretes-logik-atx-turbo-at-286-mainboard-ohne-chipsatz/
- discussions with members of the VCF forum
https://forum.vcfed.org/index.php?threads/project-to-create-an-atx-80286-mainboard-based-on-the-ibm-5170.1243108/
I want to thank users Makefile, acgs, sergey, Timo W., sharkcz, Hpela, Alvaro64, Chuck(G), Theoryboy, modem7, Toportyán, Hak Foo, sorphin, ajacocks, Eudimorphodon, lowen, jonny64, HoJoPo, mogwaay, upnorth for their responses, constructive ideas and discussions, and technical feedback!

In particular I want to thank Johann (jonny64) who took an active concern and participation in my project to reverse engineer the PAL chips on the 5170 mainboard.
This process has been extremely difficult and Johann helped a lot by programming python scripts to quickly be able to analyze large volumes of logic equation information.
Resulting from our cooperation Johann has developed a reverse engineering pythone program called "pete" and a script which can generate the PAL fuse maps from reverse analysis which can be directly programmed into a GAL. He is planning, or has published his work in the mean time on GitHub so be sure to search for his project here if you are doing similar work on PAL ICs used in old devices.

User Alvaro64 from Spain was very kind to provide friendly discussions and various information and he even offered me to borrow his legacy Intel mainboard for checking and analysis.

I was happy to see some reactions from Sergey who also did some amazing work to design and build various classic PCs. He developed a BIOS of his own and a HD Floppy supporting BIOS extension.

User lowen gave me some very useful time saving tips in using CPLD programmable logic from Atmel/Microchip, to be able to more easily and quickly get started with suitable CPLD parts in this project.
This will be my first programmable logic project which I will explain below.
User Eudomorphodon provided me some valuable feedback in terms of which type of logic would be possible to exist within the IBM PALS which was a big issue and problem to determine exactly what IBM did in their PAL programming, literally costing me a few weeks. 
User sharkcz was very helpful for pointing me to the Copam PC-501 schematics where I found more clues about the 80287 coprocessor control circuits which are also located in a PAL on the IBM 5170.
User Chuck(G) also provided various information and wrote extensive useful information about PAL chips and how to reverse engineer them.

I thank Charles MacDonald for developing his PAL read adapter and PA.EXE software which reduces the logic equations.
As I mentioned, Johann(jonny64) developed his own version of a PAL analyzer named "pete" which can do a few more advanced things to be able to do very important logic reductions and conclusions on RAW PAL read data from Charles' adapter. Especially is "pete" able to detect certain inputs on a PAL which sometimes switch to operating as an output. So the scripts Johann made can conclude this mode of operation by itself and also can reduce the subsequent logic consequences of this operation mode in the logic equations. If we don't have this automatic function from pete, it will be the person doing the analysis who will need to reason what is happening back from the observations, which is what I have initially done myself, it was quite a frustrating process to discover what was happening exactly inside the PAL U87 which caused me a lot of stress and lost sleep!

Everyone who commented and replied to all my posts, thanks for your help and friendship!

- datasheets, application notes and specifications by:
Intel (80286 datasheet)
LG Semiconductors (Goldstar) (GM82C765 FDC, GM16C550)
Standard Microsystems Corporation (FDC37C65C datasheet, FDC register access table)
Realtek (RTL8019AS)
NCR (53C400 SCSI)

Acknowledgements of people who were instrumental in preceeding developments upon which this design was elaborated:

[IBM PC development team](https://www.ibm.com/ibm/history/exhibits/pc25/pc25_birth.html)
[Some historical info](https://arstechnica.com/gadgets/2017/06/ibm-pc-history-part-1/)
[Bill Lowe](https://www.ibm.com/ibm/history/exhibits/builders/builders_lowe.html)
[Don Estridge](https://www.ibm.com/ibm/history/exhibits/builders/builders_estridge.html)

[XT-IDE universal BIOS project development team for developing the XT-IDE BIOS](https://www.xtideuniversalbios.org)
Amazing and extremely efficient software, fast disk access for XT and various AT computers.
Works with every IDE drive I have tested. Still under active development earlier in 2023.

All source data remains the copyright of the original creators and must be respected.
This design is only released for hobby computing enthousiasts and educational purposes, no profit is to be made from this design or derived work from it.

I have taken time to respectfully include all the above acknowledgements. This project has taken me almost a year up to the present time starting from all the research work I have done. If anyone or anything is left out, that is absolutely not intentional, please contact me and I will be happy to update this page further.

After elaborately studying the available source design files which inspired the system, I conceived this design with my own variations, circuit additions and changes which I see as improvements according to my personal design views and preferences. 

My purpose was a good and clear recreation in my own methods, and never to exactly copy the original. 
This project also serves to document the historical 16 bit AT PC design by implementing the fundamental concepts in a functional build which incorporates a lot of the original design concepts and functions which Don Estridge of IBM conceived. I admire Don and his work and I will attempt to explain in this text why his 16 bit AT concept was so important and elemental in promoting the industry standard development process!

I have designed various I/O control circuits using the chip manufacturer datasheets to determine the proper interfacing methods, ports etc suitable for this 286 AT design.
I also searched in many IO port documents to determine how to interface the onboard devices.

## How the project took more solid form

I started by finding a suitable mainboard for study, testing and analysis. I found a few examples from NCR and ARC however these proved to be frustratingly unstable and in a poorly operating condition. By no means would I have been able to base this project on those designs. Luckily I found an Ebay auction which offered an IBM 5170 mainboard for a very reasonable price. I repaired this mainboard and I have extensively tested it out. The IBM has the added advantage of being completely documented in their schematics which was very useful for this project.

I proceeded to draft modern KiCad schematics for the 5170 and subsequently modified the IBM designs to suit this project as much as possible. This involved removing the DRAM support logic and parity checking mechanisms from the schematics. Next I needed to reverse engineer the contents of PAL U87 which is elemental in the 5170 operation. Without the U87 design, a 5170 and its schematics will be useless and missing the vital operating circuits without which we have no AT! At the time there was not any documentation of the logic contained inside U87 to be found anywhere. So I proceeded to discover the logic by analysis. I used the method developed by Charles MacDonald initially and discussed with Johann to develop a utility program python script which I needed to form my conclusions about the actual operation of the U87 PAL.
Finally we succeeded to crack the design and even further simplify the logic equations of U87 to their most likely original PAL source code as originally created, probably by Don Estridge himself. If anyone has more information on how he developed the AT, please contact me, I am very much interested!

After I had the complete design of the 5170, I had to evaluate the large amount of logic chips which would be involved in case I would choose to use TTL chips only to implement the whole design. From the equations of U87, I could conclude why IBM chose this path of development. Adding all this additional logic would make the PCB even larger and make this whole concept impossible to properly implement on a single PCB in a practical PCB size. So I have concluded that I will need to use programmable logic in order to reduce the PCB area needed. And since I needed to use programmable logic anyway, I decided I had better do it properly to benefit from this concept the most. So I chose the ATF1508AS CPLD with the help and advice of user lowen. 

## Development path leading up to the first design revision
After reverse engineering PAL U87, I proceeded to draft schematics and did some initial parts placements on the mainboard. This quickly led me to conclude that in order to integrate many necessary devices onboard as planned, I would need to shift the entire memory subsystem and decoder CPLD onto a ISA adapter card. The BIOS and option ROM EPROMS are still placed on the mainboard because I like it more this way in a more traditional view of typical mainboards of the time.

I proceeded to draft my modified and new design of this project into schematics using KiCad and Quartus.

The complete design including my changes and additions is contained in and needs:
- a full ATX size mainboard PCB
- three 84 pin PLCC CPLDs which can be plugged into through-hole sockets
- a ISA memory subsystem card PCB containing the footprints for a total of 15MB of fully decoded SRAM memory.
This card provides 640KB of conventional memory, 128KB of UMBs at D0000 and E0000 segments with disable jumpers, and 14MB of XMS memory.
Each set of two 512KB SRAM ICs provides an additional megabyte of RAM for the system.
The amount of memory can be chosen by populating the desired amount of SRAM chips.
So basically this ISA slot card takes the function of the historically more typical DRAM SIMMs and implements the full PC memory space in SRAM memory.
Please note to observe the pin 1 mark of your particular RAM ICs and make sure you are not using a reversed pinout SRAM which would need to be soldered in flipped over orientation!

The mainboard provides two 16 bit IDE ports, a 8 bit SCSI port, a floppy drive interface, 16 bit Realtek LAN, USB to serial mouse using RP2040, discrete simplified LPT port, ATX power supply control, reset logic, and various LEDs to indicate certain system functions. The 64k BIOS is contained in two EPROMs on the mainboard and there is also a 32kb sized option ROM EPROM socket included on the mainboard. The design of this project is meant to use the XT-IDE BIOS option ROM software developed by XT IDE universal BIOS team, which needs to be configured and programmed into an option ROM EPROM IC which can be placed in the option ROM socket on the mainboard.

## BIOS to use
I recommend using a BIOS other than the IBM one mainly because the IBM BIOS is known to contain restrictions in operation and verifies the clock speed to lockout operation if the speed is raised.
So any similar BIOS to the IBM 5170 from other sources would possibly qualify to run on this project.
There have been BIOS code produced by ARC, COPAM, NRC and MR BIOS to name a few examples.

## Project status (march 2024)
I am currently awaiting the PCB production and delivery and I will proceed to build, test and possibly debug the first design revision.
I will need to get the CPLDs from recycled Chinese source programmed and functional in order to be able to test the project design for the first time.

So all the information on this GitHub page is openly provided for informational purposes only for everyone interested in such a project, with all the clear cautions and understanding that anything you do is at your own sole responsibility and no operation or useful purpose is implied or possible, please carefully read and understand the comments above. 

## (!) This project is currently completely untested and thus only a concept waiting to be confirmed
I will proceed with the work on this project when I have all the necessary parts and PCBs.
Updates will follow as soon as I have them.



