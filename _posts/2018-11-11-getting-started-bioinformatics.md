---
layout: post
title:  "Getting started in bioinformatics - A beginners guide"
date:   2018-11-11
desc: "Resources and my two cents about how to start programming and learning about bioinformatics"
keywords: "computational,python,data-science,biology,compbio,bioinformatics,learning,courses,recommendations,references"
categories: [Bioinformatics]
tags: [learning,bioinformatics,beginners]
icon: icon-python
---

As a computer scientist, programming for more than 10 years now, it is natural for me to look for resources online when I want to learn something new. In my experience many computer scientists have a tendency to learn in an autodidactic manner which facilitates the exploration of previously unknown knowledge.
As I recently started to go into the field of Bioinformatics I work with lots of biologists who never touched a command line let alone writing their own scripts and programs. From that perspective it can be intimidating to find a good starting point to learn the essentials of programming and bioinformatics; So I try to provide one here.

It is important to mention that the web is full of useful resources and it is not on me to duplicate all the information that is already out there. Also, there are already good blog posts which try to summarize useful resources (as this blog post does). For completeness I try to reference some of these posts here as well.

# How you find stuff

Important websites related to programming and bioinformatics are GitHub, Reddit, Stackoverflow and Biostars. These websites will pop up in your google searches from time to time (i.e. very often) so it is good you read about them already: 

## GitHub

Since GitHub started in 2008 it became the major platform for sharing source code. It facilitates sharing your own projects and source code. Many scientific publications provide their source code on this platform.

Similar but less popular websites include Bitbucket and GitLab

## reddit

Reddit is so popular nowadays that it feels weird to introduce it here. However it is still worth noting that there are small subreddits for bioinformatics and other related fields that can give a great starting point when looking for information (as you well see later).

## stackoverflow

Stackoverflow is the most popular website for programming related problems people run into. When you run into problems (e.g. you have a hard time understanding the error message your program shows) chances are high somebody addressed this problem on stackoverflow and got a simple solution.

## Biostars

Biostarts is a community for bioinformatics related question. It focuses more on the usage for bioinformatics tools than on programming questions. It is comparable to stackoverflow in the way how it functions.

An alternative website addressing specificially sequencing problems is seqanswers.com

# Technologies


## Command line

Before Apple und later Microsoft brought graphical user interfaces (GUIs, the type of user interface that almost everyone is using nowadays) to the masses, the *command line* was the only interface to the computer. And still today many people use command line within their graphical user interface as it offers a set of features that is hard to acquire with graphical applications.

The command line can simply be seen as an alternative way to interact with computers which is based solely on text. To access the command line we use a *terminal* program. Popular terminal programs are iTerm2 (for macOS) and Powershell (Windows; although I would not recommend using Windows, especially when it comes to programming).

Udacity offers a free interactive introduction into the Linux Shell (the most popular command line) which I would recommend to go through (note that you first need te register on their website and then click the link again to open the course):

https://classroom.udacity.com/courses/ud595

The Shell (and other command lines) also enables you to write so called shell-scripts. These are just normal text files containing the same commands which you would otherwise type manually in a shell. They allow to automate your processes in an easy and reproducible way. See this very simple example of one of my scripts that downloads and processes a file.

```
# This is a comment, it starts with a '#' and is not executed. It's just there to document your code

# create a directory data
mkdir data

# download repeat masker files (which try to annotate transposable elements) from the M. Hammell lab
wget http://labshare.cshl.edu/shares/mhammelllab/www-data/TEToolkit/TE_GTF/mm10_rmsk_TE.gtf.gz
# unzip the file
gunzip mm10_rmsk_TE.gtf.gz
# run your self written python script on the downloaded data, writing the output of your script into a file in the directory the script created before
python process.py < mm10_rmsk_TE.gtf > data/mm10_rmsk_TE.gff3
```

You will stumble upon such scripts (their filename usually ends with '.sh' ) and eventually write your own ones soon.

## Progamming languages

Often it is sufficient to use available programs, possibly combining and automating them inside a shell script, in order to solve your problem. However when you need to process data in a very specific way, there might be no program written for your task. In that case you need ot rely on your own programs.

There are dozens of programming languages which all have their advantages and their disadvantages. In the realm of data science (which includes bioinformatics for many problems), there are a bunch of languages which are dominant in the field owing their simplicity to achieve results with minimal learning and programming effort. The two most popular ones are R and Python.

### Python vs R

