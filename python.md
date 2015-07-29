## A Gentle (Pythonic) Introduction to JSON 

Programming languages have lots of ways of representing data called 
*data structures*. These may be very simple and flat (think lists of
items, like your grocery list) or complex and hierarchical (like this
document, with its sections and subsections).

Data structures work well for storing and using data inside a program.
However, sometimes you'd like to send data over the network, or store it
in a file for later. Files and network connections can only handle
streams of information in order. Look at this file: it knows that
it starts with a `#` and then has another `#`, but it doesn't
understand any other relationships among the characters. The document
authors know that there are sections and subsections, but we
had to write them down one character at a time. You're now reading
this document and reconstructing its structure in your head.

Similarly, if you have a data structure in a program that you'd like to 
transmit or store, you need to flatten, or *serialize*, it. In the old days,
you'd invent a file format of your own devising to do this and write the
different bits of your data structure into the file format. But that's a
time-consuming way of doing things and very error prone. 

Most modern languages have a way of automatically serializing data structures, 
and the one used by JavaScript took off in a big way, probably because it is 
very simple to understand and use. Conveniently in your case, it's also very 
similar to the way things are done natively in Python. This format is called 
JavaScript Object Notation or [JSON] for short.

You really only need to know about two types of structure to understand JSON. 
In Python parlance these are [lists] and [dictionaries], and they are both 
built in to the language itself. The same is true of other programming 
languages, like Ruby, Perl, PHP, Java and (of course) JavaScript.

### Lists

A list is a container into which you can put other things, knowing that their 
order will be preserved. For example if I wrote:

```python
numbers = [1, 2, 10]
```

I would create a list named `numbers` that contains the integers 1, 2 and 10 
in that order. Python will never re-arrange a list; you can guarantee the 
order stays the same unless you manipulate it yourself.

You can pretty much have anything you like in a list. For example this

```python
things = [1, "dog", 4.5]
```

creates a list named `things` that contains the integer `1`, the string `dog` 
and the real number `4.5`. 

### Dictionaries

The next thing you need to know about is a dictionary. A dictionary makes an 
association between a *key* and a *value*. It's like a mini-database where you 
can put stuff in, give it a unique identifier, and then use that identifier 
later to retrieve it. For example, a dictionary called `ages` containing 
people's ages might look like:

```python
ages = { "Anne" : 34, "Bob" : 29, "Alex" : 15 }
```

If you want you can make this a bit more readable by using multiple lines:

```python
ages = {
  "Anne" : 34,
  "Bob" : 29,
  "Alex" : 15 
}
```

This dictionary contains three entries, one with the key `Anne` and the value 
34, one with the key `Bob` and the value 29, and a third with the key `Alex` 
and the value 15.

So if you then write:

```
print(ages['Anne'])
```

you'll get back the value `34` (an integer). 

### Composing Lists and Dictionaries

To make things a bit more interesting (and expressive) you can put lists and 
dictionaries inside one another. So you could have a list containing 
dictionaries, or a dictionary where each value is a list and so on. 

This turns out to be a fairly generic way of flattening complex data 
structures, and it's exactly what JSON is based on. JSON actually uses a 
notation that's very similar (I think perhaps even identical) to the way that 
Python displays lists and dictionaries, so if you're familiar with one you can 
read the other. 

So let's imagine I want to represent a *person*. I can create a dictionary 
with specific keys and values. Something like...

```python
person1 = { 
  "name": "Anne",
  "age": 34, 
  "shoesize": 6
}
```

and maybe a second person:

```python
person2 = { 
  "name": "Bob",
  "age": 29, 
  "shoesize": 11
}
```

I could now put these two people into a list...

```python
people = [ person1, person2 ]
```

### JSON

What might the list `people` look like if I wrote it out in long hand? It 
would contain two dictionaries, `person1` and `person2`, and each of those 
would have three keys called `name`, `age` and `shoesize` associated with 
their respective values. If I wrote the whole thing out longhand in Python 
notation, it would look like this:

```python
[
  { 
    "name": "Anne",
    "age": 34,
    "shoesize": 6
  },
  {
    "name": "Bob",
    "age": 29,
    "shoesize": 11
  }
]
```

And that conveniently happens to be JSON notation too. That’s all JSON really 
is: a convenient way of describing data structures as combinations of 
(what in Python we would call) dictionaries and lists. This lets us save them 
into files or transmit them over communications links (e.g. over the web or 
between applications). It also lets users on the other end *deserialize* them,
turning them back into their original data structures for use in programs,
just like you rederived the conceptual structure of this document from its
flat representation.

Using JSON saves everyone the trouble of devising their own file formats,
and lets us all share (and test) tools for reading and writing JSON. Many
programming languages have good tools for manipulating JSON. As a result,
and because it's a format suitable for sending across the internet, it's
become the ubiquitous format for web data. (For an example, see the
documentation for the
[Twitter API](https://dev.twitter.com/rest/reference/get/statuses/mentions_timeline).)
Web application writers can use their preferred language to write requested
data into JSON, send it across the network, and trust that you will be able to
reconstruct it in your preferred language.

[lists]: https://docs.python.org/2/tutorial/datastructures.html#more-on-lists
[dictionaries]: https://docs.python.org/2/tutorial/datastructures.html#dictionaries
[JSON]: https://en.wikipedia.org/wiki/JSON
