---
layout: page
title: Repeating actions using loops
slug: python-novice-repeating-actions-using-loops
minutes: 15
---

{: .objectives}
> ## Learning Objectives
>
> *   Write for loops to repeat simple calculations.
> *   Build a basic Python script and run it.
> *   Track changes to a loop variable as the loop runs.
> *   Track changes to other variables as they are updated by a for loop.
> *   Write as basic Python script that uses loops

### Using loops to repeat things

Using the tools we've covered till now, repeating a simple statement many times is tedious. The only item
we can currently repeat easily is printing the exact same message multiple times. For example,


{: .python}
~~~
print("I love programming in Python!\n"*10)
~~~

will produce the output:


{: .output}
~~~
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
I love programming in Python!
~~~
Imagine that we wanted to number this list so that we printed:


{: .output}
~~~
1. I love programming in Python!
2. I love programming in Python!
3. I love programming in Python!
4. I love programming in Python!
5. I love programming in Python!
6. I love programming in Python!
7. I love programming in Python!
8. I love programming in Python!
9. I love programming in Python!
10. I love programming in Python!
~~~

Now, the times operator `*` is no longer capable of allowing us to produce this output. Fortunately,
Python provides us with multiple general tools for repetition where we'll simply specify which statements
we want to be repeated and a way to determine how many times to repeat those statements.

To do that, we'll have to teach the computer how to repeat things.

### Shortcomings of the interpreter

Until now, we've been writing everything directly in the Python interpreter.
It's good for testing small bits of code, and you can write any Python using the interpreter - but you wouldn't want to!
Generally you want to have the option of easily running your Python code later, and you don't want to be retyping all the code or copying and pasting it back in to the interpreter. That would be rubbish.

So, much like what we did with Bash, let's take a look at writing a Python script that stores Python in a file that we can run at our leisure.

{: .callout}
> ## Programs or scripts?
>
> The Python Software Foundation refers to Python as a 'programming language',
> But the Python documentation, us, and many others, refer to Python programs
> as 'scripts'. So is Python a scripting language or a programming language?
> The answer is YES.
>
> Traditionally, languages are either interpreted (like Bash) or compiled (like
> C). The former type were scripting languages, and the latter were programming
> languages. But more recently, the lines are beginning to blur.
>
> Python can be both! You can compile Python, but you don't need to.
> In addition, Python can fulfil the role of a scripting language in similar
> ways to Bash, including that it's source code can be run on a multitude
> of supporting platforms without needing to be explicitly compiled. But it
> can also go much further, and it's designed so you can pretty much write
> anything with it.
>
> For that reason, it's considered a programming language, but to add to the
> confusion, we refer to Python programs generally as scripts!

### Our first Python script!

Suppose we want to print each character in the word "lead" on a line of its own.
One way is to use four `print` statements.

Let's write a simple Python program, using our text editor, like we did
with Bash. Let's start our text editor and type the following, saving it in a file called `word_print.py`:


{: .python}
~~~
word = 'lead'
print(word[0])
print(word[1])
print(word[2])
print(word[3])
~~~

Notice the file has `.py` at the end - this is a convention that indicates this
is a Python script.

Once you've saved it, we can run it from the command line like this (from another terminal or shell, so we can see both the program and how it runs at once):


{: .bash}
~~~
$ python word_print.py
~~~

Here we are asking Python to run our Python script. We should see the following:


{: .output}
~~~
l
e
a
d
~~~

But looking at our code again, that's a bad approach for two reasons:

1.  It doesn't scale:
    if we want to print the characters in a string that's hundreds of
    letters long, we'd be better off just typing them in.

2.  It's fragile:
    if we give it a longer string,
    it only prints part of the data,
    and if we give it a shorter one,
    it produces an error because we're asking for characters that don't exist.

We can easily demonstrate the second point by changing our script to the following (just changing the first statement):


{: .python}
~~~
word = 'tin'
print(word[0])
print(word[1])
print(word[2])
print(word[3])
~~~

Running it again...


{: .bash}
~~~
$ python word_print.py
~~~

...gives us the following:


{: .output}
~~~
t
i
n
~~~

{: .error}
~~~
Traceback (most recent call last):
  File "loop_test.py", line 6, in <module>
    print(word[3])
IndexError: string index out of range
~~~

Here's a better approach:


{: .python}
~~~
word = 'lead'
for char in word:
    print(char)
~~~

{: .output}
~~~
l
e
a
d
~~~

This is shorter---certainly shorter than something that prints every character in a hundred-letter string---and
more robust as well:


{: .python}
~~~
word = 'oxygen'
for char in word:
    print(char)
~~~

{: .output}
~~~
o
x
y
g
e
n
~~~

