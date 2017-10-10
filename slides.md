---
title: 'Class 7: Chapter 13: Case Study: data structure'
separator: '\-\-\-\-\-'
verticalSeparator: '\+\+\+\+\+'
theme: 'moon'
revealOptions:
    transition: 'fade'
---

### ITSE-1402 Intermediate Python
<span style="font-family:Helvetica Neue; font-weight:bold; color:#e49436">Class 7: Chapter 13: Case Study: data structure</span>
<br /><br />
##### [https://z3r0.tech/slides-7](https://z3r0.tech/slides-7)

-----

##### Chapter 13: Case Study: data structure

+++++

[https://z3r0.tech/1402-chap13](https://z3r0.tech/1402-chap13)

+++++

#### Testing Knowledge!

- What are two ways to create a list?
- What data types can a list contain?
- Do all data types in a list have to be the same?
- In a two-dimensional list named myList, how do I access the second entry in the third row?
- What is x when defined as so: x = myList.sort()?
- What is an alias and what effect does it have on a list?
- How would I remove the last item in a list and save it in variable y?
- What is the difference between the sort method and the sorted function?

+++++

##### Case study: data structure

+++++

##### 13.1 Word frequency analysis

+++++

```python
#!/usr/bin/env python3

# Exercise 13.1
#
# 1. Write a program that reads a file, breaks each line into words, strips
# whitespace and punctuation from the words, and converts them to lowercase.
#
# Hint: The string module provides a string named whitespace, which contains 
# space, tab, newline, etc., and "punctuation which contains the punctuation
# characters. Let's see if we can make Python swear:
#
# >>> import string
# >>> string.punctuation
# '!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~'
#
# Also, you might consider using the string methods strip, replace and translate.
```

+++++

```python
#!/usr/bin/env python3

# Exercise 13.2
#
# 1. Go to Project Gutenberg (http://gutenberg.org) and download your favorite
# out-of-copyright book in plain text format. Modify your program from the
# previous exercise to read the book you downloaded, skip over the header
# information at the beginning of the file, and process the rest of the words 
# as before. 
#
# Then modify the program to count the total number of words in the book, and 
# the number of times each word is used.
# 
# Print the number of different words used in the book. Compare different books 
# by different authors, written in different eras. Which author uses the most 
# extensive vocabulary?
```

+++++

```python
#!/usr/bin/env python3

# Exercise 13.3
#
# 1. Modify the program from the previous exercise to print the 20 most 
# frequently used words in the book.
```

+++++

```python
#!/usr/bin/env python3

# Exercise 13.4
#
# 1. Modify the previous program to read a word list (see "Reading Word Lists") 
# and then print all the words in the book that are not in the word list. 
# How many of them are typos? How many of them are common words that should be 
# in the word list, and how many of them are really obscure?
```

+++++

##### 13.2 Random Numbers

+++++

Most computers are deterministic and provid the same outputs for the same inputs everytime. This can be undesirable in some cases where you would want a unpredicable output. A good example of this is with gaming. 

+++++

Truly nondeterministic is hard to accomplish, but we can make it seem so pretty easily using the random model (that is actually more of a psudorandom module.

+++++

The function random returns a random float between 0.0 and 1.0 (including 0.0 but not 1.0).

```python
import random
for i in range(10):
    x = random.random()
    print(x)
# Example Output:
# 0.7198071255818801
# 0.5938534709819878
# 0.3569282483020323
# 0.902230923916121
# 0.4779205640671651
# 0.38543858569616263
# 0.31952247933914135
# 0.10524277242134572
# 0.8906385919234846
# 0.4154703646191147
```
+++++

The function randint takes parameters low and high and returns an integer between low and high (including both).

```python
random.randint(5, 10)
# 5
random.randint(5, 10)
# 9
```

+++++

To choose an element from a sequence at random, you can use choice:

```python
t = [1, 2, 3]
random.choice(t)
# 2
random.choice(t)
# 3
```

+++++

```python
#!/usr/bin/env python3

# Exercise 13.5
#
# 1. Write a function named choose_from_hist that takes a histogram as defined
# in "Dictionary as a Collection of Counters" and returns a random value from 
# the histogram, "chosen with probability in proportion to frequency. For 
# example, for this histogram:
#
# >>> t = ['a', 'a', 'b']
# >>> hist = histogram(t)
# >>> hist
# {'a': 2, 'b': 1}
# 
# Your function should return 'a' with probability 2/3 and 'b' with probability 
# 1/3.
```

+++++

##### 13.3 Word histogram

Here is a program that reads a file and builds a histogram of the words in the file:

```python
import string
def process_file(filename):
    hist = dict()
    fp = open(filename)
    for line in fp:
        process_line(line, hist)
    return hist
    
def process_line(line, hist):
    line = line.replace('-', ' ')
    for word in line.split():
        word = word.strip(string.punctuation + string.whitespace)
        word = word.lower()
        hist[word] = hist.get(word, 0) + 1

hist = process_file('emma.txt')
```

Note:
This program reads emma.txt, which contains the text of Emma by Jane Austen.
process_file loops through the lines of the file, passing them one at a time to
process_line. The histogram hist is being used as an accumulator.
process_line uses the string method replace to replace hyphens with spaces before using
split to break the line into a list of strings. It traverses the list of words and uses strip
and lower to remove punctuation and convert to lower case. (It is a shorthand to say that
strings are “converted”; remember that strings are immutable, so methods like strip and
lower return new strings.)
Finally, process_line updates the histogram by creating a new item or incrementing an
existing one.

+++++

To count the total number of words in the file, we can add up the frequencies in the histogram:

```python
def total_words(hist):
    return sum(hist.values())
```    
    
+++++

The number of different words is just the number of items in the dictionary:

```python
def different_words(hist):
    return len(hist)
```

+++++

##### 13.4 Most common words

+++++

To find the most common words, we can make a list of tuples, where each tuple contains a word and its frequency, and sort it.

+++++

The following function takes a histogram and returns a list of word-frequency tuples:

```python
def most_common(hist):
    t = []
    for key, value in hist.items():
        t.append((value, key))
        t.sort(reverse=True)
    return t
```

Note:
In each tuple, the frequency appears first, so the resulting list is sorted by frequency. 

+++++

Here is a loop that prints the ten most common words:

```python
t = most_common(hist)
print('The most common words are:')
for freq, word in t[:10]:
    print(word, freq, sep='\t')
```

Note:
I use the keyword argument sep to tell print to use a tab character as a “separator”, rather
than a space, so the second column is lined up.
This code can be simplified using the key parameter of the sort function. If you are curious,
you can read about it at https://wiki.python.org/moin/HowTo/Sorting

+++++

##### 13.5 Optional parameters

+++++

We have seen built-in functions and methods that take optional arguments. It is possible to write programmer-defined functions with optional arguments, too.

Here is a function that prints the most common words in a histogram:

```python
def print_most_common(hist, num=10):
    t = most_common(hist)
    print('The most common words are:') 
    for freq, word in t[:num]:
        print(word, freq, sep='\t')
```

Note:
The first parameter is required; the second is optional. The default value of num is 10.

+++++

If you only provide one argument:

```python
print_most_common(hist)
```

num gets the default value. 

If you provide two arguments:

```python
print_most_common(hist, 20)
```

num gets the value of the argument instead. 

Note:
In other words, the optional argument overrides the default value.
If a function has both required and optional parameters, all the required parameters have
to come first, followed by the optional ones.

+++++

##### 13.6 Dictionary subtraction

+++++

Finding the words from the book that are not in the word list from words.txt is a problem
you might recognize as set subtraction.

Note:
that is, we want to find all the words from one set (the words in the book) that are not in the other (the words in the list).

+++++

subtract takes dictionaries d1 and d2 and returns a new dictionary that contains all the keys from d1 that are not in d2.

```python
def subtract(d1, d2):
    res = dict()
    for key in d1:
        if key not in d2:
        res[key] = None
    return res
```

To find the words in the book that are not in words.txt, we can use process_file to build a histogram for words.txt, and then subtract:

```python
words = process_file('words.txt')
diff = subtract(hist, words)
print("Words in the book that aren't in the word list:")
for word in diff:
    print(word, end=' ')
```

+++++

```python
#!/usr/bin/env python3

# Exercise 13.6
#
# 1. Python provides a data structure called set that provides many common set 
# operations. You can read about them in "Sets", or read the documentation at 
# http://docs.python.org/3/library/stdtypes.html#types-set.
#
# Write a program that uses set subtraction to find words in the book that are 
# not in the word list.
```

+++++

##### 13.7 Random words

+++++

To choose a random word from the histogram, the simplest algorithm is to build a list with multiple copies of each word, according to the observed frequency, and then choose from the list:

```python
def random_word(h):
    t = []
    for word, freq in h.items():
        t.extend([word] * freq)
    return random.choice(t)
```

The expression [word] * freq creates a list with freq copies of the string word. 

Note: 
The extend method is similar to append except that the argument is a sequence.
This algorithm works, but it is not very efficient; each time you choose a random word, it
rebuilds the list, which is as big as the original book. An obvious improvement is to build
the list once and then make multiple selections, but the list is still big.

+++++

An alternative is:

1. Use keys to get a list of the words in the book.
2. Build a list that contains the cumulative sum of the word frequencies (see Exercise 10.2). The last item in this list is the total number of words in the book, n.
3. Choose a random number from 1 to n. Use a bisection search (See Exercise 10.10) to find the index where the random number would be inserted in the cumulative sum.
4. Use the index to find the corresponding word in the word list.

+++++

```python
#!/usr/bin/env python3

# Exercise 13.7
#
# 1. Write a program that uses this algorithm to choose a random word from the book.
#
# def random_word(h):
#    t = []
#    for word, freq in h.items():
#        t.extend([word] * freq)
#    return random.choice(t)
```
+++++

13.8 Markov analysis
If you choose words from the book at random, you can get a sense of the vocabulary, but you probably won’t get a sentence:

> this the small regard harriet which knightley's it most things

A series of random words seldom makes sense because there is no relationship between successive words. For example, in a real sentence you would expect an article like “the” to be followed by an adjective or a noun, and probably not a verb or adverb.

+++++

One way to measure these kinds of relationships is Markov analysis, which characterizes, for a given sequence of words, the probability of the words that might come next. 

For example, the song Eric, the Half a Bee begins:

> Half a bee, philosophically,
> Must, ipso facto, half not be.
> But half the bee has got to be
> Vis a vis, its entity. D’you see?
> But can a bee be said to be
> Or not to be an entire bee
> When half the bee is not a bee
> Due to some ancient injury?

In this text, the phrase “half the” is always followed by the word “bee”, but the phrase “the bee” might be followed by either “has” or “is”.

+++++

The result of Markov analysis is a mapping from each prefix (like “half the” and “the bee”) to all possible suffixes (like “has” and “is”).

Given this mapping, you can generate a random text by starting with any prefix and choosing at random from the possible suffixes. Next, you can combine the end of the prefix and the new suffix to form the next prefix, and repeat.

Note:

For example, if you start with the prefix “Half a”, then the next word has to be “bee”,
because the prefix only appears once in the text. The next prefix is “a bee”, so the next
suffix might be “philosophically”, “be” or “due”.
In this example the length of the prefix is always two, but you can do Markov analysis with
any prefix length.

+++++

Homework is 13.8 and extra credit is to find a python2 module, convert it with 2to3, and note the differences between them/if it works in python3 now. EC is 10 points.
