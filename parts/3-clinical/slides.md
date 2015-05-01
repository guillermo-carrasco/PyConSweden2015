# Outline, slides


## Clinical Genomics
Core facility at SciLifeLab

### How are we different from NGI?
Bridge the gap between sending raw data to computer savvy researchers vs.
only somewhat computer litterate genetecists and doctors. Basically it
means processing the data as far as possible and intuitively visualize it.
The massive amounts of data can't simple be summed up in a pretty little graph
anymore.

### Mission
5 min analysis


## Genomics in healthcare today
In fact, clinics already routinely send in patient samples for sequencing.
This is pretty cool because healthcare is *not* famous for moving fast or
adopting new technology. Now cutting edge research is using the same tools as in
the clinic.

The focus area for us is diagnosis of rare inherited disoders. They are
an ideal case to bring genomics into the clinic. The symptoms are often
severe and develop early in life, the cause is 100% genetic, and the
cause-effect relationship is therefore rather simple. Basically, you
find a defect gene and there's your cause. But figuring out what gene you
are looking for isn't quite so easy.

If we step back a bit; these patients can go undiagnosed for 15 years,
if they survive that long. Each individual test can only ever give
indications of what the cause of the disorder really is.

In contrast, using DNA sequencing technologies, we are able to go straight
for the root cause of the disorder and deliver conclusive results in *two
weeks*.

So why are people still hesitant?

1. The high initial cost. One challenge is to prove that sequencing can
   effetively replace many of the old inconclusive tests.

2. Analysis of data is neither trivial nor standardized. For example how
   do you distingish an error from a mutation? Essentially 99.9% of the
   data generated is either too difficult to interpret or completely
   non-informative. Most sequences are just the same as what we know we
   find healthy individuals. To be honest we are generating a lot of
   "waste" that no ones has figured out a plan to do with. Kind of like
   a nuclear power plant.

As the patient sample travels through our facility thousands of lines of
Python code will eventually touch it. I'm going to focus on the delivery
report.


## Excel sheet -> Web interface
What these guys [point to Guillermo] are delivering to researchers is very
basic text files usually. Low level data that needs a lot of processing to
start making sense. We have the ambition to take things a lot further.
Basically we want to eliminate the need for any further non-manual
processing after we deliver our results.

We also don't focus much on providing extensive tools to filter out the
interesting data but more on prioritizing what they should look into first.
This is meant to be part of routine work and not exploratory research so
it makes sense.

In the beginning there was ... Excel. At least it's something familiar to
most people. Soon enough it got out of hand. It was very inflexible to
work with. Thousands of rows in an unwieldy, and inherently static grid.
It also took too much time to look into each case to be practical.

[introduce Scout interface]


## Scale: JavaScript vs. Python code, swinging over
In the beginning there was ... lots of JavaScript. But our input isn't
optimized for this kind of setup: we have mostly non-updating data and
big tables which gives for sluggish client side performance.

Kind of the oposite of where most of the web seems to be heading but this
is a professional, clinical grade tool and we don't need to concern
ourselves with user appeal too much. But it's always fun to make something
pretty.

The upsides are many: easier for us to collaborate because we stick to
what everyone already is familiar with (Python), more performant on our
data, iteration and testing *much* simpler, and doing it in Python >>
JavaScript.

### Jinja/Flask best practises
One thing I've started using but for some reason keep forgetting about
is macros in Jinja templates. Perhaps it's worth lifting them up. They
should be as useful as functions in regular Python code!

### When you have to render client side code
My suggestion is to leverage components (Vue.js and SCSS). This way you
can avoid messing too much with jQuery and the end result can be very
nicely declerative using web components syntax. To avoid the clash in
template language syntax there's you can add a custom Jinja filter to
escape ``{{}}``.


## Copy conventions from GitHub
I've always admired the GitHub website. They manage to present a lot of
information in a consistent and intuitive way. I've used it many times to
look for inspiration on how to solve problems. One of the cool things is
how the seems to strike a very nice balance between mostly server side
rendered templates and a sprinkle of client side magic.

- Follow the same huminized URL conventions. The URL should say something
  to the user if possible, not just be some random hash ID from a
  database.

- Just to give you an insight in my process I could explain how they
  handle a simple logout form. Under the button hides a sign out form
  that gets submitted.


## MongoDB + MongoEngine
We find it useful to not worry too much about data duplication and the
rest of the "schema" just make things more intuitive to think about.

MongoEngine as an interface to MongoDB
PyMongo for indexes, weird syntax in ODM (don't know much about this though...)

We can often repopulate the data from the file system if thing go wrong. Integrity of
the database isn't super duper important.

Being non-database experts the data model is a lot more intuitive! Nesting comments etc.

IMPORTANT: we need to keep track of what we've uploaded and be able to repopulate the
same information on request for old samples. You upload data once per sample and make
the clinical interpretation based on that. It can never change! We also can't share data
as much as you might want to think. Each sample needs to be pretty isolated form the
rest and especially between different institutes. So we can't make use of aggresive
normalization even if we wanted. This makes Mongo attractive as well!

- Bring up simplified example for comments
  - This is different than most regular setups because we need to
    separates comments between institutes and cases...
  - Much more intuitive in MongoDB

- clinical/sensitive nature of data
  - strict guidelines
  - simple or low hanging fruit features are complicated
  - e.g. personally idetifiable data; it's in the nature of the data!
    - can't share anything between different entetites (customer clinics)
    - global frequencies would greatly benefit the end product


## Concluding remarks
Promote inhouse developed open source projects
