{:title "Kobo: Annotation Extractor"
 :layout :post
 :toc false
 :tags  ["python" "kobo" "nltk"]}

Electronic ink (e-ink) displays are composed of an array of tiny micro-capsules embedded in a layer between two electrodes. Each micro-capsule in the array contains both positively charged white particles, and negatively charged black particles. These particles are suspended in a transparent oil. When a voltage is applied across the micro-capsule, the black and white particles separate. With either the black particles or white particles moving to the top of the micro-capsule, creating a white or black dot depending on the charge [[^1]].

<div align="center">
    <img src="/img/e-ink.png" alt="Notifications" style="width:60%">
</div>
<center><b>Caption: </b> Schema of E ink microcapsules from a side view .</center>
<p></p>

The array of micro-capsules together creates the appearance of text or images on the display, that is updated by changing the voltage over the electrodes. The particles in the micro-capsules remain in place even when the power is turned off, meaning that e-ink displays are able to hold their images even when not actively powered.

E-ink displays were developed by a company called the *E Ink Corporation*, founded in 1997 by a group of researchers from the Massachusetts Institute of Technology (MIT). The technology behind e-ink displays was based on a concept called "electrophoretic displays," which had been researched by several scientists in the 1970s and 1980s. *E Ink's* first commercial product was the "E Ink Vizplex", which was introduced in 2004 and used in the first generation of Amazon's Kindle e-reader [[^2]]. Since the release of the Amazon Kindle in 2007 ebook readers have become increasingly prevalent. They confer many advantages for the reader:

 + allowing many books to be carried on a single lightweight device,
 + easy purchasing and downloading of new books,
 + long battery life,
 + ability to waterproof the device,
 + ability to easily highlight text,
 + in built dictionaries to find the meaning of a word.

Having recently switched from reading paper books to reading on an e-reader, it occurred to me that an additional advantage of reading on an electronic device is the data that is captured whilst reading. This project aims to make use of some of that data generated.

## Manjushri Kobo
This project is named after Manjushri a bodhisattva in Mahayana Buddhism associated with wisdom and learning. He is often depicted holding a sword and a book, symbolising the cutting of ignorance and the attainment of knowledge. Manjushri is considered to be the embodiment of the wisdom of all buddhas, and is often invoked in tantric practices for the attainment of higher wisdom and understanding. He is also one of the most revered and important figures in Tibetan Buddhism [[^3]].

<div align="center">
    <img src="/img/manjushri.jpg" alt="Notifications" style="width:30%">
</div>
    <center><b>Caption: </b> Manjushri Thangka.</center>
<p></p>

Manjushri is an appropriate name for this project that aims to make better use of annotations made on a Kobo, to aid learning. The objective is to extract multi-word annotations created on the Kobo Clara HD outputting a file of quotations, and for single words a vocabulary list with definitions that can be learned through Anki [[^4]].


