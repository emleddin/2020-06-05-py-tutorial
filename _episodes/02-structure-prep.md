---
title: "Structure Preparation"
teaching: 0
exercises: 0
questions:
- "How do I add hydrogens to a PDB structure?"
- "How do you make a structure biologically relevant?"
objectives:
- "Take a PDB structure from download to ready for simulation."
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

First, we downloaded `5y2s.pdb` from [the RCSB]().

Clean the structure using `clean_pdb.sh`. This results in the `5Y2S_clean.pdb`
file.

Upload `5Y2S_clean.pdb` to [PROPKA](http://propka.org).
- pH 7.0
- Use PROPKA to assign protonation states at provided pH
- Forcefield: AMBER
- Choose output: AMBER
- Deselect Remove the waters from the output file

**FIGURE OUT PROPKA REINTEGRATION SCRIPT**
- Reintegrate PROPKA

Not to skip ahead in the tutorial (that's why these files are provided &#x1F603;),
but you can use MDAnalysis to reconvert the PDB from the PQR.

Go back and add in ZN and CO2 lines, because PQR couldn't handle them.
Change charge to 0, remove A segment, change HETATM to ATOM.
```
cp 5Y2S_ph7_protonated.pdb 5Y2S_ph7_nsa.pdb
```
{: .language-bash}

Upload the cleaned PDB file with the corrected pH AMBER types to
[MolProbity](http://molprobity.biochem.duke.edu/).

- Add hydrogens
- Asn/Gln/His flips
- Electron-cloud x-H

- Regenerate with flips, redownload

{% include links.md %}