While R was invented as a language for statisticians, Python is a programming language that targets simplicity, readability of code and universal usage. There are Python libraries for nearly anything: [Building](http://flask.pocoo.org "Flask") [websites](https://djangoproject.com "Django"), [scraping](https://scrapy.org "scrapy"), [image](https://opencv.org/) [processing](https://python-pillow.org/), [network](https://scapy.net/) [analysis](https://twistedmatrix.com/trac/), [graphical](https://www.nltk.org/) [user](https://wiki.python.org/moin/TkInter) [interfaces](https://wiki.python.org/moin/PyQt), [language processing](https://www.nltk.org/), and of course [all](https://www.numpy.org "Numpy") [kinds](https://www.scipy.org "Scipy") [of](http://pandas.pydata.org "Pandas") [data](https://matplotlib.org "Matplotlib") [analytics](https://pytorch.org "PyTorch").

The Python language enables developers to easily write code that is understandable and shareable. In comparison to R, it is clear and consistent in its usage which makes it easier to understand and employ in the long term. To get a feeling how the data science community shifts towards using Python instead of R have a look at the [google search trend](https://trends.google.de/trends/explore?date=today%205-y&q=R%20for%20data%20science,python%20data%20science).

### Quick start with Python

From my own personal experience, learning a programming language (especially your first one) is a trial and error procedure similar to learning a normal language: You will need to study the basics by reading the manual (or watching videos) but you won't internalize material if you don't practice and apply it. Luckily there are many resources that combine both of these steps. There are courses which are more hand-holding (like the shell course from udacity) and once that are more comprehensive. What fits you best depends on you. I provide and describe three types of resources here. Don't let the abundance of resources stop you. All these resources are great starting points and if you don't have a preference just pick one at random.

#### Dive into Python 3

This is the book I learned Python with a long time ago (in fact I learned it still using the Python 2 version of the book (Python 2 and 3 are very similar though it is discouraged to write code for Python 2 anymore)). It provides a very comprehensive yet easy to understand resource of Python 3.

[Dive into Python 3 [PDF]](http://histo.ucsf.edu/BMS270/diveintopython3-r802.pdf)

While a book is less hand-holding than a video based online course, it forces you to get comfortable with the programming tools (source code files, editors, command line terminals) you will use later on.

Similar books that are recommended frequently are
- [Automate the boring stuff](https://automatetheboringstuff.com/)
- [Learn Python the hard way](https://learnpythonthehardway.org/python3/) 

#### Interactive video courses

If you prefer watching videos videos over reading chapters, there are a variety of Python Introduction courses on Udacity, edX, coursera and so on. These courses provide everything you need for learning in the browser: Lecture videos, Exercises, and a command line where you can solve the exercises. While this comes in handy, I would advise you to also play around with code in your system's terminal (instead of the browser) to get comfortable with a more realistic scenario (you won't use the web terminals once you are done with the course and want to solve real problems). 

[Introduction to Python Programming](https://classroom.udacity.com/courses/ud1110) from Udacity offers a very smooth introduction into Python and programming in general. 

Another course you can check out that also goes a little into data science with Python is [DAT208x: Introduction to Python for Data Science](https://courses.edx.org/courses/course-v1:Microsoft+DAT208x+3T2018/course/) (at the cost of a faster learning pace).

#### The Python Tutorial

The Python website itself is hosting a comprehensive [Python 3 Tutorial](https://docs.python.org/3/tutorial/). It is a little more compact than a book, so if you are not satisfied with one of the books mentioned above, just click through the tutorial and see if this learning style fits you better.

### From Python to Bioinformatics

When I started to program, I often felt like there would be no problem that I could work on and therefore I could not apply and improve my skills. While this proved to be a lack of experience and imagination, I know how hard it is to start after having understood the first principles.

Therefore it is really important to have problems and ideas to work on. Conveniently there is a website full of bioinformatics exercises that allows you to both train your programming skills and in the meantime learn to solve Bioinformatics questions: [Rosland.info](http://rosalind.info). 

After registering and logging in on the website, you will get guides through the function of the website. There are three main problem categories which I recommend to process in the given order:

#### Python village

http://rosalind.info/problems/list-view/?location=python-village

This is a very good repetition for your Python skills and it will help you get used to the way Rosalind works.

#### Bioinformatics Stronghold

http://rosalind.info/problems/list-view/

Here you will start solving real bioinformatics problems. While the first once are rather easy, they increase in difficulty.

#### Bioinformatics Armory

http://rosalind.info/problems/list-view/?location=bioinformatics-armory

Bioinformatics is not only about programming. It is also about just to use and combine the appropriate tools for the data in question. This third problem category introduces a variety of such tools and lets you experiment with them in order to get an intuition of when and how to employ them.

# Just do it

All that being said, it is now on your own to solve the problems you are interested in. You will run into many issues, not understanding why things don't work as you expected. In those numerous cases always be assured that you are not the only one running into these problems, so a simple web search will most likely help you out. One thing you will learn along with the basics of programming is to stay persistent and to not give up. It will pay out!

If you have any comment, feedback or question, leave a comment or contact me on twitter (@muronglizi) or by e-mail (moritz.schaefer@biol.ethz.ch)

# References

As promised I'll put some links here of websites that already discussed on how to get started with programming and bioinformatics. For example, numerous people asked at reddit for resources to learn Python and Bioinformatics basics and they received a lot of useful links. Have a look into these resources to get a broader view of what is recommended for learning. 

- https://www.biostars.org/p/311/
- https://www.reddit.com/r/learnpython/comments/6f7ybq/what_is_the_best_way_to_learn_python_3/
- https://www.reddit.com/r/learnprogramming/comments/83oes2/recommendations_for_most_effective_way_to_learn/
- https://www.reddit.com/r/learnprogramming/comments/88xf0o/whats_the_best_way_to_learn_python_online_for_free/
- https://www.quora.com/How-should-you-start-learning-programming
- https://www.youtube.com/watch?v=A8vjlqUOniY
- https://github.com/ossu/bioinformatics
- https://www.reddit.com/r/bioinformatics/comments/6ccpfe/advice_for_learning_bioinformatics/
- https://edwardslab.bmcb.georgetown.edu/teaching/bchb524/2016/
- https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005871

