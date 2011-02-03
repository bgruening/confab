Example
=======

The example file, `bostrom.sdf`_, contains 36 molecules which have from 1 to 11 rotatable bonds (see *Bostrom, Greenwood, Gottfries, J Mol Graph Model, 2003, 21, 449*).

We can generate and test up to 100K conformers using :command:`confab` as follows (takes about 4 minutes)::

  > confab bostrom.sdf confs.sdf -c 100000

  **Starting Confab 1.0
  ..Input file = bostrom.sdf
  ..Output file = confs.sdf
  ..Input format = sdf
  ..Output format = sdf
  ..RMSD cutoff = 0.5
  ..Energy cutoff = 50
  ..Conformer cutoff = 100000

  **Molecule 1
  ..title = 1a28_STR_1_A_1__C__
  ..number of rotatable bonds = 1
  ..tot conformations = 12
  ..tot confs tested = 12
  ..below energy threshold = 10
  ..(tree size = 7 confs = 3)
  ..molecule has no automorphisms
  ..(new tree size = 7 confs = 3)
  ..generated 4 conformers
    
  ..etc, etc., etc

  **Molecule 36
  ..title = 1ppc_NAS-GLY-APH-PIP
  ..number of rotatable bonds = 11
  ..tot conformations = 53747712
  ..tot confs tested = 100000
  ..below energy threshold = 3606
  ..(tree size = 1944 confs = 1325)
  ..molecule has 8 automorphisms
  ..(new tree size = 5236 confs = 829)
  ..generated 830 conformers


  **Finishing Confab

To check how many of the generated conformers are within 1.0 A RMSD of the original structures, we can use :command:`calcrmsd` as follows::

  > calcrmsd bostrom.sdf conf.sdf -r 1.0

  **Starting calcrmsd
  ..Reference file = bostrom.sdf
  ..Test file = confs.sdf

  ..Molecule 1
  ..title = 1a28_STR_1_A_1__C__
  ..molecule has no automorphisms
  ..number of confs = 4
  ..minimum rmsd = 0.0644801
  ..confs less than cutoffs: 0.2 0.5 1 1.5 2 3 4 100
  ..1 2 4 4 4 4 4 4
  ..cutoff (1) passed =  Yes

  ..etc, etc., etc

  ..Molecule 36
  ..title = 1ppc_NAS-GLY-APH-PIP
  ..molecule has 8 automorphisms
  ..number of confs = 830
  ..minimum rmsd = 1.12063
  ..confs less than cutoffs: 0.2 0.5 1 1.5 2 3 4 100
  ..0 0 0 12 78 395 770 830
  ..cutoff (1) passed =  No


  **Summary
  ..number of molecules = 36
  ..less than cutoff(1) = 33

  **Finishing calcrmsd

.. _bostrom.sdf: http://www.google.com
