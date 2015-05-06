## TACA - Preprocessing

First and foremost, data needs to move from the sequencer to a machine where the
preprocessing is done. This is done on local servers for two reasons:

1. The preprocessing of the data is highly I/O intensive (converting the images
that the instrument's camera takes into an A-C-T-G string). This task is infeasible
on mounted or shared filesystems like the ones our HPC is running.
2. We take care of the back up of the data locally, so having this data available
locally for a while is a must.

_NOTE: A slide with a flowchart for TACA will go with this explanation_

**TACA - Tool for the Automated Cleanup and Analysis** is a tool completely written
in Python 2.7 that does precisely this. When a machine has finished sequencing, TACA
automatically starts the preprocessing of that data on the local servers. To do so,
a cronjob that runs every minute checks the status files that the machine generates;
this is tremendously easy to do in Python.

When the preprocessing of the data is done, the resulting data is sent to our HPC
(UPPMAX) for further analysis. After sending the data, an HTTP request is sent to the Tornado
server running in UPPMAX that triggers the `ngi_pipeline`.

## NGI-Pipeline - Data analysis
