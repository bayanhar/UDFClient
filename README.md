# UDFclient
forked from 13thmonkey.org : udfclient
http://www.13thmonkey.org/udfclient


13thmonkey.org : udfclient
Supported systems |  Releases |  Bugs and problem reporting |  Tips and tricks |  TODO

UDFclient

UDFclient is a userland implementation of the UDF filingsystem as defined by the OSTA group. UDFclient is designed to be a study platform and a run-up to a full read and write kernel level implementation.

UDFclient basicly provides a userinterface not unlike ftp(1) but differs in that it allways fetches or writes files recursively from the disc(s). As from version 0.4.9 it supports the basic get, mget, put, mput, mv, rm, mkdir, cd, lcd, free, pwd, lls command set. get and put can now also retrieve or store using different names than the origional.

NOTE work has started on the in-kenel version for NetBSD and is progressing well. This delays the development of UDFclient but important fixes have been backported into UDFclient allready. The kernel version is a new implemenation from scratch and could become UDFclient 2.x one day. Its currently imported in the NetBSD-current tree. UPDATE Its now running smoothly reading and writing all media upto version 2.01 and some support for writing 2.50 (non extendable metadata partition yet).
Supported systems

    NetBSD. UDFclient was developed on NetBSD and is running fine under both little endian and big endian machines. Actively tested on NetBSD/alpha, NetBSD/acorn32 (arm), NetBSD/sparc, NetBSD/pmax (mips). Tested are ATAPI CD-ROM, CD-RW, DVD+RW and on SCSI CD-ROM and CD-RW (might give problems; not tested recently).
    Linux. It runs fine under GNU/Linux and RedHat Linux. Like NetBSD it ought to work fine under both ATAPI and SCSI CD-ROM's when using the /dev/sg* devices. Note that under Linux 2.6.x ATAPI devices are read-only due to unresolved issues in the Linux ATAPI emulation blockdriver. update There seems to be a new resolved method for 2.6.x wich will be investigated and implemented soon i hope. Feedback on this would be much appreciated.
    FreeBSD. New in version 0.3.2 on is support for ATAPI/SCSI trough FreeBSD's CAM interface. Note that you'll need a fairly recent FreeBSD to be able to access ATAPI CD/DVD drives trough CAM since it was imported not long ago. Thanks to Andriy Gapon for the patch!
    DragonFly BSD. Although the pkgsrc system already had a patch for it in it, this patch is finally taken into version 0.5.5.
    OpenBSD. New in version 0.3.4 on is support for ATAPI/SCSI trough OpenBSD SCSI/ATAPI stack thats remarkable similar to NetBSD's though at small issues different. Thanks to Pedro Martelletto for the patch!

