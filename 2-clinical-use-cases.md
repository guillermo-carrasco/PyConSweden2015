## Opening/introduction
Right now in Swedish and international hospitals there's a medical revolution taking place. And Python is at the core of it. In case of Sweden at least, it's difficult to see how it would be a revolution without extensive Python code.

It has transformed how patient with rare inherited diseases are diagnosed in Sweden and internationally.

Hi, my name is Robin Andeer and I help solve medical mysteries at SciLifeLab in Stockholm using Python.

The cause of diseases is commonly a very abstract concept. That was the case for the diseases I work with until some few years ago.

We sequence the source code for life; DNA. As the patient blood sample travels through our facility thousands of lines of Python code will eventually touch it.

Through the information we obtain/produce, we are able to pin point down to the most minute detail, the cause of a rare inherited disease. This has tremendous effect on patients, families, and society. Treatment, knowledge of our bodies, and reduced suffering for everyone involved. These are truly mysteries that have gone unanswered for sometimes 15 years or more without conclusions. Now we are getting straight to the conclusion within weeks.

## From Excel to Flask
When I started working around a year, year and a half ago, the delivered results were presented to clinicians and geneticists as a plain Excel sheet. Thousands of lines of text in an unwidely, and inherently static grid.

We knew we could do much better. This is when the idea for Scout was born. As a tool to help clinicians working with and interpreting the massive amounts of data from DNA sequencing.

We implemented it as a Flask server talking to a Mongo database that simplifies and adds interactivity to the whole process. This is truly a project that is at the core of the success of this form of diagnosis. If we do it right it can help both doctors and patients. If we don't the whole project will be slowed down.

## Iterations
We've reworked the core of the server twice. What started as a standalone Tornado server, transformed into a mess of a Flask+Tornado and extensive client side JavaScript code into the current cleaner solution relying heavily on server side rendering and limiting client side logic to a minimum.

We have to remind outselves that what we are building is not a fancy photo sharing service, although looks are still a plus, but a tool that will be used by people who just want to get their work done. Speed matters, but smooth transitions aren't a tradeoff worth making if it means less maintainable code.

I've found the painful way that whenever possible doing something is Python is 10 times eaiser than trying to handle it through JavaScript in the browser. Now this is our default and we couldn't be happier. If anything our site is now faster and more responsive. And significantly eaiser to iterate on.

## Security (not sure if I'll have time to get to this)
DNA is personally identifying by definition. These are also affected individuals. All data needs to be handled with care. We are setting up the server with restricted IP access. We require 2 factor Oauth sign in for all users. We log every action taken on the site. Using Flask extensions have made this learning process entirely doable.

We essentially store the entire Oauth code under a single Blueprint which keeps it's implementation separate from the rest of the code. Loose coupling. We also use MongoEngine as a nice interface to deal with documents in the database as objects in Python.
