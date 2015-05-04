# Introduction

## 0. Brief introduction to genomics
Compare DNA and other concepts to programming!

1. The DNA is byte code but instead of 0s and 1s we have As, Cs, Ts, and Gs.

2. So what do they encode? Well combining a streach of bases you get genes. A gene
   encodes a protein: very same you eat to build muscles. They usually have one very
   specific task to carry out in the body.

3. Genes are further grouped into longer streaches of DNA strands called chromosomes
   which make up the software for your body.

4. Lastly this code is run inside the cell which is the hardware that understands what
   to make of the code. Basically you can "boot up" a cell with whatever DNA source
   code you want.

### How is the data generated?
...

### How is it clinically useful?
The genome is your genes, your DNA. It's the inheritable code that determines
fundamentally how you will develop. When the code is passed down from parents to child,
the entire code is copied and mixed manually. This process introduces bugs, most of
which are perfectly benign. But when they rarely cause disease we are interested in
finding and learning more about them.


## 1. What makes Python uniquely capable of handling NGS data?
[Why python?](http://www.nature.com/news/programming-pick-up-python-1.16833)

Python is a very versatile and easy to use language. It is famous for having a very
quick learning curve:

![Python XKCD](/assets/python.png?raw=True)

This eases the introduction to programming to people not used to it like may be
molecular biologists or scientists in general. Also the fact that it is so widely
used gives new programmers a lot of extra help in forums, tutorials, conferences, etc.

A strong feature in life sciences is how easy it is to work with files and strings in
Python, since _every_ scientific computing program needs to work with input files, as
basically they work with results from lab experiments that come in a large range of
different formats. Perfect for glueing tools together.

As a general purpose yet simple language for beginners, this is probably also why
Python is so prevalent in bioinformatics. In fact Python is at near monopoly in Science
([ref][monopoly]). There's a big open source community (numpy, pandas) which ties really
well into the academia-heavy field. A downside is that many groups are still
transitioning to using Git and testing for example.

Reverse the question: what if Python didn't exist?
  - Where would that have left us?
  - It's an impossible question but it's sort of scary to imagine that reality... Perl...
  - I think at least we are better off with our current situation!

## 2. Who are these two guys?
Spanish vs. Swedish, CS vs. Biology, DevOps vs. Design

### Guillermo Carrasco
My name is Guillermo Carrasco and I am a software engineer infiltrated between biologists :)

To be honest, I ended up in Life Sciences by pure chance. A couple of years ago I was
looking for a part time job to pay my engineering studies in Spain, and I saw a system
administration job advertisement at the Molecular Biology Institute of Barcelona. After
applying and being hired, I started working with people that were so passionate
about what they were doing that they were willing to learn how to code by themselves
in order to achieve what they were looking for. I've always admire that so much, took
me 5 years of university!

I decided to do my Msc.Thesis abroad and this is how I ended up in Science For Life
Laboratory, where my interest on life science has been growing and growing, always
motivated by the strong open source and collaborative environment that is
growing among scientists.

Nowadays I spend my day helping researchers with data management and software development.

### Robin Andeer
My name is Robin Andeer and I develop tools to solve medical mysteries at SciLifeLab.

Many scientists spend a lot of time doing research. When it comes time to analyze your
data you often realize that no one has built something to meet your specific research-y
needs.

So you start to inch your way to becoming a programmer to accomplish your goals. All of
a sudden you notice you are really more of a developer than a researcher. Your mindset
has changed and you find these new technical problems very interesting in their own to
tackle.

It's very motivating to still have the medical/research goals in the background, but
still. This was at least my own experience. Starting in the lab in school, and now I'm
sitting in front of a computer all day - and couldn't be happier to be on the other side
of the glass walls.

I believe this story resonates with many "scientific" programmers. Some of the most
influential developers in the field are ex-researchers that have initially taught
themselves to code. Brad Chapman, Aaron Quinlan, etc. [insert GH streak] Do you think he
has time for lab work anymore? Hehe. Now *they* are pushing the envelope when it comes
to building scientific software.


[monopoly]: http://news.kynosarges.org/2015/04/05/programming-languages-in-2014/