Releases

    UDFclient.x.x : (planning/in progress/delayed) Finally writing to recordable media (CD-R/DVD+R/DVD-R) etc. ! Preferably combined with a first fsck_udf implementation.
    UDFclient.0.8.8 : Minor release fixing a bug in strlcpy, cheats on linux's missing creation time, fixes compilation errors under CLang and adds the NetBSD man pages for newfs_udf and mmc_format. Thanks Pali for pointing them out!
    UDFclient.0.8.7 : Minor release fixing newfs_udf bug that would not detect an overflow on the number of sectors. It now allows for discs bigger than 2tb.
    UDFclient.0.8.6 : Minor release fixing compilation on systems that have undetected or unsupported SCSI support.
    UDFclient.0.8.5 : Minor release fixing some bugs that had crept in, enhancing cd_disect a bit by printing out previously obmitted bits and finally and fixing compilation warnings given by gcc5 in Linux
    UDFclient.0.8.1 : Fix spelling mistakes! Thanks Pali!
    UDFclient.0.8 : Fix metadata distribution issue to be calculated on the disc size rather than on a fixed length. Also fix 32 bit issues. It can now create discs bigger than one TerraByte!
    UDFclient.0.7.7 : Fix distribution error in 0.7.6 : some parts are not ready for release (yet). While here also fix a warning on a debug print format.
    UDFclient.0.7.6 : After some time being dormant, this new release fixes a small standing bug in newfs_udf regarding the volume set identifier name.
    UDFclient.0.7.5 : After some time being dormant, this new release fixes a lot of small standing bugs and a serious bugfix that prevented it to read Microsoft formatted UDF 2.50 and UDF 2.60 discs. Also, logical volume integrity checking is now fixed, directory handling has been made more robust and UDF 2.50 and UDF 2.60 are now correctly signaled as read-only and won't try to corrupt a disc anymore. cd_disect has been enhanced and extended to also support BluRay recorders.
    UDFclient.0.7.1 : Fix Linux compilation issues.
    UDFclient.0.7.0 : Enhance UDFclient with ideas and features from my NetBSD kernel implementation enhancing directory operations and fixing potential lockups on 512 bytes/sector media, repaired NetBSD harddisc support and fixed a few compilation warnings when compiled with '-Wextra' revealing some possible bugs. Enhanced cd_disect to display some more disc types. Also included some patches to fix possible buffer screwups; thanks Andrey!
    UDFclient.0.6.3 : Implemented byteswapping option to allow udfclient to read and write PVR harddiscs who appear to be byteswapped for some reason (copy protection?). Also improved udfdump dumping making it handle big free space maps and allocation extensions and making cd_disect ATAPI happy again.
    UDFclient.0.6.2 : lots of enhancements to cd_discect; now also reporting not only the TOC and the PMA, but also the ATIP. In this ATIP there is information on the CD-RW subtype wich is crucial to check if the disc can be written by the drive. Also fixing up yet another regression found on some DVD-R/CD-RW drives fixing newfs_udf and udfclient writing on those drives. Complete harddisc/flash support on Linux apeared to be broken and should be fixed now.
    UDFclient.0.6.1 : fix up yet another regression found on modern CD-RW drives when dealing with CD-MRW media. It would report them as sequential.
    UDFclient.0.6.0 : fix regressions found in newer DVD/CD combi drives that report bogus values for CD-RW media and fix 2G+ file write problems on some platforms. This fixes hese drives inability to newfs a CD-RW with newfs_udf and writing problems with udfclient on CD-RW media.
    UDFclient.0.5.8 : fixes a nasty locking assertion error, improves error handling on mounting multi-session discs and fix a small printing error in cd_discect for audio CD's.
    UDFclient.0.5.7 : fix for Microsoft Vista formatted media that has a perculiar partition numbering scheme that confused UDFclient. Also minor cosmetic changes to make it less dependent on gcc's C extensions.
    UDFclient.0.5.6 : important fixes in VAT searching on CD-R/DVD*R allowing more discs to be read. Also better dumping of TOC's in cd_discect and sequential dumping of files using a different sectorsize than the media allowing disc images of CD's to be dumped.
    UDFclient.0.5.5 : Support for reading UDF 2.50/2.60 media! This also adds support for all HDDVD and BluRay media! Also small but important fixes have been made on cd_disect for ATAPI drives; these could give up in the process.
    UDFclient.0.5.4.1 : Fix small but important bug that crept into the 0.5.4 releasing !
    UDFclient.0.5.4 : New in this release is support for harddisc partitions on NetBSD, OpenBSD and Linux. Have to figure out FreeBSD still. Tips welcome! Also new is support for USB sticks! As usual small bugs here and there are fixed.
    UDFclient.0.5.3 : recommended upgrade that fixes some nitty-gritty standards compliance issues and a better recordable/VAT search algorithm parameters.
    UDFclient.0.5.2 : recommended upgrade that fixes memory corruption bugs and obscure deadlocks making it a lot more robust. Functional identical to release 0.5.1.
    UDFclient.0.5.1 : recommended upgrade that also fixes a lot of small bugs. New in this release are the preservation of attribute times and ownership of files and directories and an important fix to filesize related issues making it more robust. Some important SCSI/ATAPI fixes have been made that greatly increase drive compatibility.
    UDFclient.0.5 : featuring a SCSI layer rewrite, CD-MRW and DVD+MRW support, new scsi/atapi format utility, more support for customer DVD (video) recorder DVDs and lots of bug fixes. Please do test this version and report strange behaviour 0.4.9 didn't show and report any problems!
    UDFclient.0.4.9 : recommended upgrade since it fixes lots of interchange issues and is now fully read & write compatible with Roxio's DirectCD/Drag2Disc! See the tips and trics for more details. It also adds the modified get and put functionality as well as the new mget and mput commands. In the run-up for 0.50's recordable support i've taken the opportunity to clean up loose ends and long standing small issues like the rm printing bug. Support has also been created for non 2048 bytes media such as harddiscs and files. Note: UDFclient will automatically set its sectorsize to the media used, so you have to use the new -b 2048 to be able to read and write files used for testing and mastering.
    UDFclient.0.4.5 : serious cleanup and bugfix release fixing serious `mkdir' brokenness and introducing a more decent logical volume open/close behaviour with coupled logical volume integrity sequence support that was lacking. Discs opened read-only are now really read-only; one could delete files from a read-only disc that could result in broken discs.
    UDFclient.0.4 : major upgrade to the 0.3 series due to a structural rebuild of main engine based on insights gained from developing version 0.3. Pitty enough still no recordable media write support (sorry folks...). Significant speed improvements have been made in both reading and writing heaps of little files. Offcource also heaps of bug fixes. Work has also started on an in-kernel implementation though i decided to get UDFclient fully functional first. New in this version is support for non 2048 byte media using the -b flag, new `rename' and `free' commands in udfclient and a fixed and hopefully full working `rm' command. Warning some flags have been changed meaning so check your scripts!
    UDFclient.0.3.5 : patch release fixing a serious memory leak.
    UDFclient.0.3.4 : small patch release; support for OpenBSD and some small bug fixes.
    UDFclient.0.3.3 : patch release fixing SCSI/ATAPI issue's, `rm' lockup and various small bugfixes. Recommended to use this one over version 0.3.2.
    UDFclient.0.3.2 : a patch release consisting of various bugfixes, a proper configure script to ease compiling on various systems, FreeBSD CAM support, cdrw_format tool and finally access rights preservation. Ownership of files is recorded but is not restored yet since i first want to check security hazzards induced by this.
    UDFclient.0.3 : expirimental writing support to files and CD-RW/DVD+RW !!. Reads CD-R/CD-RW/DVD+R/DVD+RW/(DVD-R?)/(DVD-RW?) UDF versions 1.02, 1.50, and 2.01. Accompanied is a udf-volume formatter `newfs_udf' that creates a filingsystem on a formatted media or file. NOTE: use `-W' flag to enable writing in `udfclient' itself and use `-d2' in `newfs_udf' to force a filingsystem compatible upto 1.50.
    UDFclient.0.2 : major sanitising release fixing various compatibility issues and important file reading fixes. Regretfully UDFv2.50 is temporary disabled but no discs are known to be formatted by this standard yet.
    UDFclient.0.1p2 : patch release fixing compilation errors on newer NetBSD-current systems and providing Linux users with mode sense information when SCSI errors occure.
    UDFclient-ro1-p1 : patch release fixing a compilation error on some 32 bit architectures.
    UDFclient-ro1 : first release featuring read-only access to ATAPI/SCSI discs and image files.

