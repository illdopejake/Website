
Many Steps to Reconstructing FDG em using a good tx
===================================================


On Sun computer running ECAT software
+++++++++++++++++++++++++++++++++++++

1. Download data onto Sun
~~~~~~~~~~~~~~~~~~~~~~~~~
  a. sftp usernamecfi
  b. cd into appropriate directory (/home/raid/cfi/users/awesomeperson/PET... awesomeperson being either slbaker, jkluth, or ivyen)
  c. get fname

  need:
	+ norm *.N file
	+ both *tx.S files
	+ blank *bl.S file
	+ FDG emission file de.S that is 138MB)

**DO NOT GET THE PIB EMISSION FILE - this will take a while, clog up the Sun hard drive, and we don't need it for this problem**


2. Load these files into Database Utilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  a. Tools - Database Utilities
  b. Action - Add ... type in Subj ID under last name and Subj ID
  c. Double click on Subject of interest
  d. Action - Add ... name folder something like Raw FDG data
  e. Double click on Raw FDG data
  f. Action - Add, type in description, filename (starting with
/home/data/), change isotope to Ge68-Ge68 Solid for Tx and Bl, and
F18-FDG for dynamic emission. To close window, first click File
button, then OK button. In description, differentiate between PIB and
FDG tx (FDG tx is take 2nd if the two scans were done on the same
day... if not done on the same day, look up to see if PIB or FDG was
done first). Add the norm, blank, 2 transmission scans, and fdg
emission scan to the database.


3. Reconstruct emission and 2 transmission files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**PIB tx**

  a. Tools - Quick Acquisition
  b. File - Load Patient - choose appropriate patient
  c. File - Open, Open *Step1 Tx Recon
  d. Hit play button
  e. Choose blank, then Pib Tx.
  f. Go into Database Utilities and change Desciption of v-2D Meas.Atten
     file so that "PIB" is in there somewhere.


**FDG tx**

  g. Repeat a-d ... or just hit "backup" button until over Tx and then
     hit play
  h. choose blank then FDG tx (or just FDG tx if starting recon over the
     TX box)
  i. be sure NOT to overwrite any files
  j. Change description in Database Utilities so "FDG" appears
     somewhere.

**FDG em**

  k. In Quick Acquisition, open *3d Retro Recon (n/em)
  l. Hit "start" button, choose fdg em, and norm.


4. Move files
~~~~~~~~~~~~~
  m. Once done, move de.v and 2 tx.v files (in your favorite way) onto
     the raid on campus... make sure you know which is Pib tx
     and which is FDG tx.


On Campus RAID
++++++++++++++


1. In matlab, make sure spm2 is in your path (under File - SetPath
   , that spm2 is higher than spm5 in the paths, and that
   /home/jagust/slbaker/Code/PET is in your path. You can add this path
   through the ui, or by typing::

   	addpath /home/jagust/slbaker/Code/PET/



2. Find appropriate files (2 tx.v and em.v)::

   	fdgtx=spm_get; pibtx=spm_get; fdgem=spm_get;




3. Run the following function::

       	GoodTxBadTxSwitch(pibtx, fdgtx, fdgem)




4. The function will run a realignment on the FDG emission data and
   print out the overall translation and rotation at the Matlab command
   prompt... if the numbers are high, make note of it.


5. It will then create a plot of the FDG tx over the FDG em (frame1)
   and ask if these two line up. If they do, type y and hit return, if
   they don't, see Suzanne.


6. It will align the PIB tx to the FDG tx and fill in any holes due to
   the rotation/translation of the PIB tx (with FDG tx data). Check to
   make sure they overlap in the figure titled "New FDG tx (aka moved PIB
   tx) over FDG em." If all looks good, respond y and hit return in the
   matlab command window.


7. New FDGtx file will be written out in ecat format. Transfer to the
   cfi raid, and download onto ECAT Sun.


On LBL PET-Sun computer
+++++++++++++++++++++++


1. Transfer new PIB tx.v file onto PET-Sun computer, and add to
   database utilities.


2. Open Tools - Quick Acquisition. Load in appropriate subject.


3. File - Open: *Vol2Atten + Recon (em,n,att) hit play


4. Load emission, load norm, load newpibtx.v file.


5. Once file is done reconstructing (it will take ~2 hours), transfer
   to somewhere on cfi raid and notify person who may be waiting for it.


