# xbedump
Modifications and bugfixes of xbedump for the XQEMU project.

Upstream: http://xbox.cvs.sourceforge.net/viewvc/xbox-linux/xbedump/

#Original Readme:

```
XBE Dumper 0.4
---------------

by franz@caos.at, based on the original XBE
   Dumper by Michael Steil (mist@c64.org)


The XBE dumper is now in the process of being enhanced to perform
the same crypto operations on the XBE file as the Xbox kernel itself,
using the same algorithms.

The XBE signing process is in two stages.  In Stage one, a SHA-1 hash of
the contents of each XBE section is made and the hash stored in a table
in the XBE header section.  In stage 2, a single SHA-1 hash is made of
the header region (including the section hashes and a signer certificate),
the resulting single hash is then itself encrypted with strong 2048-bit
RSA public/private key encryption and the resulting encrypted single hash
''signature'' stored near the start of the final, signed XBE file.

In this release, the action of the first& second stage is implemented, so that
the software is able to compute and store in the header SHA-1 hashes
for each section in the unsigned XBE.  It is also able to confirm that
the hashes stored in the header are correct for the corresponding section
contents.  Work has started to implement Stage two, although this will be
quite hard to fully complete without having the private key :-)

However, the intention is to at least be able to have a functional model
of the xbox validation actions, so that the correctness of any attempt to
create a signed XBE can be reliably and rapidly assessed without using
any Microsoft code.  In the other direction, it is intended to have proven
all of the code needed to sign XBEs given a valid signer certificate and
the correct private key (which we of course lack at the moment).

Additionally, this Software gives us the oportunity to make "cleaner" xbe's
as the patching of Kernel (done by mod_chips) is reduced, and only the real
Verify signature has to be "adapted".

There are 2 additional key's in the source, these are key's build with my computer.
The keys are test keys and do not work on "real" xboxes.
We have agreed not to publish the MS$ public key in the CVS, as this would be a copyright
problem. You have to copy a decryped and decompressed flash to the same directory, 
the programm is working in.

Please refeer to the Help in the programm itself for operations.


Installation
------------

The app relies on the OpenSSL libraries from
http://www.openssl.org/source

Here are the steps for installation:

 1) download and unpack the openssl sources somewhere
 2) enter the openssl-0.9.6g (<-- or whatever) directory
 3) ./config
 4) make
 5) make test (should end with some version info, no explicit OK)
 6) su (<-- make yourself root)
 7) make install  (<--- installs SSL stuff into /usr/local/ssl)
 8) exit (<-- make yourself normal user again)
 9) cd to where xbe dumper sources are
10) make (<--- should be no errors or warnings)

One note, it was found that there are bogus link errors with the
GCC 3.2 version shipped with Redhat 8.0 beta, if you experience
these bogus "undefined reference to `__gxx_personality_v0'"
errors uncomment the definition of this symbol in xbe.c and
remake.



Changelog
---------

0.2b Franz has added code to verify the signature
0.2a Franz started on adding crypto structure code
0.3a Mismatch of Andy and Franz checking, now learned to work with CVS
0.3b Checking the RSA signature + update sections hashes
0.3c Generation of a "custom signature" implemented

(this document by andy@warmcat.com & franz@caos.at)
```
