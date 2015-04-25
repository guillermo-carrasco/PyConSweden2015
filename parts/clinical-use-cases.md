# Outline, slides

## Clinical Genomics and our mission
Clinical Genomics at SciLifeLab: 5 min analysis

Bridge the gap between sending raw data to computer savvy researchers vs. only somewhat computer litterate genetecists and doctors. Basically it means processing the data as far as possible and intuitively visualize it.

## Genomics in healthcare today
We focus on rare inherited disoders. They are often severe and have simple
cause-effect relationships. You find a defect gene and there's your cause.
Done. But it's not quite so simple most of the time.

Patients can go undiagnosed for 15 years, if they
survive that long. Each individual test can only ever give indications of
what the cause of the symtoms really is.

However, people still hesitate mainly because of the high initial cost and because the analysis is not trivial. Someone compared it to: "looking for a needle in a haystack ... of needels". For each patient, relatively, we generate huge amounts of data, 99.9% of which no one really knows what to do with or interpret.

Prices are coming down rather rapidly but to be honest it's a little like nuclear power plants - we generate a lot of "waste" that no ones has figured out a plan to do with.

In contrast, using DNA sequencing technologies, we are able to go straight for the root cause of the disorder and deliver conclusive results in *two weeks*. As the patient sample travels through our facility thousands of lines of Python code will eventually touch it.

Clinics already routinely send in patient samples for sequencing. This is pretty cool because healthcare is infamous for not moving very fast or adapting new technology.

## Excel sheet -> Web interface
What these guys are delivering to researchers is very basic text files usually. Low level data that needs a lot of processing to start making sense. We have to ambition to take things a lot further. Basically we want to eliminate the need for any further compute processing after we deliver our results.

Instead of giving users extensive tools to filter out the interesting results we tend to prioritize what they should look into first. The ambition is that this is routine work and not exploratory research so it makes sense. This is also what many similar tools are focused on; filtering etc.

First attempt: Excel... at least it's familiar to most people. Soon enough it got out of hand. It was very inflexible to work with. It also took too much time to look into each case to be practical.

- In the beginning there was ... Excel
  - Thousands of rows in an unwieldy, and inherently static grid

## Scale: JavaScript vs. Python code, swinging over
Kind of the oposite of where most of the web seems to be heading but this is a professional, clinical grade tool and we don't need to concern ourselves with user appeal too much. But it's always fun to make something pretty.

- in the beginning there was ... lots of JavaScript
    - mostly non-updating data, big tables, sluggish performance
  - we repented: rely on server side + minimize client side
  - easier for us to collaborate
  - more performant
  - iteration and testing *much* simpler
  - users just want to get their work done
  - doing it in Python >> JavaScript

- Jinja/Flask best practises
  + Macros in templates are something you often forget about

- leverage components (Vue.js and SCSS) on what client side we have
  - don't need to mess too much with jQuery.
  - Jinja filter for {{}}
  - Web components syntax

## Copy conventions from GitHub
URL conventions (real names, consistency)
Form to submit a logout button press
Mostly server side rendered, partly client side magic, components

## MongoDB + MongoEngine
We find it useful to not worry too much about data duplication and the rest of the "schema" just make things more intuitive to think about.

MongoEngine as an interface to MongoDB
PyMongo for indexes, weird syntax in ODM (don't know much about this though...)

- Bring up simplified example for comments
  - This is different than most regular setups because we need to separates comments between institutes and cases...
  - Much more intuitive in MongoDB

- clinical/sensitive nature of data
  - strict guidelines
  - simple or low hanging fruit features are complicated
  - e.g. personally idetifiable data; it's in the nature of the data!
    - can't share anything between different entetites (customer clinics)
    - global frequencies would greatly benefit the end product

## Concluding remarks
Promote inhouse developed open source projects
