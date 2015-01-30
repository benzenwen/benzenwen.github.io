---
layout: post
title:  "File Vault 2 Master Key"
date:   2015-01-28
categories: howto sysadmin
tags: crypto security mac apple osx
---

Part of my duties as the extended family IT guy is that I deal with
failed hard drives.  I'm one to squeeze out the maximum life from
computer hardware, so I install new hard drives, updrade to SSD's, add
more RAM, etc. Once I had to return a failing Mac OS X SSD drive that
was under warranty.  It was encrypted, so I was compelled to do a
little research on the File Vault 2 system.  The drive was too flaky
to write to for a full wipe, nevermind that wipes are challenging for
SSDs.  No one in the family is an international spy (as far as I know)
so we don't have state secrets to protect, but I try and take security
seriously without being alarmist.

Secure SSD wipes are challenging because of the way that their
controllers move data around to compensate for SSD storage cell
mechanics. See this Usenix 2011 paper by
Wei, Grupp, Spada, and Swanson:
[Reliably Erasing Data From Flash-Based Solid State Drives](https://www.usenix.org/legacy/events/fast11/tech/full_papers/Wei.pdf).
It's from the UCSD Non-Volatile Systems Lab's (NVSL)
[Sanitize project](http://nvsl.ucsd.edu/index.php?path=projects/sanitize).
For SSD's, full volume encryption is attractive as destroying the
master encryption key or losing the passphrase renders the data on the
disk effectively unreadable.

As for File Vault 2, I found this detailed paper reverse engineering
the system by Choudary, Grobert, and Metz:
[Infiltrate the Vault: Security Analysis and Decryption of Lion Full Disk Encryption](http://eprint.iacr.org/2012/374.pdf).

Summarizing, the File Vault 2 full volume master key is
stored on the Recovery HD partition, encrypted with AES-XTS.  So
destroying those bits would make it very hard to recover the data on a
File Vault 2 drive, also known as a
[FVDE drive](https://github.com/libyal/libfvde).  That's useful to
know when wanting to wipe a FileVault2 encrypted disk.

The key file is EncryptedRoot.plist.wipekey found in `com.apple.boot.X
/System/Library/Caches/com.apple.corestorage/` (where `X` can change
among literals R, S and P).  The final volume key can be derived from
data in that .plist file with either the user-provided passphrase or the
recovery key.  Interestingly, the EncryptedRoot.plist.wipekey is
encrypted itself with an AES-XTS-128 key found right on the volume.*
Destroying the CoreStorage Volume header that holds the key to
unencrypt the .wipekey file would also effectively destroy the final
volume key material. 

Securely deleting a single file on an SSD presents challenges as well,
as described by the NVSL paper.  For my pedestrian purposes what I did
was enough to satisfy me. Besides, the drive's performance degraded so
much that I couldn't confirm erasure the file.  Of course I didn't
give out the passphrase nor the recovery key to the drive vendor.
Still, deleting that file adds an extra step of circumventing the SSD
controller that an attacker would need to surmount.

So to render a File Vault 2 encrypted disk challenging to recover:

* destroy and "forget" the passphrase
* destroy any recording of the recovery key

To the extent possible:

* securely delete EncryptedRoot.plist.wipekey. See above for location.
* or destroy the CoreStorage Volume header. (More on this later.)

Final note: What happens on a hybrid SSD + HDD Fusion drive isn't
considered.

*I originally agreed with the authors of the Infiltrate paper that
 this encryption was gratuitous (Section 4.5) because the key was
 stored in the clear. But the name given to the file: "wipekey" is a
 hint; it provides for a Core Storage-level mechanism to wipe the
 disk.  However, it does introduce an vulnerability in that the key
 can be copied by an attacker, making this type of "wipe" potentially
 reversible.  Note that the passphrase or recovery key is still needed
 to get to the final volume key.

Much thanks to the authors of those articles.

_UPDATE:_ Added note about copying unencrypted CoreStorage Volume
header. Grammar, readability, etc.
