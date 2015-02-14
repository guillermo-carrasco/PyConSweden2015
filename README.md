# Proposal sketch for PyCon Sweden 2015

## Some notes and suggestions on how to make a proposal

* [Proposal advice](https://us.pycon.org/2015/speaking/proposal_advice/)
* [Proposal resources](https://us.pycon.org/2015/speaking/proposal-resources/)
* [Proposal sample](https://us.pycon.org/2015/speaking/proposal_advice/samples/SpacePug/)
* [PyCon 2014 Biology talk](http://blog.karinlag.no/2014/06/sweden/)
  - Too easy for the audience

## Brainstorming

**What do we want to talk about?**

* Brief introduction of genomics (really short, just to explain where the
  data comes from, how is it generated, and why is it useful)
  - Do we want to include clinical usefulness here or later? It's a pretty powerful opener I think :)

* [Why python?](http://www.nature.com/news/programming-pick-up-python-1.16833)
  Easy to learn, powerful, perfect for glueing, enormous number of
  libraries, huge community support, very easy choice in bioinformatics community, quickly growing to be the de facto standard.

* Data management and the importance of automation: Disks filling up
  quickly, long term storage importance, manual -> error prone and spikes of
  work.

* Data analysis: NGI-pipeline description (it will be more mature
  by the time of the presentation)

* Clinical use cases:
  - Motivation from real world use of genomics in the clinic
  - Delivering data to clinicians (a.k.a. non-bioinformaticians)
    => [Scout][scout]

* Open source!!! Remark that all our code is open source, definitely
  link to the [open source site][open-source].
  - Develop according to open source model: good documentation practices
  - This is a good way to end the talk I think!

## Proposal

### Title

Python in Life Sciences:
How Python Drives the Analysis of Billions of DNA Sequences

### Category

Science

### Duration

I would prefer a 30 minutes slot

### Description

A genomics research center produces larges amount of data per day, a single one of
the new [Illumina machines](http://www.illumina.com/systems/hiseq-x-sequencing-system/performance-specifications.html)
for sequencing can produce around 2TB of data composed by millions of files in less
than 3 days.

The first part will focus of a Python pipeline developed at Science For Life Laboratory for the automated analysis of all of that data, the [NGI-pipeline](https://github.com/NationalGenomicsInfrastructure/ngi_pipeline).

The second part will tell the story of how Python is at the center of a medical revolution. It will focus on how we have fundamentally changed the way we deliver data to "regular" clinicians using a Flask powered website.

### Audience

- Any Python programmer with interest in how Python is applied to the growing
  life sciences field of genomics.

- Any scientist with interest in how other labs are managing the complex data
  flow and analysis of a genomics facility.

### Python level

Intermediate - Advanced

### Objectives

The attendees will learn about a state of the art genomics pipeline and
how we use Python to manage, store and analyze large amounts of biologically
significant data.

They will also get a peak behind the website that allows clinicians to
productively review results from DNA sequencing and make life changing
diagnoses.

### Detailed abstract
TODO: Do we need to write this? I think it's covered elsewhere, no?

### Outline
TODO: how long are we planning to speak? 10 + 10 + 5 min + Q&A?

**Introduction**

**Part 1**

**Part 2**

1. Introduce DNA sequencing + the role of Python in the clinic (5 min)

2. Scout, our web based data delivery interface (10 min)
  1. From Excel sheet to Flask website
  2. From JavaScript-mess to Python-bliss

**Finale**

1. Doing everything in open source; GitHub, documentation, [...]
2. Promoting great project through our open source portal

### Additional notes

### Additional requirements



[chanjo]: https://chanjo.readthedocs.org/en/latest/
[open-source]: http://opensource.scilifelab.se/
[scout]: http://www.clinicalgenomics.se/scout/
