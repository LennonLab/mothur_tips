#Guideline to communinity sequence analysis
This document is intended as a general guideline for how to set up an analysis of your amplicon 16S rRNA gene sequences from an Illumina run using mothur on the high-speed clusters at IU. 

###1) Receiving your files from the sequencing facility
After submitting your barcoded samples to someone at the sequencing facility, you will get an email with a link to your sequences. You should access these and move them to the Scholarly Data Archive right away for safe, long-term keeping. However, this isn't a good place to store your data for analysis. You'll need to move the sequences to Mason. I don't have instructions or recollections on how to do this right now. 

###2) Moving files
After moving your sequences to a directory on Mason, you'll need then move your scripts and fasta files to the cluster as well. This includes:

*  **"files" file -** in each row of this file there is a sample name/file name, which often contains the barcode
*  **Batch file -** this contains all of the script to run the various functions in mothur
*  **Shell command file -** this file contins script that will specify limits of your job and load the mothur module, etc.
*  **DatabaseDownload.sh -** this file contains all of the reference databases and traingsets that you will need for classifying sequences, etc.

It's good practice to keeep you scripts on a github-linked folder on your local computer.  Then you can move the modified files over to Mason using **secure copy**. The first step is to open a terminal windown and change directory to the folder on your local computer containing the github-linked folder and desired files:

`> $ cd github/eDNA`

Then, as an example, you can move your files - in this case your Shell command file - to Mason with the following command:

`> $ scp eDNA.Bacteria.sh lennonj@mason.uits.iu.edu:/N/dc2/projects/Lennon_Sequences/2015_eDNA`

The secure copy command will ask you to supply your IU passcode for each file that you transfer. 

###3) Running mothur
Once all of your files are in the proper working directory (e.g., N/dc2/projects/Lennon_Sequences/2015_eDNA), you are ready to submit your job. This can be done using TORQUE (https://kb.iu.edu/d/bezu). For example, to submit a job, use the following code:

`> $ qsub eDNA.Bacteria.sh`

From this you will get output that looks something like this, containing your job number: 

`344753.m1.mason`

You can monitor the status of your job by typing the following:

`qstat 344753`

Or by the following:

`qstat -ulennonj`

If you want to kill a job, use the following command and your job number:

`qdel 344753`

Assuming that you included your email address in the shell file, you will get a message when your job starts and when it is (successfully or unsuccessfully) terminated. 

###4) Interpreting mothur ouput
As you can tell from the mothur batch file, there are a lot of steps and places where things can go wrong. It's advisable to go through your **logfiles** to make sure things look reaonsble. For example, you are going to lose sequence reads during the pipeline; that's to be expected. But you want to make sure that you're not losing *too* many. 

Perhaps the easiest way to retrieve your logfiles is as follows:

`> $ ls-l ./*.logfile`

You can than take a peak and scan through the rather long mothur output using the following commands (see [here](https://en.wikipedia.org/wiki/Less_%28Unix%29) for additional commands) :

* Space bar = next page
* b = previous page
* Shift + g = end of logfile
* q = quit






