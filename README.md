# Proposal sketch for PyCon Sweden 2015

## Some notes and suggestions on how to make a proposal

* [Proposal advice](https://us.pycon.org/2015/speaking/proposal_advice/)
* [Proposal resources](https://us.pycon.org/2015/speaking/proposal-resources/)
* [Proposal sample](https://us.pycon.org/2015/speaking/proposal_advice/samples/SpacePug/)

## Brainstorming

**What do we want to talk about?**

* Brief introduction of genomics (really short, just to explain where the
  data comes from, how is it generated, and why is it useful)

* [Why python?](http://www.nature.com/news/programming-pick-up-python-1.16833)
  Easy to learn, powerful, perfect for glueing, enormous number of
  libraries, huge community support

* Data management and the importance of automation: Disks filling up
  quickly, long term storage importance, manual -> error prone and spikes of
  work.

* Data analysis: NGI-pipeline description (hopefully it will be more mature
  by the time of the presentation)

* Clinical use cases:
  - Briefly about motivation from real world use of genomics in the clinic
  - Delivering data to clinicians (a.k.a. non-bioinformaticians)
    => [Scout][scout]
  - Providing clinically relevant QC metrics => [Chanjo][chanjo]
  - Restrictions and the lesson that clinicians don't like change
    + This is work for them, they just want to get it done

* Open source!!! Remark that all our code is open source, definitely
  link to the [open source site][open-source].

## Proposal

### Title

Python in Life Sciences:
How Python Drives the Analysis of Billions of DNA Sequences

### Category

Science

### Duration

I would prefer a 30 minutes slot

### Description

[The first part...]

The second part will contrast the different aspects of dealing with end users
without extensive data science background. The focus will be on our in-house
developed Flask server for delivering results and a command line tool used to
generate QC metrics reports.

### Audience

- Any Python programmer with interest in how Python is applied to the growing
  life sciences field of genomics.

- Any scientist with interest in how other labs are managing the complex data
  flow and analysis of a genomics facility.

### Python level

Intermediate - Advanced

### Objectives

The attendees will learn about a state of the art genomics pipeline and
how we use Python to manage and analyze large amounts of biologically
significant data.

In the second part they will learn how we adapt the output data for clinicians
and other non-bioinfo people.

### Detailed abstract

### Outline

### Additional notes

### Additional requirements



[chanjo]: https://chanjo.readthedocs.org/en/latest/
[open-source]: http://opensource.scilifelab.se/
[scout]: http://www.clinicalgenomics.se/scout/
