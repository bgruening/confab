Usage
=====

Two command-line applications are included in the Confab distribution: :command:`confab` for generation of conformers, and :command:`calcrmsd` for calculating RMSDs to reference structures.

confab
------

``confab``
  Display help text

``confab [options] <inputfile> <outputfile>``
  Generate conformers

The *inputfile* should contain one or more 3D structures (note that 2D structures will generate erroneous results). Generated conformers are written to the *outputfile*. All of the conformers for a particular molecule will have the same title as the original molecule.

Supported file formats are SDF (recommended), MOL2 and PDB.

-i <format>
    Input file format

    If unspecified, the file format is determined by the *inputfile* extension.

-o <format>
    Output file format

    If unspecified, the file format is determined by the *outputfile* extension.

-r <rmsd>
    RMSD cutoff (default 0.5 Angstrom)
-e <energy>
    Energy cutoff (default 50.0 kcal/mol)
-c <#confs>
    Max number of conformers to test (default is 1 million)
-a
    Include the input conformation as the first conformer
-v
    Verbose - display information on torsions found


calcrmsd
--------

``calcrmsd``
  Display help text

``calcrmsd [options] <reference> <testfile>``
  Calculate RMSD of structures in *testfile* to the *reference* structures

Once a file containing conformers has been generated by :command:`confab`, the result can be compared to the original input structures or a set of reference structures using :command:`calcrmsd`. Conformers are matched with reference structures using the molecule title. For every conformer, there should be a reference structure (but not necessarily *vice versa*).
  
-a <format>
    Reference file format

    If unspecified, the file format is determined by the *reference* extension.

-b <format>
    Test file format

    If unspecified, the file format is determined by the *testfile* extension.

-r <rmsd>
    RMSD cutoff (default 0.5 Angstrom)

    :command:`calcrmsd` reports the number of structures with conformers
    within this RMSD cutoff of the reference.
