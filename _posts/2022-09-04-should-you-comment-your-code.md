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

Comments are most certainly essential for complex and published code.
And they absolutely do serve a purpose.

But you might not believe that if you spend a few minutes browsing forums
or YouTube videos on the subject.

In recent years, I've seen the argument that well-written, organized code
does not need comments. Some go so far as to suggest that the presence of comments
is actually a code smell, bad practice, or indicator for lack of experience.

That isn't to say that these detractors don't have a point.
I have seen (and written) my fair share of code that is littered with useless 
and distracting comments.

Learning when and where to leave comments in your code, what to comment on,
and how best to summarize your thoughts is a skill that takes time, effort,
and the guidance of a mentor to hone.

As with most advanced skills in this industry, we have a tendency to coin a catchphrase or acronym that captures the essence of hard-learned truths.

- D.R.Y.
- Y.A.G.N.I.
- Crash Early
- Avoid Global Data

All of these phrases capture important lessons, but in this summary we lose that nuance the experience brought to the originator. 
Each has limitations, exceptions, and details left out for brevity and catchiness at the expense clarity.

I suspect the same is true for comment code smells.

## What is a comment?

The core truth that is lost in the argument against comments is this:

> Not all comments are equal.

Every language that I've ever worked in substantially has some directive for leaving comments. C# has a few.

```csharp
// inline comment

/*
 * Block comment
 */

/// <summary>
/// XML comment
/// </summary>
```

And for beginner and intermediate programmers, the phrase "Comments are bad-practice" will lead them to conclude that
any time they hit `/` twice, they're making a mistake.

As I see it, there are three types of comments:

1. What comments,
2. Why comments,
3. and Documentation comments

*What* comments explain what the code around them is doing. They clarify complexity and abstractions.

*Why* comments provide context, often indicating the author's reasoning for implementing the feature in the way they did.

*Documentation* comments show others how to use your code, typically by acknowledging quirks or pitfalls.

## The problem with "What" comments

From my experience, *what* comments are troublesome and when someone says "comments are a code smell" they are refering to *what* comments.

These comments indicate that the code they refer to is too complex or unorganized to be understood without them.

> If you feel the need to leave explanitory comments, your code is likely too complex and/or unclear and is in need of refactoring.

Utimately, the problem is rooted in the complexity of the code -- the comment is just an indicator of that complexity.
Look to refactor your code in ways that reduce complexity and increase clarity rather than filling gaps with comment "putty."

### Extraction and naming

I come from a background in mathematics and code written by mathematicians can often contain long expressions pulled directly from a white paper.

```csharp
var fg = - G * (m1 * m2) / (d * d);
```

That... isn't very easy to understand. 
But do some renaming and hide the details behind a method and you get something much nicer.

```csharp
var forceGravity = InverseSquare(mass1, mass2, distance);

public double InverseSquare(double mass1, double mass2, double distance)
{
    const double GravitationalConstant = ...;
    var proportion = mass1 * mass / (distance * distance);
    return - GravitationalConstant * proportion;
}
```

### Assertions

Often we presuppose some condition has been met when entering a block of code. It can be commonplace to leave a comment indicating that this precondition is assumed.

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

## The role of good comments

The other kinds of comments (*why* and *documentation* comments) are an important part of well-formed code and skipping them is a mistake you'll pay for later.

### Comment for context

Some issues, especially performance issues, can take months or even years to reveal themselves. 
When they do rear their ugly head, it can be difficult to remember why you chose the implementation that you did.

Usually, its the simpliest or quickest solution that gets slotted first. But other times we were aware of a limitation or constraint that led us to the (less performant) solution we chose.

A lot of time, effort, and frustration can be saved by leaving your thoughts along side your less than obvious coding decisions.

### Comment for the future you

Developers spend a lot of time solving difficult problems.
You might spend a day resolving a strange bit of syntax needed to perform a novel task with an external package.Adequately recording your findings will save you time in the future should you need to reproduce these results.

Embedded microblogs in my code that summarize my findings alongside the working example is an invaluable resource when I inevitably need to solve a similar issue again.
The initial time invested in recording the knowledge as it is fresh in my mind is offset by the hours saved months or years later.

### Comment for others

Documentation comments should be included for any publicly callable code, such as library code in a NuGet package. 
Including documentation alongside the code it documents ensures that it remains up to date and easy to find.

XML comments are especially effective for this purpose.
They structure the comments in a machine parsable fashion that can be utilized by plugins, analyzers, or an IDE to serve documentation to your users in a variety of ways.

## Conclusion

"Comments are a code smell" is a well-intentioned attempt to pass important lessons onto a new generation of software developers. But, as with any coinable phrase, the true lesson is obscured behind a convenient facade.

To newer developers this simplification can lead to worse coding practices or an assumption that the comments themselves are the problem in need of solution.
Understanding that "comment" can refer to three distinct concepts that serve different purposes helps uncover the true meaning behind this phrase.

Thanks for coming to my TED Talk.
Hopefully, this has been helpful to you as either a learning or teaching tool.
