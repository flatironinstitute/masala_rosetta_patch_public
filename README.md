# Masala patch for Rosetta 3.15.

## Description 
This public repository contains a patch for Rosetta permitting Rosetta to link Masala's Core library, and to make use of Masala plugin libraries loaded at runtime.

## Authors

Masala support for Rosetta was developed by Vikram K. Mulligan, a Research Scientist in the Center for Computational Biology, at the Flatiron Institute.  For questions, e-mail vmulligan@flatironinstitute.org.

In addition, the following individuals contributed to the development of the Masala patch for Rosetta:

- Noora Azadvari, a graduate student at the University of Oregon (eazadvar@uoregon.edu).
- Tristan Zaborniak, a graduate student at the University of Victoria (tristanz@uvic.ca).
- Qiyao Zhu, a Flatiron Research Fellow in the Center for Computational Biology, Flatiron Institute (qzhu@flatironinstitute.org).
- S.M. Bargeen A. Turzo, a Flatiron Research Fellow in the Center for Computational Biology, Flatiron Institute (bturzo@flatironinstitute.org).
- Parisa Hossienzadeh, a professor at the University of Oregon (parisah@uoregon.edu).
- P. Douglas Renfrew, a Research Scientist in the Center for Computational Biology, Flatiron Institute (pdrenfrew@flatironinstitute.org).

The Masala patch for Rosetta is maintained by the Biomolecular Design (BmD) Group in the Center for Computatonal Biology at the Flatiron Institute.  Vikram K. Mulligan and P. Douglas Renfrew co-head the BmD Group.

# Licence

The Masala patch for Rosetta is distributed under a BSD 3-clause licence.  Briefly, this licence permits use for commercial or noncommerical purposes, or redistribution as part of other software (including Rosetta), provided the licence is maintained.  Please refer to the LICENCE file for details.

Masala itself is released under an AGPL 3.0 licence.  This is a stronger copyleft licence that requires that any software project that includes Masala which is then redistributed inherit the AGPL 3.0 licence.  For this reason, users must obtain Masala separately from Rosetta and link Rosetta against Masala themselves.  Masala's Core library (against which Rosetta may be linked at compilation time with this patch) is available from <a href="https://github.com/flatironinstitute/masala_public">https://github.com/flatironinstitute/masala_public</a>, and the Standard Masala Plugins (which may be loaded at runtime once Rosetta has been linked against Masala's Core at compilation time) are available from <a href="https://github.com/flatironinstitute/masala_public_standard_plugins">https://github.com/flatironinstitute/masala_public_standard_plugins</a>.

# Use of this patch

To patch your copy of Rosetta:

1.  Obtain the correct version of Rosetta.  This patch has been tested against Rosetta 3.15, revision c389ea27189ed431c5f30718cf7d86843feeab8e.  However, it can likely be used to patch newer versions of Rosetta as well.  Note that Rosetta is not open-source software: its current licence allows non-commercial use for free, or commercial use for a fee.  Rosetta may be obtained from <a href="https://rosettacommons.org/software/">https://rosettacommons.org/software/</a>.
2.  Change to the Rosetta/main/ directory: `cd <path to Rosetta>/Rosetta/main`.
3.  Apply the patch: `patch -p1 < <path to patch>/masala.patch`.
4.  Obtain the correct version of the [Masala Core library](https://github.com/flatironinstitute/masala_public).  This patch has been tested against Masala Core version 1.0, revision 7ab1abb448a76193ba65cd1eb605c301ed8a794a.  However, it should work wth newer versions of Masala's Core library.
5.  Build Masala's Core library.  (Follow the instructions in Masala's README.md.)
6.  Recompile Rosetta with Masala support: `cd source && ./scons.py -j <number of parallel compilation processes> mode=release extras=masala bin`.
7.  Obtain whichever Masala plugin libraries (_e.g._ the [Standard Masala Plugins](https://github.com/flatironinstitute/masala_public_standard_plugins)) you wish to use with Rosetta, and build them.
8.  When running a Rosetta application, pass the path to the Masala plugin library or libraries that you wish to use using the `-masala_plugins` commandline flag.  Masala plugin libraries will be loaded on Rosetta initialization, and Masala plugin modules will be available for use from within Rosetta protocols.
