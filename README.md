Fork of Inno2John by Daniel Marschall
-------------------------------------

This fork is based on https://github.com/PancakeSparkle/inno2john with the following changes:
- Added structures for InnoSetup 5507 till InnoSetup 6201u
- Added `use lib '.';` to inno2john.pl and makestruct.pl
- Removed line `printf("%u: %s %s %u %s %s%s...", $i, $file->{Name}, $file->{Type}, $file->{Size}, $file->{Da ....` from inno2john.pl, because there were errors on some EXE files (date not found).
- Extended this readme file


Installation notes:
-------------------

Tested on Debian:

```
sudo aptitude install libswitch-perl libdatetime-perl libtext-glob-perl libdata-hexdumper-perl libdata-printer-perl -y
sudo aptitude install liblzma-dev
cpan Compress::Raw::Lzma 
cpan IO::Scalar
cpan Digest::CRC
```

On Fedora (untested):

```
sudo dnf install perl-Data-Printer perl-Switch perl-DateTime perl-Compress-Raw-Lzma perl-Digest-CRC
```

How to extract files and hash from a setup
------------------------------------------

```
rm -rf app
./inno2john.pl /daten/test/XXX.exe
```

On the screen, you will see the hash, which you can put into john.
The "app" directory contains the extracted setup files.


How to create structure files for newer setup versions
------------------------------------------------------

Install once:

```
cpan Marpa::R2
```

Example for InnoSetup 6.2.1:

```
git clone --depth 1 --branch "is-6_2_1" https://github.com/jrsoftware/issrc.git
nano issrc/Projects/Struct.pas    # Remove comment "Must be same as Graphics.TAlphaFormat", otherwise "Marpa" will fail...
./makestruct.pl  --src issrc/ --version 6.2.1
./makestruct.pl  --src issrc/ --version 6.2.1u
mv Struct* Setup/Inno/
rm -rf issrc/
```

And please make a Pull request to share the structure file with other people! Thank you very much.

