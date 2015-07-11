# A Gentle (Pythonic) Introduction to JSON 

Programming languages have lots of ways of representing data called 
*data structures*. Very often you want to flatten, or *serialize* these 
data structures so that they can be transmitted over the network or stored 
in a file for later.

In the old days, you'd invent a file format of your own devising to do this 
and write the different bits of your data structure into the file format. 
But that's an expensive way of doing things and very error prone. 

Most modern languages have a way of automatically serialising data structures, 
and the one used by JavaScript took off in a big way, probably because it is 
very simple to understand and use. Conveniently in your case, it's also very 
similar to the way things are done natively in Python. This format is called 
JavaScript Object Notation, or [JSON] for short.

You really only need to know about two types of structure to understand JSON. 
In Python parlance these are [Lists], and [Dictionaries], and they are both 
built in to the language itself. The same is true of other programming 
languages, like Ruby, Perl, PHP, Java and (of course) JavaScript.

A List is a container into which you can put other things, knowing that their 
order will be preserved. For example if I wrote:

```python
numbers = [1, 2, 10]
```

I would create a list containing the integers 1, 2 and 10 in that order. 
Python will never re-arrange a list, you can guarantee the order stays the 
same unless you manipulate it yourself. 

You can have anything you like in a list pretty much, e.g.

```python
things = [1, "dog", 4.5]
```

is a list called *things* containing the integer `1`, the string `dog` and the 
real number `4.5`. 

The next thing you need to know about is a Dictionary. A dictionary makes an 
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

To make things a bit more interesting (and expressive) you can put Lists and 
Dictionaries inside one another. So you could have a List containing 
Dictionaries, or a Dictionary where each value is a List and so on. 

This turns out to be a fairly generic way of flattening complex data 
structures, and it's exactly what JSON is based on. JSON actually uses a 
notation that's very similar (I think perhaps even identical) to the way that 
Python displays Lists and Dictionaries, so if you're familiar with one you can 
read the other. 

So let's imagine I want to represent a *person*. I can create a Dictionary 
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

What might the list `people` look like if I wrote it out in long hand? It 
would contain two Dictionaries (`person1` and `person2`), and each of those 
would have three keys called `name`, `age` and `shoesize` associated with 
sensible values. If I wrote the whole thing out longhand in Python notation, 
it would look like this:

```python
[
  { 
    "name": "Anne",
    "age": 34,
    "shoesize": 6
  },
  {
    "name": 'Bob',
    "age": 29,
    "shoesize": 11
  }
]
```

and that conveniently happens to be JSON notation too. That’s all JSON really is: a convenient way of describing data structures as combinations of 
(what in Python we would call) Dictionaries and Lists so they can be saved 
into files or transmitted over communications links (e.g. over the web or 
between applications).

[Lists]: https://docs.python.org/2/tutorial/datastructures.html#more-on-lists
[Dictionaries]: https://docs.python.org/2/tutorial/datastructures.html#dictionaries
[JSON]: https://en.wikipedia.org/wiki/JSON
