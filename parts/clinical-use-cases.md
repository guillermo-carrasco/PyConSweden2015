## Motivation and background
- Cheaper: 1 test vs. multiple tests
- Less time consuming: 2 weeks vs. 15 years
- Conclusive: exact cause of disease vs. guesses
- People still hesitate because analysis is not trivial: like looking for a needle in a haystack ... of needels.


## Why?
- We are trying to take the burden of analyzing results from doctors
  + Quicker, simpler, more approachable
- Revolution in healthcare


## Unique aspect of our implementation

### Server side rendering galore
- We already went down the client side route...
  + mostly non-updating data, big tables, sluggish performance
- Much easier to develop, fast enough, sometimes more responsive
- tip: look at GitHub site and copy conventions!
  + How they order URLs
  + What's server side vs. client side rendered
  + Log out issues resolved when adding a form

### Why did we opt for MongoDB?
- MongoEngine as an interface

### Components on client side
- Components over jQuery
- Jinja filter for {{}}
- Web components syntax


## Opening/introduction
Right now in Swedish and international hospitals there's a medical revolution taking place. And Python is at the core of it.

It has transformed how patient with rare inherited diseases are diagnosed in Sweden and internationally.

Hi, my name is Robin Andeer and I help solve medical mysteries at SciLifeLab in Stockholm using Python.

The cause of diseases is commonly a very abstract concept. That was the case for the diseases we work with until some few years ago.

We sequence the source code for life; DNA. As the patient blood sample travels through our facility thousands of lines of Python code will eventually touch it.

Through the information we obtain/produce, we are able to pin point down to the most minute detail, the cause of a rare inherited disease. This has tremendous effect on patients, families, and society. Treatment, knowledge of our bodies, and reduced suffering for everyone involved. These are truly mysteries that have gone unanswered for sometimes 15 years or more without conclusions. Now we are getting straight to the conclusion within weeks.


## From Excel to Flask
When I started working around a year, year and a half ago, the delivered results were presented to clinicians and geneticists as a plain Excel sheet. Thousands of lines of text in an unwieldy, and inherently static grid.

We knew we could do much better. This is when the idea for Scout was born. As a tool to help clinicians working with and interpreting the massive amounts of data from DNA sequencing.

We implemented it as a Flask server talking to a Mongo database that simplifies and adds interactivity to the whole process. This is truly a project that is at the core of the success of this form of diagnosis. If we do it right it can help both doctors and patients. If we don't the whole project will be slowed down.


## Iterations
We've reworked the core of the server twice. What started as a standalone Tornado server, transformed into a mess of a Flask+Tornado and extensive client side JavaScript code into the current cleaner solution relying heavily on server side rendering and limiting client side logic to a minimum.

We have to remind ourselves that what we are building is not a fancy photo sharing service, although looks are still a plus, but a tool that will be used by people who just want to get their work done. Speed matters, but smooth transitions aren't a trade off worth making if it means less maintainable code.

I've found the painful way that whenever possible doing something is Python is 10 times easier than trying to handle it through JavaScript in the browser. Now this is our default and we couldn't be happier. If anything our site is now faster and more responsive. And significantly easier to iterate on.


## Security (not sure if I'll have time to get to this)
DNA is personally identifying by definition. These are also affected individuals. All data needs to be handled with care. We are setting up the server with restricted IP access. We require 2 factor Oauth sign in for all users. We log every action taken on the site. Using Flask extensions have made this learning process entirely doable.

We essentially store the entire Oauth code under a single Blueprint which keeps it's implementation separate from the rest of the code. Loose coupling. We also use MongoEngine as a nice interface to deal with documents in the database as objects in Python.

-----------------

## Scout
We previously built a JavaScript heavy solution that quickly got out of hand. Therefore we pivoted to a Python native solution which made it easier for us to collaborate, it was still plenty fast, and made iteration much simpler.

We still leverage components (Vue.js and SCSS) on the front end so that we don't need to mess too much with jQuery.

Using Python (Click, Flask) has made interfaces really intuitive and easy to develop and making them conform to UNIX pipelines and standards.

One interesting point to talk about would perhaps be what it's like to be forced to validate every release. What are the up- and downsides? What do we need to think about extra and what consequences does this how on our development work flow.
  - Examples: bugs like not sorting the list of samples, incorrect GT call

Chance for conclusive diagnosis, chance for treatable diagnosis, you will at least learn more about genetics etc.

To also get into some actual Python code and conventions I could talk about using MongoEngine as an interface ^^ to MongoDB.
- PyMongo for indexes, weird syntax in ODM
