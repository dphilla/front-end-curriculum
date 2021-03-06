---
title: Complete-Me
---

## What is a trie?

A `trie` is a data structure in computer science. The word `trie` is derived from the word retrieval (as in re-`trie`-val). So catchy 🤓!

Now there are many types of `tries` and one you will hear a lot about is the `binary search trie`. It's like a linked list the only difference is that each `node` has a left and right `node` attached to it.

The benefits of something like a `trie` is that it makes dealing with large sets of data easier to handle.

## What do you mean by data structure?

I'm not the most organized human being as you've noticed. My wife who is pretty amazing is. She has files stored in folders, she has spread sheets, and she knows where everything typically is.

I've always struggled with that. Organizing my things in way that makes grabbing something or finding something easily has kind of been difficult for me.

Sometimes what I tend to do is put all the things in one place. Just because everything that is important is found in a single place doesn't mean it's optimal. If me and my wife were to have a race on retrieve a specific form, or calendar date I'm coming in last place.

We are currently doing things that are similar inside of our programs. We find something that is important and we store it inside of a data structure. In our case that data-structure is an array. In some cases it also can be saved inside of an object. Now as our data set grows it can become more and more difficult to manage that information.

Array's are great but what you will find is that they can get kind of slow because you are only going in a straight line. You can do somethings to optimize the speed of traversing through the array but what you will notice is that because the data set is not organized optimally it can lead to some problems.

You are essentially sorting through information that can typically be ruled out. It feels like keeping all your important documents in one folder instead of sorting it out into a parts or pieces.


Consider the following gif.

![](https://i.gyazo.com/77f415128f0ea9ae46b80a61a127d9dc.gif)

If we structure our data in a way that it becomes easier to access all of a sudden pulling information out of a large set of data becomes a lot easier and performant. We can rule out data that doesn't have to be sifted through or looked at. I can essentially look at one section for the information I need.

## Let's talk about a prefix trie

Whats really great about a prefix trie is that every parent node will typically have a node for every possible answer. So in our case if we're talking about a prefix trie each node can have up to 26 nodes (each for letter in the alphabet). If I was looking to add names to my trie it would look like this.

           [ root ]
            /     \
           .       .
          /         \
         [a]        [e]
        /   \       /  \
      [m . . n]   [m  . z]
       |     |     |    |
      [y]   [n]   [m]  [r]  
             |     |    |   
            [a]   [a]  [a]  
          /  |  \      
        [b . i . l]
         |   |   |
        [e] [k] [i]
         |   |   |
        [l] [a] [s]
         |       |
        [l]     [a]  
         |
        [e]

In our example here we have two parent nodes. `a` and `e` they have children nodes of `m`, `n`, `m`, `z`. And it continues to trickle down.


## Complete Me

Everybody uses auto complete. In this project you are going to be building a low level version of an auto complete system in javascript.

You will use your TDD repo (created during the config lesson).

### Hint
You can use `console.log` along with `JSON.stringify` to view your trie in your console when running your tests.
`console.log(JSON.stringify(trie, null, 4))`

## Requirements

## Phase 1

The first thing your `trie` should be able to do is take in a word. It should also keep a count of how many words have been inserted.

```
import Trie from "./lib/Trie"

var completion = new Trie()

completion.insert("pizza")

completion.count()
=> 1

completion.insert('apple')

completion.count()
=> 2
```

## Phase 2
Once the words are placed into the `trie` it should be able to offer some suggestions based on a word prefix.

```
completion.suggest("piz")
=> ["pizza"]

completion.insert("pizzeria")

completion.suggest("piz")
=> ["pizza", "pizzeria"]

completion.suggest('a')
=> ["apple"]
```

## Phase 3

Our Trie won't be very useful without a good dataset to populate it. Our computers ship with a special
file containing a list of standard dictionary words.
It lives at `/usr/share/dict/words`

Using the unix utility `wc` (word count), we can see that the file
contains 234371 words:

```
$ cat /usr/share/dict/words | wc -l
=> 234371
```

We are going to load that data set into our trie.

```
import fs from 'fs';

const text = "/usr/share/dict/words"
const dictionary = fs.readFileSync(text).toString().trim().split('\n')

const completion = new Trie()

completion.populate(dictionary)

completion.count()
=> 234371

completion.suggest("piz")
=> ["pize", "pizza", "pizzeria", "pizzicato", "pizzle"]
```

## Phase 4

Next week you will create a Weather App that needs an autocomplete feature.
Package your complete-me trie in a node module so that you can import it into
future projects. (Note: don't publish to npm, you can install your package from github)

## Extensions

### Front Facing Application

See if you can implement a front facing application for your `trie`. The user should be able to submit a word and then receive the suggestions on the dom.

### Delete method

Sometimes auto-completes give suggestions which we never want to see. Add a delete method to your Trie. 

```
completion.suggest("piz")
=> ["pizzeria", "pize", "pizza", "pizzicato", "pizzle", ...]

completion.delete("pizzle");

completion.suggest("piz")
=> ["pizzeria", "pize", "pizza", "pizzicato", ...]
```

## Evaluation Rubric

The project evaluation will have two parts: 
* an in-person live code
  - implement a new method
  - this demonstrates your problem-solving process
* submission of the complete project
  - complete functionality
  - complete testing suite
  - instructors will do code reviews

Complete Me will be assessed with the following rubric:

### 1. Process

* 4: Developer demonstrates a clear understanding of their own problem solving process. Logically breaks down large problems into manageable challenges. Has a thoughtful, refined strategy for approaching complex challenges. Developer clearly articulates thought processes.
* 3: Developer has strategies for approaching complex challenges. Can explain thought process and strategy when prompted. 
* 2: Developer demonstrates a haphazard, trial and error approach, without clear strategy. Developer does not articulate thought process clearly, and cannot explain the problem-solving strategies they utilized.
* 1: Developer does not demonstrate any strategy or process. No meaningful code is written and developer cannot articulate their process.

### 2. Fundamental JavaScript & Style

* 4:  Application demonstrates excellent knowledge of JavaScript syntax, style, and refactoring
* 3:  Application shows strong effort towards organization, content, and refactoring
* 2:  Application runs but the code has long methods, unnecessary or poorly named variables, and needs significant refactoring
* 1:  Application generates syntax error or crashes during execution

### 3. Test-Driven Development & Code Sanitation

* 4: Application is broken into components which are well tested in both isolation and integration using appropriate data. Linting shows 0 complaints.
* 3: Application is well tested but does not balance isolation and integration tests, using only the data necessary to test the functionality. Linting shows five or fewer complaints.
* 2: Application makes some use of tests, but the coverage is insufficient. Linting shows ten or fewer complaints.
* 1: Application does not demonstrate strong use of TDD. Linting shows more than ten complaints.

### 4. Functional Expectations

* 4: Application meets all requirements, and implements one extension properly.
* 3: Application meets all requirements as laid out per the specification.
* 2: Application runs, but does not work properly, or does not meet specifications.
* 1: Application does not run, crashes on start.


## Additional Rescources

Take a moment and read more about Tries:

* [Tries writeup in the DSA Repo](https://github.com/turingschool/data_structures_and_algorithms/tree/master/tries)
* [Tries Wikipedia Article](https://en.wikipedia.org/wiki/Trie)


If you like watching kewl videos:

* [Tries Video](https://www.youtube.com/watch?v=zIjfhVPRZCg)
