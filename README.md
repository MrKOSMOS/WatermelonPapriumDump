*Reminder, if you like these repos, fork them so they don't disappear*
https://github.com/ArcadeHustle/WatermelonPapriumDump/fork

Big thanks to Fonzie for allowing this to be published.
- written by hostile, with supporting information from the community at large!
<p align="center">
<img src="https://github.com/MrKOSMOS/WatermelonPapriumDump/blob/main/images/FonzieWMProjectLittleMan.jpg">
</p>

* [Pseudo-Legal opinion](#pseudo-legal-opinion)
* [Project Little Man](#project-little-man)
   * [Current Progress](#current-progress)
   * [DATENMEISTER DT128M16VA1LT](#datenmeister-dt128m16va1lt)
      * [DT128M16VA1LT parts related to data storage, and game logic.](#dt128m16va1lt-parts-related-to-data-storage-and-game-logic)
         * [Intel® MAX 10 FPGAs](#intel-max-10-fpgas)
         * [STM32F4](#stm32f4)
      * [MirrorBit Flash](#mirrorbit-flash)
      * [i2c EEPROM](#i2c-eeprom)
   * [Useful tools](#useful-tools)
      * [Cart Specific detail](#cart-specific-detail)
         * [Megawire 4.0 (MW4.0)](#megawire-40-mw40)
         * [Exposed vias on rear of cart](#exposed-vias-on-rear-of-cart)
         * [Debug headers?](#debug-headers)
   * [References](#references)
      * [Grandious Ideas](#grandious-ideas)
      * [Failure to deliver](#failure-to-deliver)
      * [Need for Change!](#need-for-change)
      * [Drama](#drama)
      * [An amazing Paprium troll, ahead of their time](#an-amazing-paprium-troll-ahead-of-their-time)
      * [Little men](#little-men)
      * [Fun Quotes](#fun-quotes)
      * [Youtube Interviews &amp; Documentaries](#youtube-interviews--documentaries)
      * [Support situation](#support-situation)

# Pseudo-Legal opinion
Additional text relevant to this document can be found below:<br>

Exemptions to Prohibition against Circumvention of Technological Measures Protecting Copyrighted Works<br>
Seventh Triennial Section 1201 Final Rule, Effective October 28, 2018 <br>
https://library.osu.edu/document-registry/docs/1027/stream<br>
"Video games in the form of computer programs, where outside server support has been discontinued, to allow individual play and preservation by an eligible library, archive, or museum"<br>

https://library.osu.edu/site/copyright/2019/03/20/2018-dmca-section-1201-exemptions-announced/ <br>
"Video games in the form of computer programs, lawfully acquired as complete games 37"<br> 
"CFR §201.40(b)(12)"<br> 
"For personal, local gameplay; or To allow preservation in a playable format..."<br>

"Computer programs protected by dongles that prevent access due to malfunction or damage and which are obsolete. A dongle shall be considered obsolete if it is no longer manufactured or if a replacement or repair is no longer reasonably available in the commercial marketplace."<br>
https://www.copyright.gov/fedreg/2006/71fr68472.html<br>

"The final rule allows eligible libraries, archives, and museums to circumvent technological protection measures on certain lawfully acquired computer programs (including video games) to preserve computer programs and computer program-dependent materials."<br>
https://clinic.cyber.harvard.edu/2018/10/26/a-victory-for-software-preservation-dmca-exemption-granted-for-spn/<br>

"Exemption to Prohibition on Circumvention of Copyright Protection Systems for Access Control Technologies"<br>
https://www.govinfo.gov/content/pkg/FR-2018-10-26/pdf/2018-23241.pdf<br>

Please note that the following text is considered ["for purposes of good-faith security research"](https://www.ftc.gov/news-events/blogs/techftc/2016/10/dmca-security-research-exemption-consumer-devices). This write up will give you all the knowledge, and access you need to backup and preserve your Genesis MegaDrive Paprium cart as supplied by Watermelon Games. It will also serve as an academic tome on the security ramification of Voltage Glitching the STM32F4 MCU, FPGA security through obscurity, physical protection methods, and anti tamper techniques.<br>

President Joe Biden’s latest executive order is a huge win for right to repair because it specifically calls out "unfair anticompetitive restrictions on third-party repair or self-repair of items", just like the DT128M16VA1LT concept in Paprium imposes on any end user lucky enough to acutally obtain the game. 
https://www.whitehouse.gov/briefing-room/presidential-actions/2021/07/09/executive-order-on-promoting-competition-in-the-american-economy/<br>

# Project Little Man 
This project details the active efforts to dump the contents of the Watermelon Games Paprium cart, and understand the logic that allows the cart to function.<br>

The [Paprium Press Release](http://www.paprium.com/press/?language=en) from 03/16/2017 brought many promises that simply never manifested into reality. At this point many people have recieved their Paprium cart, where as many others have not. Some of those that have carts in hand, happen to have broken, unusable carts. There is no replacement path, there are no support options, you simply have the pleasure of owning a brick. What can you do? Shitpost? Bellyache, and whine? Quit being a "little man", and take matters into your own hands? "Rule, Be Ruled, or Die"!<br>

[![Paprium launch](http://img.youtube.com/vi/f3CTqTzkgZQ/0.jpg)](https://www.youtube.com/watch?v=f3CTqTzkgZQ)<br>

The goal of this project is to empower Paprium cart owners to ensure that their investment is protected well into the future. Design flaws such as BGA voiding in the cartridge manufacturing process make it succeptible to failure. It is literally a ticking timebomb, and it will likely fail eventually.<br>

## Current Progress
Update: 10/3/21<br>
- Intel 10M02 (10M04 dev board ordered for research)<br>
- STM32F4 (custom SWD breakout PCB sent to Fab House)<br>
- 24C64WP EEprom (dumped)<br>
- Spansion GL064N Series Flash (dumped)<br>
- Game Audio has been extracted
- Game 4Bpp & Palate images have been extracted
- Game Strings have been extracted
- Sprite Sheets! 

https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/ChipDumps/RT809H/S29GL064N90BFI03%40BGA48_20210924_142237_DECODED.BIN<br>
https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/ChipDumps/RT809H/24_64_1.8V_20210924_215810_goodcart.BIN<br>
https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/Extracted/audio/AllSoundsDirty.wav<br>
https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/Extracted/strings/gametext.txt<br>
https://github.com/ArcadeHustle/WatermelonPapriumDump/tree/main/Extracted/4BPP_bmp<br>
https://github.com/ArcadeHustle/WatermelonPapriumDump/tree/main/Extracted/sprites<br>

## DATENMEISTER DT128M16VA1LT
The DT128M16VA1LT is supposedly a "custom" chip made by [Daten Semiconductor](https://web.archive.org/web/20190706065046/http://datensemi.com/), that is really just a bunch of commodity parts covered in black [epoxy glob top encapsulant](https://www.youtube.com/watch?v=dRsl4c6NM8U). Never mind that it has been proven that ["Datenmeister DT128M16VA1LT chipset is fake"](https://papriumfiasco.wordpress.com/tag/datenmeister/), or that the website of the company that "makes" it, was originally registered to Fonzie.<br>
<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/datenwhois.png"><br>

The Datenmeister serves as the central piece of technology driving the Paprium cart. The only problem is, that it does not exist, at all. In reality, it is just handful of common components.<br>
https://twitter.com/MyLifeInGaming/status/1341092115250630656

Any Paprium ROM archival efforts would have to revolve around exploiting weaknesses in the "DT128M16VA1LT" components.

### DT128M16VA1LT parts related to data storage, and game logic. 
The actual technology in the ficticious "DT128M16VA1LT" from the Paprium cart is made up of known ICs that are succeptable to known weaknesses, and potential attacks. Being beneath black goop does not at all make the chips impervious to attack.<br>

It should in practice be trivial to interface with each of the major componets. The major hurdle right now is physical access to each component, or it's pinout due to the black epoxy.  

#### Intel® MAX 10 FPGAs
Altera 10M02SCU169C8G FPGA (UBGA169)<br>
https://www.mouser.com/datasheet/2/612/m10_overview-2401081.pdf<br>
https://www.intel.com/content/dam/www/programmable/us/en/pdfs/literature/an/an556.pdf

The Intel "10M02" FPGA on the Paprium cart ["may allow an authenticated user to potentially enable escalation of privilege and information disclosure via physical access"](https://www.intel.com/content/www/us/en/security-center/advisory/intel-sa-00349.html). The vulnerability has been assigned [CVE-2020-0574](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-0574). Dr. Sergei Skorobogatov of the Dept of Computer Science and Technology, University of Cambridge, Cambridge, UK, has been credited with reporting this issue. His papers and persentations on the subject are linked below:<br> 
https://arxiv.org/abs/1910.05086<br>
https://arxiv.org/pdf/1910.05086.pdf<br>
https://www.cl.cam.ac.uk/~sps32/HWIO_MAX10.pdf<br>
https://www.youtube.com/watch?v=Ev28MXJdjHE<br>

Sergei's research outlines several weaknesses that can aid in archival of Paprium's Max10 FPGA contents:<br>

"Verify Protect fuse only protects the configuration Flash memory (CFM) but leaves user Flash memory (UFM) fully accessible"<br>

"Encrypted POF Only fuse on its own does not protect JTAG access to the Flash memory"<br>

"Write access to both user Flash and configuration Flash is still possible. This can be used for modification attacks, for example, to extract the encrypted bitstream"<br>

"AES decryption always leaves distinctive power traces clearly distinguishable for different keys and different data. In combination with Flash modification attacks this can be used for encrypted bitstream extraction."<br>

"Semi-invasive attacks in the form of laser fault injection were found to be capable of bypassing all security protection fuses in MAX 10 devices."<br>

All of these vulnerabilities can in theory be used to dump the FPGA that is present on the Paprium cartridge. Although the bitstream can not be easily reverse engineered, it could absolutly be used in a remanufactured cart, assuming it plays some role in security, or audio and GFX rendering<br>

#### STM32F4
ST STM32F446ZEJ6 MCU (UFBGA144)<br>
https://www.st.com/resource/en/datasheet/stm32f446re.pdf<br>
https://www.st.com/resource/en/application_note/dm00493651-introduction-to-stm32-microcontrollers-security-stmicroelectronics.pdf<br>

Assuming that the STM32 is making use of RDP based protection it will require some special conditions in order to dump the firmware. If it is on the otherhand not protected, a physical connection to the SWD pins will be all that is needed. Once freed from the black epoxy, the chip is more succeptable to examination, and attack.<br> 

Similar to the Intel FPGA, the STM32F4 inside the Paprium cart is known to be vulnerable to voltage glitching attacks that should aid in archival of Paprium's data. The attacks have moved from theory, and manual one off demonstrations to now being available in ready made productized form with tools like [ChipWhisperer](https://www.newae.com/chipwhisperer). Various exploitation demonstrations have occured outside common lab constraints, and SDK kit based testing.<br>

Real, actual products have been attacked at this point. The exploitation techniques are reliable:<br> 
https://lists.gnupg.org/pipermail/gnuk-users/2020-February/000243.html<br>
https://www.synacktiv.com/sites/default/files/2020-11/presentation.pdf<br>
https://tches.iacr.org/index.php/TCHES/article/download/7390/6562/<br>
https://blog.kraken.com/post/3662/kraken-identifies-critical-flaw-in-trezor-hardware-wallets/<br>

[TheHpman](https://wiki.mamedev.org/index.php/TheHpman) appears to have done some basic reversing of the Paprium cart mini game that was dumped via traditional techniques. Watermelongames included a security mechanism to prevent dumping of the actual game, instead serving up a "mini game" when dumping is attempted. The logic used by the carts STM32 is explictly mentioned on his Twitter account as he explains his disassembly efforts:<br>
https://twitter.com/The_Hpman/status/1383191393393389570<br>
https://twitter.com/The_Hpman/status/1383191380743356416<br>

Commerical RE company [BreakIC](http://www.break-ic.com) aka Mikatech will dump the STM32 for a fee of $6500 USD, claiming that "The tools needed to read it costs USD2million". We have reliably used Mikatech in the past for less costly extractions, and originally found them because their marketing claims that they are "World first mcu cloning company". Worst case scenario, we could in theory pay to have the Paprium STM32 chip dumped via their expensive machine.<br>

<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/breakIC.jpg">

Alternatively practicing on [STM32F4 dev boards](https://www.st.com/en/evaluation-tools/nucleo-f446re.html) using a standard ChipWhisperer setup should set the stage for dumping the Paprium STM32F4 using standard community accessible tools. Again, assuming there is RDP protection enabled at all!<br>

Similarly starting with the standard [STM43F4 "UFO" target board](https://store.newae.com/stm32f4-target-for-cw308-arm-cortex-m4-1mb-flash-192kb-sram) is a great way to practice before moving on attempting to attack the Paprium cart.<br>

### MirrorBit Flash
Spansion GL064N Series Flash (BGA48)<br>
https://www.cypress.com/file/202426/download<br>

Reading the Spansion flash is confirmed to be possible with a standard Universal Programmer, and the appropriate adapter. Your adapter must also support the flash algorithm. We had to purchase an RT809H for example, because our Top3000 did not properly support reading the chip. 
https://www.aliexpress.com/item/32820731419.html<br>
https://www.aliexpress.com/item/32978614065.html<br>

You can see from the chip routing that the Flash data access for the running cart is gatekept by the FPGA.<br>
<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/flashdatalines.jpg">

### i2c EEPROM
24C64WP EEprom (SO8)<br>
https://www.st.com/resource/en/datasheet/m24c64-f.pdf<br>

Similarly reading the i2c EEPROM is confirmed possible with standard EEPROM readers, or even an [Arduino](https://learn.sparkfun.com/tutorials/reading-and-writing-serial-eeproms/all). It is sitting outside the black epoxy, making it easy to examine. 
<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/exposedi2cflash.jpg">
Example dumps can be found here:<br>
https://github.com/MrKOSMOS/WatermelonPapriumDump/blob/main/ChipDumps/RT809H/24_64_1.8V_20210924_215810_goodcart.BIN
https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/ChipDumps/RT809H/24_64_1.8V_20210924_220101_badcart.BIN

You can read the chip in place on the cart without removing it by using a pogo reader. 
https://www.ebay.com/itm/324696874863

## Useful tools
The standard tool for voltage glitching is the Chip Whisperer, STM32 is a default target in the "level 1" kit, so this seems like a natural fit for anyone wanting to play along:<br>
https://store.newae.com/side-channel-glitching-starter-pack-level-1/<br>
https://www.mouser.com/new/newae-technology/newae-chipwhisperer-lite-l1-kit/<br>

Before the ChipWisperer came along you often saw [FeelTech FY3200S](https://www.ebay.com/itm/402781810775) used in academic papers about voltage glitching STM32 MCUs. This device contains a USB API that can be used to script voltage changes. A [Python API](https://github.com/atx/python-feeltech) makes scripting easy.<br>

Keeping in mind of course that these tools may only be necessary if RDP protection is enabled on the STM32F4.<br>

### Cart Specific detail
The Paprium cart is a special unicorn. If you don't pay attention, you may perhaps miss some notable "features".<br>

#### Megawire 4.0 (MW4.0)
Described in the manual as being used to "Connect to PAPRIUM's NXT network and enable the game's online services". It can also be used because "Some game updates may be available for download. Nobody's perfect...", or for DLC that "can be purchased with GEMS".<br>

"Megawire 4.0 is a special connector that has 4 segments to it. There are 2 segments for data transfer & 2 for are for power & ground."<br>
https://warosu.org/vr/thread/7319474<br>

You can find the appropriate 4 Pole Stereo 2.5mm adapter easily on Amazon<br>
https://www.amazon.com/gp/product/B07ZT85PN7/<br>

#### Exposed vias on rear of cart
Vias on the cart expose the BGA ball array from the STM32F4, making the epoxy less effective at protecting it. 
<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/exposedVIAs.jpg">
<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/exposedVIAmirror.jpg">

This allows for access to SWD lines from outisde of the black epoxy obfuscation blob. 
<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/exposedSWD.jpg">

Attacking the cart through via access would require some effort to build a bed of nails, or some sort of effective jig. This is really intended as a last ditch effort in the event that the STM32 can't be free'd effectively from the epoxy. It is unlikely that chasing via's will be needed, but the information is good to have on hand.<br>

#### Debug headers?

There is a 9 pin header at the top of the cart labeled "DT", the functionality is not understood at this time. Several of the pins are GND, and three of the pins connect to themselves. The remaining pins may go to the Megawire interface, or to the Spansion flash. They may also simply be a red herring troll by Fonzie. <br>

<img src="https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/images/DT1.jpg"><br>

There is also an 8 pin header just below the STM32 above the cart connector that appears as if it may connect to the UART pins and be useful for the UART bootloader programming interface. In order to use it BOOT0 would need to be pulled to GND.<br>
https://github.com/ArcadeHustle/WatermelonPapriumDump/blob/main/ChipDocs/programming-an-external-flash-memory-using-the-uart-bootloader-builtin-stm32-microcontrollers-stmicroelectronics.pdf
<img src="https://github.com/MrKOSMOS/WatermelonPapriumDump/blob/main/images/8pindebug.jpg"><br>


## References
These are random related backstory items that make for good reading, or listening.<br>

### Grandious Ideas
https://web.archive.org/web/20190226071931/http://www.magicalgamefactory.com/en/blogs/wm-blog_1/<br>

### Failure to deliver
https://www.facebook.com/110283612372658/posts/2326873840713613/<br>

### Need for Change!
https://www.change.org/p/paypal-paypal-usa-please-transfer-the-money-to-watermelon-for-releasing-the-game-paprium<br>

### Drama
https://twitter.com/St1ka/status/1364024924873097216<br>

### An amazing Paprium troll, ahead of their time
https://papriumfiasco.wordpress.com/tag/datenmeister/<br>

### Little men
Fonzie ranting on Twitter calling everyone "little man", and complaining about PayPal. 
https://twitter.com/watermelongames/status/1365356392022966278<br>
https://twitter.com/watermelongames/status/1428150734361661440<br>
https://twitter.com/watermelongames/status/1366710552005906439<br>
https://twitter.com/watermelongames/status/1428156649823424512<br>
https://twitter.com/watermelongames/status/1428157032549556225<br>
https://twitter.com/watermelongames/status/1428159286388133892<br>
https://twitter.com/watermelongames/status/1428162198078164997<br>
https://twitter.com/watermelongames/status/1428164359923118086<br>

### Fun Quotes
https://www.youtube.com/watch?v=Nj2LM1rvFQ8&t=4550s<br>
st1ka: "A ROM dump will always happen, I believe Paprium has already Been dumped, if I'm not mistaken"<br>
Fonzie: "no no no no no no no no no no I don't think so I don't think so, I don't encourage anyone to dump anything"<br>
...<br>
"What about the customer"<br>
"These guys are lucky we don't have very strong lawyers"<br>

https://www.youtube.com/watch?v=Nj2LM1rvFQ8&t=5530s<br>
st1ka: "the fpga is primarily used as a copy protection"<br>
Fonzie: "... what ever is said is just some ideas, it is true it serves in some way as copy protection"<br>
"It has a memory interface"<br>
"the game is going realtime decompression, and this decompression algorithem is inside the one IC"<br>

https://www.youtube.com/watch?v=Nj2LM1rvFQ8&t=5650s<br>
Fonzie: "I chose component from the market, because I can not make my own IC".<br>
"I chose the IC from the market that fits the requirements, of course becuase it is not custom".<br>

https://youtu.be/lxByzNzWTlI?t=1300<br>
Fonzie: "The final state of testing we modified something on the game, but we could not test again"<br>
"We have to trust everybody to not put the cartridge on eBay. the problem is it was very big risk"<br>
"for sure someone with alot of money will try to take the cartridge and dump it"<br>

### Youtube Interviews & Documentaries

<a href="https://www.youtube.com/watch?v=xQTD0Z4tWvE" target="_blank">
 <img src="http://img.youtube.com/vi/xQTD0Z4tWvE/0.jpg" alt="PAPRIUM megadrive / genesis longplay part 1" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=sFfNuhEyzD0" target="_blank">
 <img src="http://img.youtube.com/vi/sFfNuhEyzD0/0.jpg" alt="PAPRIUM megadrive / genesis longplay part 2" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=2it-3NwZ9Go" target="_blank">
 <img src="http://img.youtube.com/vi/2it-3NwZ9Go/0.jpg" alt="PAPRIUM megadrive / genesis part 3 - instruction manual & manga investors" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=kXLtnqbeBNI" target="_blank">
 <img src="http://img.youtube.com/vi/kXLtnqbeBNI/0.jpg" alt="What Happened to Paprium? A Documentary - St1ka's Retro Corner" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=kOiM7ikcBx0" target="_blank">
 <img src="http://img.youtube.com/vi/kOiM7ikcBx0/0.jpg" alt="What Happened to Paprium? A Documentary (Part 2) - St1ka's Retro Corner" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=jbBIua_BXjc" target="_blank">
 <img src="http://img.youtube.com/vi/jbBIua_BXjc/0.jpg" alt="What Happened to Paprium? A Documentary (Part 3) - St1ka's Retro Corner" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=VUaAEqiIi_s" target="_blank">
 <img src="http://img.youtube.com/vi/VUaAEqiIi_s/0.jpg" alt="Paprium Documentary - Complete Series | Movie Length Documentary | St1ka's Retro Corner" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=kATTdGY8HkI" target="_blank">
 <img src="http://img.youtube.com/vi/kATTdGY8HkI/0.jpg" alt="PAPRIUM - THE FONZIE INTERVIEW (English Subtitles)" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=bhHp5Q7LUbs" target="_blank">
 <img src="http://img.youtube.com/vi/bhHp5Q7LUbs/0.jpg" alt="The Paprium SCANDAL" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=fukGY5wDTiQ" target="_blank">
 <img src="http://img.youtube.com/vi/fukGY5wDTiQ/0.jpg" alt="Paprium Update: Fonzie FINALLY Breaks His Silence" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=PdUTPv038HE" target="_blank">
 <img src="http://img.youtube.com/vi/PdUTPv038HE/0.jpg" alt="Analyse de l'interview de Fonzie" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=lxByzNzWTlI&t=514s" target="_blank">
 <img src="http://img.youtube.com/vi/lxByzNzWTlI/0.jpg" alt="Scene World Podcast Episode #109 - Watermelon Games' CEO Gwénaël Godde aka Fonzie" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=svHHCMNOvN8" target="_blank">
 <img src="http://img.youtube.com/vi/svHHCMNOvN8/0.jpg" alt="L'entrevue la plus puissante avec Gwénaël 'fonzie' Godde PDG de Watermelon Partie 1" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=x482W3m8P7I" target="_blank">
 <img src="http://img.youtube.com/vi/x482W3m8P7I/0.jpg" alt="Entrevue avec 'Fonzie', PDG de Watermelon #teaser" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=BXr229U9430" target="_blank">
 <img src="http://img.youtube.com/vi/BXr229U9430/0.jpg" alt="Entrevue avec fonzie, suite et fin." width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=Nj2LM1rvFQ8" target="_blank">
 <img src="http://img.youtube.com/vi/Nj2LM1rvFQ8/0.jpg" alt="Paprium's Creator: An Interview | St1ka's Retro Corner" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=ZgTRyHRtdCA" target="_blank">
 <img src="http://img.youtube.com/vi/ZgTRyHRtdCA/0.jpg" alt="FAQ watermelon : Les réponses" width="240" height="180" border="10" />
</a>
<a href="https://www.youtube.com/watch?v=axvJSqKApdo" target="_blank">
 <img src="http://img.youtube.com/vi/axvJSqKApdo/0.jpg" alt="Scene World Podcast Episode #125 - Watermelon Games - Fonzie Part 2" width="240" height="180" border="10" />
</a>

### Support situation
https://twitter.com/Scene_World interview with https://twitter.com/watermelongames<br>
https://twitter.com/Scene_World/status/1445178396988874754<br>

https://www.youtube.com/watch?v=axvJSqKApdo&t=1936s<br>
Q: So before this interview we actually spoke a couple of times on the phone and you told me that you found a way to make an update on Paprium cartridge for the compatibility and perhaps tell me about that because I'm waiting to make to make my game running on my version one of my megadrive"<br>

https://www.youtube.com/watch?v=axvJSqKApdo&t=1957s<br>
A: "Yes Yes many people ask this online at least we got uh not many customers asking to us on our customer support but many people ask online so I think there's some problem with that. It's a serious problem and uh I have to confirm I would say it should be fine, but I I don't want to give something and then I don't want to tell anything until I want 100% sure people can do it at home themselves. So that's the only point I'm not sure if people have to return their cartridge to some service point or if they can do it themselves. That's the thing I need to confirm but I would not hide that the last couple of months have been very tough and uh I'd say <haha> I have to decide on which thing I focus. My main focus was to not get bankrupt mostly"<br>
...<br>
https://youtu.be/axvJSqKApdo?t=2033<br>
"This kind of stuff does not work well if the company is not in a good shape, you don't want to ship something and of course if we had everything running fine if our shop was still running I could have paid someone full time to do this servicing, it's no problem. We can even pay for the shipping is not so expensive the problem is that there is no way to do anything like so I don't want to I I I want to wait and see how things are going to happen. Then we can give a good service to the customers becasue it's not a at the moment it's not good. Like we don't the customer support. I have to shut it down like some customers they call us on the phone, it's fine, but when some people they send emails so but it's um too many people make fake requests or to get free games. It takes a lot of time people don't see that like it takes a lot of time to figure that out and uh we have nobody to do the customer support at the moment. <br>
...<br>
https://youtu.be/axvJSqKApdo?t=2101<br>
"Oh there's nobody. So I got to decide if I do it, and then nothing else is done, or it's like I got to decide what I want to do like. I think it's better for now that we try to solve this situation. We try to move forward and then we when things is back on track we can fix every people's problem. But if I start handling the case one by one uh in a in a cheap way, it's not going to be good. So yeah, I'm sorry for that some cusomers are waiting and they get the personal return but like I keep saying that I cannot ship you back. There's no way like as they say oh hey but I can pay but I can pay. Even if you pay I cannot ship back to you becasue I have so many uh things to pay before I got to ship your things. <br>
...<br>
https://youtu.be/axvJSqKApdo?t=2159<br>
"If the kickstarter goes well if we get back on track I can arrange a customer service. Someone to contact every customer and fix this, yeah by the way like, a yeah, it's my the biggest issue is for people who are living in the US because um in europe uh maybe we can have a even center in paris or in germany. Some people who live around can bring their cartridge you can fix them. But um in USA it's a very big country so you can't do this easily. So he has to do he has to be some shipping or people to do it at home. We will see, we will see. I don't want to announce this thing yet because uh I'm a very um let's say I have good experience now and I'm saying something, and the next day it goes horrible.<br>

