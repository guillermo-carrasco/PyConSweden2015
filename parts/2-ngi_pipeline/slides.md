## TACA - Preprocessing

First and foremost, data needs to move from the sequencer to a machine where the
preprocessing is done. This is done on local servers for two reasons:

1. The preprocessing of the data is highly I/O intensive (converting the images
that the instrument's camera takes into an A-C-T-G string). This task is infeasible
on mounted or shared filesystems like the ones our HPC is running.
2. We take care of the back up of the data locally, so having this data available
locally for a while is a must.

The biggest problem that we have with this solution is storage. The amount of data
generated, specially after the acquisition of new instruments recently, is huge.
Thus we have to keep the data locally the shortest time possible, but ensuring that
it arrived to the analysis cluster and has been long-term archived before removing.

In the early times (this is about 3 years ago...) this whole process was done manually,
this is nowadays impossible.

_NOTE: A slide with a flowchart for TACA will go with this explanation_

**TACA - Tool for the Automated Cleanup and Analysis** is a tool completely written
in Python 2.7 that does precisely this. When a machine has finished sequencing, TACA
automatically starts the preprocessing of that data on the local servers. To do so,
a cronjob that runs every minute checks the status files that the machine generates;
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

In the HPPT request received in the server, the id of the dataset to be analyzed is
passed as a parameter. TACA has already transferred the dataset so as soon as the
request is processed, the analysis can start.

A common problem in genomics bioinformatics, is that every lab/research center ends
up implementing their own pipeline... and so we did! But _at least_ we **tried** to do
it in a way that can be reused in other labs or HPCs.

The architecture of the whole thing is designed in such a was that:

* we can integrate in our pipeline different "engines". An engine is the piece of
software that runs the actual analysis of the data. The engine is selected according
to a YAML configuration file and using a combination of try..except strategy and
python importlib module. _show some code here?_
* Independently of the engine used, `ngi_pipeline` keeps track of the status of all
the analysis steps using a local database (SQLite), that is then used to populate a
global database. The reason for this logic is that worker nodes in our HPC can't have access
to that global database, so we update this local database in a shared filesystem
that can be accessed by the single login node that has access to the global database.
_show here Mario's flowchart? maybe simplifyed_.

`ngi_pipeline` also sends email notifications to the researchers indicating that the
analysis are done, or else that they failed. In any case, human intervention is
needed _only_ to check the final results, but all the repetitive and tedious tasks
of formatting data and directories, running analysis and gathering results is done
automatically.

Icons in the slides (slightly modified):

 -- DNA: https://thenounproject.com/term/dna/77921/
 -- Snake: https://thenounproject.com/term/snake/24037/
 -- Test tube: https://thenounproject.com/term/test-tube/42653/
 -- Server: https://thenounproject.com/term/server/14182/
