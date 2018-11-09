As a computer scientist, programming for more than 10 years now, it is natural for me to look for resources online when I want to learn something new. In my experience many computer scientists have a tendency to learn in an autodidactic manner which facilitates the exploration of previously unknown knowledge.

As I recently started to go into the field of Bioinformatics I work with lots of biologists who never touched a command line let alone writing their own scripts and programs. From that perspective it can be intimidating to find a good starting point to learn the essentials of programming and bioinformatics; So I try to provide one here.

It is important to mention that the web is full of useful resources and it is not on me to duplicate all the information that is already out there. Also, there are already good blog posts which try to summarize useful resources (as this blog post does). For completeness I try to reference some of these posts here as well.

# How you find stuff

Very important websites related to programming and bioinformatics are GitHub, Reddit, Stackoverflow and Biostars. These websites will pop up in your google searches from time to time (i.e. very often) so it is good you read about them already: 

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

The Shell (and other command lines) also enables you to write so called shell-scripts. These are just normal text files containing the same commands which you would type manually in a shell. They allow to automate your processes in an easy and reproducible way. See this very simple example of one of my scripts that downloads and processes a file.

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

## Progamming languages

Often it is sufficient to use available programs, possibly combining and automating them inside a shell script, in order to solve your problem. However when you need to process data in a very specific way, there might be no program written for your task. In that case you need ot rely on your own programs.

There are dozens of programming languages which all have their advantages and their disadvantages. In the realm of data science (which includes bioinformatics for many problems), there are a bunch of languages which are dominant in the field owing their simplicity to achieve results with minimal learning and programming effort. The two most popular ones are R and Python

### Python vs R
While R was invented as a language for statisticians, Python is a programming language that targets simplicity, readability of code and universal usage. There are Python libraries for nearly anything: [Building](http://flask.pocoo.org "Flask") [websites](https://djangoproject.com "Django"), [scraping](https://scrapy.org "scrapy"),image processing (opencv and Pillow),network analysis(scapy, Twisted),Graphical user interfaces (Kivy, pyqt),language processing(nltk), and of course [all](https://www.numpy.org "Numpy") [kinds](https://www.scipy.org "Scipy") [of](http://pandas.pydata.org "Pandas") [data](https://matplotlib.org "Matplotlib") [analytics](https://pytorch.org "PyTorch").

conclusion: Python ist eine schöne einfache sprache, die richtig gut data science kann (während R leider eine schlechte unschöne Sprache ist die data science kann)

![Python R comparison](https://www.kdnuggets.com/images/google-trends-python-data-science-r-2012-2017.jpg "Python vs R")
