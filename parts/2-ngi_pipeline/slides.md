## TACA - Preprocessing

First and foremost, data needs to go from the sequencer to a machine were the
preprcessing is done. This is done in local servers because of two reasons.

1. The preprocessing of the data is highly I/O intensive (converting the images
that the instrument's camera takes into A-C-T-G string). This makes is non-doable
of mounted or shared filesystems like the ones our HPC is running.
2. We take care of the back up of the data locally, so having this data locally
for a while is a must.

_NOTE: A slide with a flowchart for TACA will go with this explanation_

**TACA - Tool for the Automated Cleanup and Analysis** is a tool completely written
in Python 2.7 that does precisely this. When a machine finished sequencing, TACA
starts automatically the preprocessing of that data in the local servers. To do so
a cronjob that runs every minute check the status files that the machine generates,
this is tremendously easy to do in Python.

When the preprocessing of the data is done, the resulting data is sent to our HPC
(UPPMAX) for further analysis. After sending the data, an HTTP request is sent to the Tornado
server running in UPPMAX that triggers the `ngi_pipeline`.

## NGI-Pipeline - Data analysis