The improved version of code for printing characters uses a [for loop](../../reference.html#for-loop)
to repeat an operation---in this case, printing---once for each thing in a collection.
The general form of a loop is:


{: .python}
~~~
for variable in collection:
    do things with variable
~~~

We can call the [loop variable](../../reference.html#loop-variable) anything we
like, but there must be a colon at the end of the line starting the loop,
and we must indent the body of the loop. Unlike many other languages, there is
no command to end a loop (e.g. end for); what is indented after the for
statement belongs to the loop.

The great thing about Python is that the simplicity of how it handles loops
means we can use the same loop structure for handling other types of data, like
lists instead. So with one minor alteration:


{: .python}
~~~
word = ['oxygen', 'lead', 'tin']
for char in word:
    print(char)
~~~

{: .output}
~~~
oxygen
lead
tin
~~~

Which is really helpful, and means we don't need to remember a different way to do something else for a loop. Although, our variable names are now a bit misleading!

{: .callout}
> ## What's in a name?
>
> Whilst we can name variables anything we like, it's a good idea to ensure the
> name helps you to understand what is going on. Calling our `char` loop
> variable earlier `x` may still be clear in that small script, but if our loop
> were quite large (and/or more complex, with other similarly named variables)
> it would become difficult to understand. So pick something that's meaningful
> to help others, and yourself at a later date, understand what is happening.

### So what's happening in a loop?

Let's look at a different program called `count_vowels.py`, with another loop that repeatedly updates a variable:


{: .python}
~~~
length = 0
for vowel in 'aeiou':
    length = length + 1
print('There are', length, 'vowels')
~~~


{: .bash}
~~~
$ python count_vowels.py
~~~

{: .output}
~~~
There are 5 vowels
~~~

It's worth tracing the execution of this little program step by step.
Since there are five characters in `'aeiou'`,
the statement on line 3 will be executed five times.
The first time around, `length` is zero (the value assigned to it on line 1)
and `vowel` is `'a'`.
The statement adds 1 to the old value of `length`,
producing 1, and updates `length` to refer to that new value.
The next time around,
`vowel` is `'e'` and `length` is 1,
so `length` is updated to be 2.
After three more updates,
`length` is 5;
since there is nothing left in `'aeiou'` for Python to process,
the loop finishes
and the `print` statement on line 4 tells us our final answer.

Note that a loop variable is just a variable that's being used to record progress in a loop.
It still exists after the loop is over,
and we can re-use variables previously defined as loop variables as well:


{: .python}
~~~
length = 0
for vowel in 'aeiou':
    length = length + 1
print('There are', length, 'vowels')
print('The last vowel counted was', vowel)
~~~

{: .output}
~~~
There are 5 vowels
The last vowel counted was u
~~~

Note also that finding the length of a string is such a common operation
that Python actually has a built-in function to do it called `len`, which
we can add to the end of our program:


{: .python}
~~~
print(len('aeiou'))
~~~

{: .output}
~~~
5
~~~

`len` is much faster than any function we could write ourselves,
and much easier to read than a two-line loop;
it will also give us the length of many other things that we haven't met yet,
so we should always use it when we can.

{: .challenge}
> ## From 1 to N
>
> Python has a built-in function called `range` that creates a list of numbers:
> `range(3)` produces `[0, 1, 2]` (thus starting at `0` if only one parameter
> is supplied), whilst `range(2, 5)` produces `[2, 3, 4]`. By default, `range`
> increments the number by one each time.
> If we specify three parameters, e.g. `range(3, 10, 3)`, the third parameter
> indicates how much to increase the number by each time, so we get `[3, 6, 9]`.
> Using `range`,
> write a loop to print the first 3 natural numbers:
>
>
> {: .python}
> ~~~
> 1
> 2
> 3
> ~~~
>
>{: .solution}
> > ## Solution
> > ~~~
> > for i in range(1, 4):
> >    print(i)
> > ~~~

{: .challenge}
> ## Turn a String Into a List
>
> Use a for-loop to convert the string "hello" into a list of letters:
>
>
> {: .python}
> ~~~
> ["h", "e", "l", "l", "o"]
> ~~~
>
> Hint: You can create an empty list like this:
>
>
> {: .python}
> ~~~
> my_list = []
> ~~~
>
>
> {: .solution}
> > ## Solution
> > ~~~
> > my_list = []
> > for char in "hello":
> >     my_list.append(char)
> > print(my_list)
> > ~~~

{: .challenge}
> ## Computing powers with loops
>
> Exponentiation is built into Python:
>
>
> {: .python}
> ~~~
> print(5 ** 3)
>125
> ~~~
>
>Write a loop that calculates the same result as `5 ** 3` using multiplication (and without exponentiation).

{: .challenge}
>## Reverse a string
>
> Write a loop that takes a string, and produces a new string with the characters in reverse order, so `Newton` becomes `notweN`.
