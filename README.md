# BBC Micro filing system tests

Code that exercises a number of the usual disk filing system entry
points and checks the results are... what's the right term here?
"Sensible", I suppose. I'm not promising more than that. There's not
even a right or wrong in every case, as the documentation isn't always
consistent.

The goal is to produce some tests that pass on every filing system
tested, partly as documentation, and partly as a mini test suite for
any future filing systems.

# how to run

To run, load `0/$.FSTEST` - a tokenized BBC BASIC file - on the BBC
Micro.

If the filing system is DFS-type, activate it, put blank disk in drive
0, and run the program.

If it's ADFS-type, mount blank disk, modify `ADFSDRIVE$` if the disk
isn't in drive 0, and run the program.

The test will stop with a `STOP` if anything surprising happens.

6502 second processor recommended - this won't speed up the disk
access, of course, but some of the checks are a bit slow in BASIC at
2MHz.

# filing systems tested

List of systems and any oddities encountered.

## DFS 2.24 (Master MOS 3.20)

* OSFILE A=0 returns 1 in accumulator whether the file was newly
  created or not

## ADFS 1.50 (Master MOS 3.20)

* OSFILE A=5 modifies LSB of parameter block attributes only
* OSFILE A=2/3/4 can modify the current directory if directed to
  change attributes of files in another directory - suspect this is an
  ADFS bug - haven't looked into this in any detail yet
* OSGBPB directory name retrieval returns a name padded with spaces

## BeebLink

* OSFILE A=0 returns 1 in accumulator whether the file was newly
  created or not (this is arguably incorrect, but it's trying to copy
  DFS...)
