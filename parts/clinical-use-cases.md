## What are we doing?
- Diagnosing children with rare inherited diseases
  - Often shrouded in mystery
  - Patients go undiagnosed for 15 years if they survive that long
- We are able to go straight for the root cause of the disease and deliver results in two weeks
  - That's 1 possibly conclusive test over multiple garanteed inconclusive tests

- We sequence the source code for life; DNA
  - As the patient blood sample travels through our facility thousands of lines of Python code will eventually touch it.

- Tremendous effect on patients, families, and society/healthcare system
  - Treatment, knowledge of our bodies, and reduced suffering for everyone involved

- People still hesitate: analysis is not trivial
  - "like looking for a needle in a haystack ... of needels"
  - Huge amounts of data, 99.9% no one really knows what to do with or how to store and backup
    - It's a little like nuclear power plants - we generate a lot of "waste" that no ones has figured out a plan to do with

## Why are we doing this? Non-python
- In the beginning there was ... Excel
  - Thousands of rows in an unwieldy, and inherently static grid

- Reasons to improve
  - we are dealing with routine tasks more than exploratory research
    - prioritize variants and focus less on filtering for example
  - quicker turn-around times
  - automate parts that can be automated (free up doctors)

- We want to revolutionize healthcare.
  - [insert Clinical Genomics objectives]

If we do it right it can help both doctors and patients. If we don't the whole project will be slowed down.

## What are we going to cover?
- Flask app + MongoDB/MongoEngine
- Logging??
- Jinja/Flask best practises
  + Macros in templates are something you often forget about

Hopefully I can share some best practises around working with Flask and teach you something new to test in your own projects.

## How does the field look like? Current situation (not essential)
- Lots of activity around the world (GB)
- Many "competitors" focus on research + more complicated to work with

## What is the unique problems? - how are you solving them?
- close collaboration with end users
  - blessing and a curse
  - likely to deliver what they want
  - risk of building something that is too tailored to be useful for others

- clinical/sensitive nature of data
  - strict guidelines
  - simple or low hanging fruit features are complicated
  - e.g. personally idetifiable data; it's in the nature of the data!
    - can't share anything between different entetites (customer clinics)
    - global frequencies would greatly benefit the end product

### Server side rendering galore
- in the beginning there was ... chaos
  - Flask+Tornado + lots of JavaScript
    - mostly non-updating data, big tables, sluggish performance
  - we repented: rely on server side + minimize client side
  - easier for us to collaborate
  - it more performant
  - iteration and testing *much* simpler
  - users just want to get their work done
  - doing it in Python >> JavaScript

- tip: look at GitHub site and copy conventions!
  + How they order URLs
  + What's server side vs. client side rendered
  + Log out issues resolved when adding a form

- leverage components (Vue.js and SCSS) on what client side we have
  - don't need to mess too much with jQuery.
  - Jinja filter for {{}}
  - Web components syntax

### Why did we opt for MongoDB?
- Bring up simplified example for comments
  - This is different than most regular setups because we need to separates comments between institutes and cases...
  - Much more intuitive in MongoDB

To also get into some actual Python code and conventions I could talk about using MongoEngine as an interface ^^ to MongoDB.
- PyMongo for indexes, weird syntax in ODM

We find it useful to not worry too much about data duplication and the rest of the "schema" just make things more intuitive to think about.

### Security concerns - TODO: refactor this
DNA is personally identifying by definition. These are also affected individuals. All data needs to be handled with care. We are setting up the server with restricted IP access. We require 2 factor Oauth sign in for all users. We log every action taken on the site. Using Flask extensions have made this learning process entirely doable.

We essentially store the entire Oauth code under a single Blueprint which keeps it's implementation separate from the rest of the code. Loose coupling. We also use MongoEngine as a nice interface to deal with documents in the database as objects in Python.

One interesting point to talk about would perhaps be what it's like to be forced to validate every release. What are the up- and downsides? What do we need to think about extra and what consequences does this how on our development work flow.
  - Examples: bugs like not sorting the list of samples, incorrect GT call