Bugs and problem reporting

No obvious problems or bugs are known; it can read corrupted discs but it might fail at times.

Update DirectCD/Drag2Disc will now read and write discs formatted with UDFclient fine! Older DirectCD/Drag2Disc versions might only accept media formatted with the -2 option.

Feedback is much apreciated also when its running fine!; please do mail me about any failure of disc reading with a small report to reinoud@netbsd.org consisting of the following points (replace "/dev/cdrom" by the device or file you used):

    UDFclient version
    The operating system UDFclient is running on

    uname -a

    Device report

    cd_disect /dev/cdrom

    and

    cd_sessions /dev/cdrom

    Logical dump of offending disc/file

    udfdump -D -u3 -t /dev/cdrom

Tips and tricks

Resqueing files and directories from unreadable, incomplete or broken recordables can be done by using the -r flag. By using the cd_sessions command you can see the number of CD/DVD sessions the disc has and specify wich session(s) you would like to give a try. These can be seen as older snapshots of the disc.

Roxio DirectCD/Drag2Disc interoperatibility. Newer DirectCD/Drag2Disc versions that support UDF version 2.00 and higher will happily read and write media created by UDFclient and vice versa. Older versions might only be able to read and write UDFclient discs created with the -2 flag that forces it to use older descriptors.

Important for DirectCD/Drag2Disc is to select in the advanced eject settings of DirectCD/Drag2Disc the option "use UDF version used on current disc". It will otherwise try to use a mechanism that is breaking certain UDF rules in order to try to be more compatible with older customer appliances.

TinyUDF interoperatibility. TinyUDF is known to be in certain appliances and its discs can be read in fine.
TODO
UDFClient TODO list after 0.5 release :

    if possible, write support for recordable media (CD-R, DVD+/-R).
    userID, groupID restoration; its recorded now but not restored back. (security issues?)
    not only looking for errors but also repairing them : fsck_udf
    write support for metadata partitions in UDF 2.50/2.60
    ...


