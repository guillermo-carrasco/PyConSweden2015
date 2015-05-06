## TACA - Preprocessing

First and foremost, data needs to go from the sequencer to a machine were the
preprcessing is done. This is done in local servers because of two reasons.

1. The preprocessing of the data is highly I/O intensive (converting the images
that the instrument's camera takes into A-C-T-G strings). This makes it non-doable
for mounted or shared filesystems like the ones our HPC is running.
2. We take care of the back up of the data locally, so having this data locally
for a while is a must.

The biggest problem that we have with this solution is storage. The amount of data
generated, specially after the acquisition of new instruments recently, is huge.
Thus we have to keep the data locally the shortest time possible, but ensuring that
it arrived to the analysis cluster and has been long-term archived before removing.

In the early times (this is about 3 years ago...) this whole process was done manually,
this is nowadays impossible.

_NOTE: A slide with a flowchart for TACA will go with this explanation_

**TACA - Tool for the Automated Cleanup and Analysis** is a tool completely written
in Python 2.7 that does precisely this. When a machine finished sequencing, TACA
starts automatically the preprocessing of that data in the local servers. To do so
a cronjob that runs every hour checks the status files that the machine generates,
this is tremendously easy to do in Python.

When the preprocessing of the data is done, the resulting data is sent to our HPC
(UPPMAX) for further analysis. After sending the data, an HTTP request is sent to the Tornado
server running in UPPMAX that triggers the `ngi_pipeline`.

As for the storage part, TACA periodically compresses and sends old data to our long
term storage facility without us having to worry about the servers getting full. This
has been enormous manual and tedious work liberation for us.

## NGI-Pipeline - Data analysis

On the HPC side, a very simple Tornado server is running in a special node. This server
is listening to the HTTP requests that TACA send to trigger the start of an analysis.

The reason to use a simple tornado server and not something more complicated/robust, i.e
RabbitMQ + Celery, is that the HPC has its own task scheduler, called SLURM, that
will allocate and distribute the jobs among computing nodes.

Icons in the slides (slightly modified):

 -- DNA: https://thenounproject.com/term/dna/77921/
 -- Snake: https://thenounproject.com/term/snake/24037/
 -- Test tube: https://thenounproject.com/term/test-tube/42653/
 -- Server: https://thenounproject.com/term/server/14182/
