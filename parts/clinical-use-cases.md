## What are we doing?
Diagnosing children with rare inherited diseases. Often shrouded in mystery. Patients stay in the systems undiagnosed for 15 years. We go straight for the root cause of the disease and deliver results in two weeks time. That's 1 possibly conclusive test over multiple garanteed inconclusive tests.

We sequence the source code for life; DNA. As the patient blood sample travels through our facility thousands of lines of Python code will eventually touch it.

This has tremendous effect on patients, families, and society/healthcare system. Treatment, knowledge of our bodies, and reduced suffering for everyone involved. These are truly mysteries that have gone unanswered for sometimes 15 years or more without conclusions. Now we are getting straight to the conclusion within weeks.

However, people still hesitate because analysis is not trivial: like looking for a needle in a haystack ... of needels. We also generate huge amounts of data of which 99.9% no one really knows what to do with or how to store and backup.

## Why are we doing this? Non-python
When I started working on these problems the doctors were litterally delivered an unwieldy Excel sheet that they had to sift through manually. Thousands of rows in an unwieldy, and inherently static grid.

We develop tools for use by clinicians to enable as quick turn-around times as possible. Take the burden of automatable parts of the analysis from the doctors. The difference from what Guillermo was talking about is that we are deling with more routine tasks not exploratory research. We therefore prioritize variants and focus less on filtering for example.

We want to revolutionize healthcare. We believe this can help patient [more Clinical Genomics objectives]

If we do it right it can help both doctors and patients. If we don't the whole project will be slowed down.

## What are we going to cover?
The variant browser interface which is a Flask application with a MongoDB backend. To get structure in the database we define the "schema" using an ODM (MongoEngine). Hopefully I can share some best practises around working with Flask and teach you something new to test in your own projects.

## How does the field look like? Current situation
With major initiatives launching all over the world and with GB as a sort of genomics hub there are alternatives starting to pop up. Many of them are much more researcer focused and a lot more complicated to work with than what we are building.

We are also working in very close collaboration with our end users which is both a blessing and a curse. We are likely to deliver what they want but risk building something that is too tailored to be very useful for other people from outside.

## What is the unique problems? - how are you solving them?
We need to consider the clinical nature of our data. We are working under strict guidelines and many of the simple or low hanging fruit features are complicated by this fact. One issue that keeps coming back to us is that no matter how we do, we are storing personally idetifiable data; it's in the nature of the data! This makes is particularly hard to share almost anything between different entetites like different customer clinics. Even if the data like global frequencies would greatly benefit the end product. The end does not quite justify the means in this case.

### Server side rendering galore
We initially built Scout into a mess of a Flask+Tornado and extensive client side JavaScript code into the current cleaner solution relying heavily on server side rendering and limiting client side logic to a minimum.

Therefore we pivoted to a Python native solution which made it easier for us to collaborate, it was still plenty fast, and made iteration much simpler.

I had to remind myself that what we are building is not a fancy photo sharing service, although looks are still a plus, but a tool that will be used by people who just want to get their work done. Speed matters, but smooth transitions aren't a trade off worth making if it means less maintainable code.

I've found the painful way that whenever possible doing something is Python is 10 times easier than trying to handle it through JavaScript in the browser. Now this is our default and we couldn't be happier. If anything our site is now faster and more responsive. And significantly easier to iterate on.

We still leverage components (Vue.js and SCSS) on the front end so that we don't need to mess too much with jQuery.

- We already went down the client side route...
  + mostly non-updating data, big tables, sluggish performance
- Much easier to develop, fast enough, sometimes more responsive
- tip: look at GitHub site and copy conventions!
  + How they order URLs
  + What's server side vs. client side rendered
  + Log out issues resolved when adding a form

### Why did we opt for MongoDB?
To also get into some actual Python code and conventions I could talk about using MongoEngine as an interface ^^ to MongoDB.
- PyMongo for indexes, weird syntax in ODM

- MongoEngine as an interface
- Bring up simplified example for comments
  - This is different than most regular setups because we need to separates comments between institutes and cases...
  - Much more intuitive in MongoDB

### Components on client side
- Components over jQuery
- Jinja filter for {{}}
- Web components syntax


### Security concerns
DNA is personally identifying by definition. These are also affected individuals. All data needs to be handled with care. We are setting up the server with restricted IP access. We require 2 factor Oauth sign in for all users. We log every action taken on the site. Using Flask extensions have made this learning process entirely doable.

We essentially store the entire Oauth code under a single Blueprint which keeps it's implementation separate from the rest of the code. Loose coupling. We also use MongoEngine as a nice interface to deal with documents in the database as objects in Python.

One interesting point to talk about would perhaps be what it's like to be forced to validate every release. What are the up- and downsides? What do we need to think about extra and what consequences does this how on our development work flow.
  - Examples: bugs like not sorting the list of samples, incorrect GT call
