# Outline, slides

## Clinical Genomics
Core facility at SciLifeLab

Bridge the gap between sending raw data to computer savvy researchers vs.
only somewhat computer litterate genetecists and doctors. Basically it
means processing the data as far as possible and intuitively visualize it.
The massive amounts of data can't simply be summed up in a pretty little graph.

### Mission
5 min analysis - would bring DNA sequencing into routine practise

## What?
Diagnose disoders that are 100% genetic, 100% inheritable. They often develop early
in life. These disorders are often rare and cause severe symptoms. Finding out the
cause of such a disoder can have tremendous beneficial effects for the patient,
family, and healthcare system.

The use of DNA sequencing in healthcare is pretty cool! Hospitals are *not* famous 
or moving fast or quickly adopting new technology. Now they are using the same tools
as cutting edge research.

## Why?
Patients can go undiagnosed for 15 years
Todays blunt tests give only vague indications of waht could be cusing these
disoders.

In contrast, using DNA sequencing technologies, we are able to go straight
for the root cause of the disorder and deliver conclusive results in *two
weeks*.

## How?
As the patient sample travels through our facility thousands of lines of
Python code will eventually touch it. I'm going to focus on the delivery
report.

This is the story...


## Excel sheet -> Web interface
In the beginning there was ... Excel. At least it's something familiar to
most people. Soon enough it got out of hand. It was very inflexible to
work with. Thousands of rows in an unwieldy and inherently static grid.

Researchers you can give very basic text files that need a lot of processing to
start making sense. We want to eliminate the need for any further non-manual
processing after we deliver our results.


## The Scout interface
To reduce the time it takes to go over each case we focus a lot of prioritizing the
information. This helps doctors to know what they should look at first. This is meant
to be part of routine work and not exploratory research so it makes sense.


## JavaScript vs. Python code
And then there was ... lots of JavaScript. But our input isn't optimized for this
kind of setup: we have mostly non-updating data and big tables which gives for
sluggish client side performance.

I can confess that when I started this project I saw it as a great opportunity to
learn more about e.g. Ember.js so I just picked it for the project. Only after my geek
entuthiasm had died down did I realize that this is a professional, clinical grade tool
and we shouldn't concern ourselves with user appeal too much.

The upsides are many: easier for us to collaborate because we stick to what everyone
already is familiar with (Python), more performant on our data, iteration and testing
*much* simpler, and doing it in Python >> JavaScript.


## MongoDB + MongoEngine
We implemented the backend in MySQL to begin with but decided to switch to MongoDB
when we went through a major refactor. There are a few undeniable upsides such as
the much simplified and more intuitive data model with e.g. nested comments. We can
also repopulate almost all data from the file system if thing do go wrong. Integrity
of the database isn't super duper important. The data that gets added over time is
limited and not always mission critical.

But most importantly; we need to keep track of what we've uploaded and be able to
repopulate the same information on request for old samples. You upload data once per
sample and make the clinical interpretation based on that. It can never change! We
also can't share data as much as you might want to think. Each sample needs to be
pretty isolated form the rest and especially between different institutes. So we
can't make use of aggresive normalization even if we wanted. This makes MongoDB
attractive as well!

### MongoEngine ODM as the API
MongoEngine as an interface to MongoDB - we've built our API around it!
Finally a chance to show some code examples ^^


## Concluding remarks
Promote inhouse developed open source projects!

-----------------------------

## [BONUS] So why are people still hesitant?
1. The high initial cost. One challenge is to prove that sequencing can
   effetively replace many of the old inconclusive tests.

2. Analysis of data is neither trivial nor standardized. For example how
   do you distingish an error from a mutation? Essentially 99.9% of the
   data generated is either too difficult to interpret or completely
   non-informative. Most sequences are just the same as what we know we
   find healthy individuals. To be honest we are generating a lot of
   "waste" that no ones has figured out a plan to do with. Kind of like
   a nuclear power plant.

## [BONUS] Steal conventions from GitHub
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
