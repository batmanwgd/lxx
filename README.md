# LXX

This project is dedicated to find citations of the Septuaginta in the Greek New Testament.

## Background

The Bible, a book that has been translated into [many languages](https://en.wikipedia.org/wiki/Bible_translations),
is maybe the most important book has ever existed. Believers
have evidence that it is God's word, written by
various people being inspired by God himself.

The Bible has many internal references. Many of them
connect the two parts of the Bible: the Old Testament
and the New Testament. The books of the Old Testament are
usually written in Hebrew, while the books of the New Testament
are Greek. A natural question can arise: How can Hebrew
texts be cited in the Greek text?

There are several research projects on this,
and today it seems to be clear that many authors of
the New Testament cite a Greek translation of
the Hebrew text, namely the Septuaginta, that
was widely popular in the first centuries, and still popular
in some Christian churches. Many
Bible translations, however, mostly use only the
Hebrew text as a basis of the Old Testament,
because the importance of the Septuaginta is
not yet widely identified.

## This project

This software project attempts to support finding citations
of the Septuaginta in the New Testament automatically.
The work is based on The SWORD Project.

## The method used

The provided software tool compares all verses
of the Septuaginta with all verses of the Greek New Testament.
The texts are provided by the Sword project
from the modules LXX and SBLGNT.

It is well-known that citations can differ in
some letters sometimes. The current method therefore makes
a major rewrite of each Bible verse before comparison:

1. All accents are removed. (This step is performed
only on the text of SBLGNT.)
2. All letters are converted into lowercase.
3. All words that are shorter than 5 letters are removed.
4. The remaining words are shortened to 5 letters by
removing their last letters.

After these steps an exact match is checked
between two verses, using substrings of whole words,
leaving them in the same consecutive order.

### Example

Genesis 1:27 ("So God created mankind in his own image,
in the image of God he created them; male and female he created them.",
New International Version) appears as **και εποιησεν ο 
θεος τον ανθρωπον κατ εικονα θεου εποιησεν αυτον 
αρσεν και θηλυ εποιησεν αυτους** in the Septuaginta.
This verse is stored in the form "εποιη ανθρω
εικον εποιη αυτον αρσεν εποιη αυτου" internally.

In the New Testament there are two matches of this
verse of the Old Testament. The first occurence
is Matthew 19:4: **ὁ δὲ ἀποκριθεὶς ⸀εἶπεν· Οὐκ
ἀνέγνωτε ὅτι ὁ ⸀κτίσας ἀπʼ ἀρχῆς ἄρσεν καὶ θῆλυ
ἐποίησεν αὐτοὺς**. This is internally rendered
as "αποκρ ειπεν ανεγν κτισα αρσεν εποιη αυτου".

Now Genesis 1:27 is stored as 8 words, and Matthew 19:4
on 7 words, both on 5 letter. The computer finds
then that the 3 last words match, and prints
both verses on the terminal window in this form:
```
Genesis 1:27 (30) seems to be cited in Matthew 19:4 (24757)
```
The numbers in parentheses show where these
verses are placed in the Sword databases.

Note that the software tool ignores matches
under having at least 3 matching words. 

### Problems with the method

* Short verses are ignored.
* Verses that have short words may be ignored
or can be reported unnecessarily when the long
words in them appear in other verses.

Hopefully these problems will be fixed in
a future version of the tool.

## Using the software tool

At the moment the project was tested on
Ubuntu Linux 17.04 but it should work
on many other systems.

### Installation

The following commands
should be entered on command line:
```commandline
sudo apt install libsword-common libsword-dev git cmake build-essentials
git clone https://github.com/kovzol/lxx.git
cmake .
make
```
Then the modules LXX and SBLGNT need to be downloaded from
[The SWORD Project](https://www.crosswire.org/sword/modules/ModDisp.jsp?modType=Bibles)
and follow the steps at the [For Linux](https://www.crosswire.org/sword/docs/moduleinstall.jsp)
section on the website of The SWORD Project.

### Running

Enter the command
```commandline
./lxx
```

### Full output

The full output of a simple run can be found in the file [output.txt](output.txt).
