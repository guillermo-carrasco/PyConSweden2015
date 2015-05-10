# Outline, slides

## Clinical Genomics
So my name is Robin and I work at a sister facility to NGI at SciLifeLab where we
provide DNA sequencing services to hospitals across Sweden.

We do mostly similar automation and data analysis as we've talked about before.
However, one of the things that makes working at our facility unique is that our end
users tend to be only somewhat-computer-literate doctors. This means that we need to
find a way to process the data as far as possible before we intuitively visualize it.

We have a long term vision that after doctors recieve their "test results" from
DNA sequencing it shouldn't take them more than 5 minutes to reach a clincal decision.


## Genomics in healthcare today
The kinds of disoders we are talking about here are rare and inherited from parent to
child. The cause is, for the sake of this presentation 100% genetic and often develop
early in life of the patients and cause severe symptoms.

Right now the process is quite bleak. Patients meet with a doctor, run some tests,
are sent home, some more tests are run, the see another doctor, home again... This
can go on for 15 years without definitive answers.

However using sequencing you have the possibility of finding out the root cause
within 2 weeks. This can have tremendous beneficial effects for the patient, family,
and healthcare system.


## Excel sheet -> Web interface
In the beginning there was ... Excel. This is pretty close to the raw output of the
data analysis. 6000 rows of variants along with a lot of annotations. From the
perspective of some people this is rather intuitive and offers a familiar setup for
the doctors.

However, I think this shows the benefit of working with people from very different
backgrounds. When I looked at this with some web developmend in my past I felt
imidietly that we could do so much better!


## The Scout interface
So through a few major iterations we built a web interface that has become the de
facto delivery report that doctors look at after they've sent in samples for sequencing.

### Tech stack
We're using a MongoDB database, I'll get back to this later, with a Flask server.
Basically because this is what I was familiar with. We also make extensive use of
other thrid party libraries such as Jinja2 for HTML templates and MongoEngine as an
API for our database.

We have to remember that we are dealing with sensitive clinical data. We are by no
means security experts but what we do, do is to restrict access based on IP adresses,
enforce two-step authentication on all user accounts, and encrypt data using SLL.

### The interface
Just to give you and idea what I'm talking about I'll show you the actual interface.
This is where your doctor would login to review the results of one of the clinical
tests.

This view is where you would find the full list of all the variants, or possiblity
disease causing alterations to the patients DNA. You can filter variants here and also
click on one individual variant to reveal _all_ the annotations for it. We try to
present the information so that as you scroll down you get into more detailed
information that is only relevant if the variant is deemed interesting.

Now let's get into some more technical aspects...


## JavaScript vs. Python code
An early version of the interface was built heavily around Ember.js. Why? I wanted to
learn more about Ember.js and no one told me it would be a bad idea ;)

Basically I found out that big tables of non-updating data will give you sluggish
performance without many benefits. So we rewrote most of the application with the idea
in mind that this was a professional, clinical grade tool. If it gets the job done
it isn't going to matter at all whether the page reloads or not.

The upsides are many: it has made it easier for us to collaborate because we stick
to what everyone already is familiar with, Python, it's improved performance, and
iteration and testing is *much* simpler.

Basically we've learned the lesson that when it's possible to do something in Python
- do it in Python!


## MongoDB + MongoEngine
There are a few undeniable upsides such as the much simplified and more intuitive data model with e.g. nested comments.

Most importantly: if a doctors shows up and wants to take a look at a result from way
back we need to be able to show her the exactly what the previous clinical
interpretation was based on. We solve this problem by limiting Scout to a visualization
tool. It's not Wikipedia.

We also need to denormalize data to avoid information spilling over between patient
data. For example comments. This makes MongoDB an attractive choice as well!

I also really like the ability to create computed properties that behave as regular
fields. This has really helped a lot to maintain readability as we pass aruond these
objects in the templates.


## Concluding remarks
I have two take-away messages to share. The first is how important it's been for us
to be able to come together under a single language to do just about everthing we
need to run a sequencing platform. Python allows us to do that unlike any other
language.

The second message is what a huge potential we have in science/academia of being
leveraging open source development. Bioinformatics has a hig and lively open source
community that are doing some amazing things.

Internally we have decided to promote our inhouse developed open source projects
through a web portal that you can all visit if you like at opensource.scilifelab.se.
