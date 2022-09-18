---
layout:     post
title:      "Should you comment your code?"
date:       2022-09-04 00:00:00
summary:    
categories: best-practices
thumbnail: comments
tags:
 - code
---

Comments most certainly do serve a purpose in the code that I write.
I, and anyone else that happens to read it, would be worse off if I didn't include them and I suspect the same is true for much of the code that you write.

But you might come to believe that including comments in your code is problematic if you spend a few minutes browsing forums or YouTube videos on the subject.
In recent years, I've seen the argument that well-written, organized code
does not need comments. Some go so far as to suggest that the presence of comments
is actually a code smell, bad practice, or indicator for lack of experience.

I am not here to say that these detractors don't have a point.
I have seen (and written) my fair share of code that is littered with useless and distracting comments.
But as with many ideas in the industry today, the desire to make these ideas marketable has led to confusion and zealotry more than anything else.

Learning when and where to leave comments in your code, what to comment on, and how best to summarize your thoughts is a skill that takes time, effort, and the guidance of a mentor to hone.
As with most advanced skills in this industry, we have a tendency to coin a catchphrase or acronym that captures the essence of hard-learned truths.

- D.R.Y.
- Y.A.G.N.I.
- Crash Early
- Avoid Global Data

All of these phrases capture important lessons, but in this summary we lose that nuance the experience brought to the originator. 
Each has limitations, exceptions, and details left out for brevity and catchiness at the expense of clarity.
Trying to shortcut this complexity with simplified rules-of-thumb can be helpful as a reminder, but only after the initial learning process has given you the skills and tools necessary to leverage them.

I suspect the same is true for claims of comments as code smells.

## What is a comment?

For beginner and intermediate programmers, the phrase "Comments are bad-practice" will lead them to conclude that
any time they type `//`, they're making a mistake.

The core truth that is lost in the argument against comments is this:

> Not all comments are equal.

As I see it, there are three types of comments:

1. What comments,
2. Why comments,
3. and Documentation comments

*What* comments explain what the code around them is doing. They clarify complexity and abstractions.

*Why* comments provide context, often indicating the author's reasoning for implementing the feature in the way they did.

*Documentation* comments show others how to use your code, typically by acknowledging quirks or pitfalls.

## The problem with "What" comments

From my experience, *what* comments can be troublesome.
When someone says "comments are a code smell," I believe these are the kind of comment they are referring to -- comments that explain what the code is doing at a low, technical level.
These comments indicate that the code they refer to is too complex or unorganized to be understood without them.

If you feel the need to leave explanatory comments, your code is likely too complex and/or unclear and may be in need of refactoring.
Ultimately, the problem is rooted in the complexity of the code -- the comment is just an indicator of that complexity.
Look to refactor your code in ways that reduce complexity and increase clarity rather than filling gaps with comment "putty."

Here are a few strategies to achieve this.

### Extraction and naming

I come from a background in mathematics and code written by mathematicians can often contain long expressions pulled directly from a white paper.

```csharp
// Calculate force gravity
var fg = - G * (m1 * m2) / (d * d);
```

That... isn't very easy to understand. 
It lacks context and assumes a level of expertise and comfort with the domain at hand (physics) that a developer reading this code may not have.
But do some renaming and hide the details behind a method and you get something much nicer.

```csharp
var forceGravity = InverseSquare(mass1, mass2, distance);

public double InverseSquare(double mass1, double mass2, double distance)
{
    const double GravitationalConstant = ...;
    var proportion = mass1 * mass2 / (distance * distance);
    return - GravitationalConstant * proportion;
}
```

This still doesn't give the reader all of the details about gravitational force calculations but it does provide some vocabulary they may find useful when looking for answers.
It may also prove useful at reseeding your own memory on the subject.

### Assertions

Often we presuppose some condition has been met when entering a block of code.
It can be commonplace to leave a comment indicating that this precondition is assumed.

```csharp
public void ExampleFunction(int value)
{
    // value should be greater than 0
    ...
}
```

Try replacing those comments with assertions that encode the assumption.

``` csharp
public void ExampleFunction(int value)
{
    Debug.Assert(value > 0)
    ...
}
```

Depending on your language of choice, the exact behavior of assertions may vary and raising an exception may be more appropriate for your application.
But the strategy stays the same.
By enforcing this assumption programmatically, developers in the future will receive an exception when the assertion fails rather than a more esoteric message or invalid results out the other side.

## The role of good comments

The other kinds of comments (*why* and *documentation* comments) are an important part of my process when writing well-formed code and skipping them is a mistake I'll pay for later.
Here are some of the benefits that I find leaving comments can bring to your work.

### Comment for context

Some issues, especially performance issues, can take months or even years to reveal themselves. 
When they do rear their ugly head, it can be difficult to remember why you chose the implementation that you did.

Usually, I go for the simplest or quickest solution first but other times I am aware of a limitation or constraint that led me to the (less performant) solution I chose.
Time passes, my attention is pulled elsewhere, and when I return the code in question, all of the context surrounding any carefully considered decisions has been lost.

A lot of time, effort, and frustration can be saved by leaving your thoughts along side your less than obvious coding decisions.

### Comment for the future you

Developers spend a lot of time solving difficult problems.
You might spend a day resolving a strange bit of syntax needed to perform a novel task with a poorly documented external package.
Adequately recording your findings will save you time in the future should you need to reproduce these results.

Embedded microblogs in my code that summarize my findings alongside the working example has been an invaluable resource when I inevitably face a similar issue again.
The initial time invested in recording the knowledge as it is fresh in my mind is offset by the hours saved months or years later.

### Comment for others

I strive to include documentation comments for any publicly callable code, such as library code in a NuGet package. 
Including documentation alongside the code it documents ensures that it remains up to date and easy to find as I continue to expand and maintain the project.

XML comments are especially effective for this purpose.
They structure the comments in a machine parsable fashion that can be utilized by plugins, analyzers, or an IDE to serve documentation to consumers of your code in a variety of ways.

## Fit your practice to your problem

All too often, developers on the internet speak in prescriptivist terms: You *must* do this and *can't* do that.
One of my goals while writing for this blog is to avoid this whenever I can.

To make it clear, this is how *I* think about comments, the practices *I* use, and how they fit into *my* environment and workflow.

I primarily wear two hats: 

1. maintaining a legacy enterprise resource management system that stretches and sprawls across time, technologies, paradigms, and developers; and
2. writing user interfaces for embedded systems that will live in the field for decades to come.

And I believe that this situation has influenced my understanding of the role of comments fundamentally.
They may even represent the most essential aspect of the code that I write.

You write code in your own environment. If the assumptions about the audience, lifespan, and scope of your code radically differs from mine it may be true for you that all comments are indeed a code smell.

In other words, your mileage may vary.