## Overview
The Github repository for the project is located here: [manjushri_kobo](https://github.com/williamgrimes/manjushri_kobo). At a high level the project is structured as follows, where main is the entry point for the project.

<pre style="line-height:120%">
  <code>
    .
    ├── core
    │   ├── argparser.py
    │   ├── database.py
    │   ├── logs.py
    │   ├── quotes.py
    │   └── words.py
    ├── logs
    │   └── manjushri_kobo_<date>.log
    ├── main.py
    ├── README.md
    ├── requirements.txt
    ├── run_manjushri_kobo.sh
    └── sql
        ├── books_read.sql
        └── extract_annotations.sql
  </code>
</pre>

The `argparser.py` module allows for passing arguments from the command line for example the location of the kobo `.sqlite` database, which is connected via a context manager in `database.py`. Logging is setup in the `logs.py` module.

A SQL query is run against the kobo database to extract all highlights made, which are split based on a `max_word_len` parameter into "quotes" and "words". Quotes are then extracted to an org-file in `quotes.py`. Finally words are cleaned and definitions found in `words.py` before being written to `.csv`.

## Python 3.11
For this project I took the opportunity to try Python 3.11. This latest Python release includes significant performance increases being between 10-60% faster than Python 3.10 due to updates to CPython [[^5]]. In addition to faster code execution, Python 3.11 brings:

 + a faster start-up time,
 + more informative error tracebacks,
 + task and exception groups that simplify working with asynchronous code,
 + native support for working with TOML configuration files,
 + and, several new static typing support features [[^6]].

The most immediately obvious and welcome change is in more refined and specific error tracebacks introduced in PEP 657 [[^7]]. In the example below the traceback shows the exact expression causing the error, instead of just the line in previous versions.

```python
Traceback (most recent call last):
  File "distance.py", line 11, in <module>
    print(manhattan_distance(p1, p2))
          ^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "distance.py", line 6, in manhattan_distance
    return abs(point_1.x - point_2.x) + abs(point_1.y - point_2.y)
                           ^^^^^^^^^
AttributeError: 'NoneType' object has no attribute 'x'
```

## Quotes and Org-mode
Org-mode is an open-source, plain-text outlining and note-taking tool for the Emacs text editor. It is built on top of the org-mode file format, which is a simple, plain-text format for organising notes, lists, and other information [[^8]]. Org-mode provides a wide range of features for managing and organising information, including:

 + **Outlining**: org-mode allows you to create nested, hierarchical outlines of your notes and information.
 + **Todo Lists**: You can easily create and manage to-do lists, with support for deadlines, priorities, and tags.
 + **Timestamps and Dates**: org-mode allows you to assign timestamps and dates to your notes, making it easy to track when things were done or when they are due.
 + **Tags and Properties**: org-mode allows you to assign tags and properties to your notes, making it easy to organise and search for specific information.
 + **Hyperlinks** and Cross-referencing: org-mode supports hyperlinks and cross-referencing, allowing you to easily link to other notes, files, and websites.
 + **Document export**: org-mode allows you to export your notes and outlines to a variety of formats, including HTML, LaTeX, and PDF.
 + **Customisable**: org-mode is highly customizable and extensible, with a wide range of built-in commands and functions, as well as support for user-defined macros and scripts.

In the `core/quotes.py` module I extract my annotations longer than 2 words to an org file called `book-annotations.org`. I particularly like this since org-mode provides a hierarchical approach making it easy to fold and unfold sections of the document.

<div align="center">
    <img src="/img/book-annotations.png" alt="Book Annotations" style="width:100%">
</div>
<center><b>Caption: </b> Screenshot of extracted quotes in org-mode.</center>
<p></p>


## Words, Natural Language Toolkit (NLTK), and Anki
For the task of looking up word definitions I tried using the Kobo proprietary Oxford Dictionary of English, but could not determine a way to query this through Python. So I then explored some python libraries for the task, namely:

 + [PyDictionary](https://pypi.org/project/PyDictionary/), and,
 + [WiktionaryParser](https://github.com/Suyash458/WiktionaryParser).

I decided not to use these since many words could not be found, and I wanted to avoid the dependency of an external request. After some experimentation WordNet from the NLTK [[^9]] library gave the most succinct and reliable definitions.

The NLTK is an open-source library for natural language processing (NLP) in Python. NLTK provides a wide range of tools and resources for working with human language data, including: tokenization, part-of-speech tagging, parsing, named entity recognition (NER), sentiment analysis, text classification, stemming, and lemmatization.

WordNet is a lexical database for the English language that is included with the NLTK in Python. The WordNet lexical database groups words into sets of synonyms (synsets) and provides a hierarchy of concepts (taxonomy) to organize the synsets[[^10]]. The NLTK library provides several functions for interacting with the WordNet database, such as looking up synonyms, antonyms, and definitions of words.

In the `core/words.py` module I use NLTK to clean words by:

1. removing whitespace,
2. removing punctuation,
3. converting words to lower case, and
4. lemmatizing them.

Then I use WordNet to lookup definitions, part of speech, and examples. These results are marked up with HTML tags and written to a csv file that can later be imported into Anki, for example a result in the csv file looks like this:

``` html
<h1>Portentous</h1>,"
--------------------<large> 1 </large>--------------------
<em><b>
Of momentous or ominous significance; - herman melville</b> - (Adjective Satellite)</em><small><u>

Examples:</u>
<em>""Such a portentous...monster raised all my curiosity""</em>
<em>""A prodigious vision""</em>
</small>

--------------------<large> 2 </large>--------------------
<em><b>
Ominously prophetic</b> - (Adjective Satellite)</em>

--------------------<large> 3 </large>--------------------
<em><b>
Puffed up with vanity; ; ; ; - newsweek</b> - (Adjective Satellite)</em><small><u>

Examples:</u>
<em>""A grandiloquent and boastful manner""</em>
<em>""Overblown oratory""</em>
<em>""A pompous speech""</em>
<em>""Pseudo-scientific gobbledygook and pontifical hooey""</em>
</small>
-------------------------------------------"
```

This csv file can be imported into the Anki flashcards program to have a tool for memorising new vocabulary.

<div align="center">
    <img src="/img/anki-import.png" alt="Anki Import" style="width:100%">
</div>
<center><b>Caption: </b> Importing csv file to Anki deck "English Vocabulary".</center>
<p></p>

After importing the csv to an existing or newly created deck the words can be studied.

<div align="center">
    <img src="/img/anki-portentous.png" alt="Anki Study" style="width:100%">
</div>
<center><b>Caption: </b> Viewing an Anki card.</center>
<p></p>

## Summary
This short project I hope will be useful to get more value from reading on the Kobo, assisting in learning new vocabulary, and providing a reference library of quotes from books read. As e-ink displays slowly eat up the market I imagine more tools will become available for this, but I think using free and open source projects like Anki, and Org mode makes the outputs more generally useful.

In the future I might extend this project to include some reading statistics in the output logs. For example it would be interesting to log the books read, time spent reading broken down by month, fastest books read, words read per day, etcetera. The project could also be set to run directly when connected by setting a udev rule to launch the `run_manjushri_kobo.sh` bash script.

## References
[^1]: [Wikimedia: Electronic paper - Side view of Electrophoretic display](https://upload.wikimedia.org/wikipedia/commons/3/3a/Electronic_paper_%28Side_view_of_Electrophoretic_display%29_in_svg.svg)
[^2]: [Wikipedia: E Ink](https://en.wikipedia.org/wiki/E_Ink)
[^3]: [Wikipedia: Manjushri](https://en.wikipedia.org/wiki/Manjushri)
[^4]: [Anki](https://apps.ankiweb.net/)
[^5]: [Python Documentation: What’s New In Python 3.11](https://docs.python.org/3.11/whatsnew/3.11.html)
[^6]: [RealPython: Python 3.11 New Features](https://realpython.com/python311-new-features/#so-should-you-upgrade-to-python-311)
[^7]: [PEP 657 – Include Fine Grained Error Locations in Tracebacks](https://peps.python.org/pep-0657/)
[^8]: [Org-mode](https://orgmode.org/)
[^9]: [NLTK](https://www.nltk.org/)
[^10]: [Wordnet](https://wordnet.princeton.edu/)

