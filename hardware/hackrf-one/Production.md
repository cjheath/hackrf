## Making files for production of HackRF One

### Check everything

In eeschema, run Inspect->Electrical Rules Checker

### BOM

In eeschema (schematic editor), select "Tools->Generate Bill of Materials".
Click Export. This creates the file doc/hardware/hackrf-one-gerbers/hackrf-one-bom.csv

### Assembly silk with references

In pcbnew (the PCB editor) select File->Plot....
* Ensure F.SilkS (front silk) layer is selected.
* Select "Use drill/place file origin".
* Deselect "Use Protel filename extensions".
* De-select "Generate Gerber job file".
* Select "Plot reference designators"
* Click "Plot". This puts files into doc/hardware/hackrf-one-gerbers.
* Rename doc/hardware/hackrf-one-gerbers/hackrf-one-F_Silkscreen.gto to doc/hardware/hackrf-one-gerbers/hackrf-one-Placement.gbr

### Gerber files

In pcbnew (the PCB editor) select "Plot...".
* Ensure all required layers are selected: C1F, C2, C3, C4B, F.Paste, F.SilkS, F.Mask, B.Mask, Edge.Cuts
* De-select "Plot references designators"
* Click "Plot".

This puts files into doc/hardware/hackrf-one-gerbers. Change to that directory.

### Drill file

From pcbnew->Plot, select "Generate Drill Files".
* Select "Excellon".
* Tick "Minimal header"
* Tick "PTH and NPTH in single file"
* Select Drill Origin "Drill/place file origin"
* Select Drill Units "Inches"
* Select Zeros Format "Suppress trailing zeros"
* Click "Generate Drill File"

This creates the file "doc/hardware/hackrf-one-gerbers/hackrf-one.drl"

* Click "Generate Map File"
* Click "Generate Report File" and Save

### Placement file

In pcbnew, select File->Fabrication Outputs->Component Placement (.pos) File
Select CSV, Inches, Single file per board.
Click "Generate Position File"
This makes the file doc/hardware/hackrf-one-gerbers/hackrf-one-all-pos.csv

Check the rotation of U3, the low-pass filter. Its footprint is 180 from how they come off the reel.

### Zip it up

cd into doc/hardware/hackrf-one-gerbers
zip -j ../hackrf-one-fabrication-draft-YYYY-NN-DD.zip ../README.production *
