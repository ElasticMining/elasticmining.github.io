---
layout: post
title: Pattern Matching in Scala
categories: scala
description: "Pattern Matching is a shining feature in Scala language, which provides additional ability that is more powerful and  beautiful than if statement or switch control structure."
comments: true
tags: ["scala","functional programming","pattern matching"]
image:
  feature:
  credit: 
  creditlink: 
date: 2016-03-21T00:00:00+00:00
author: markyang
---
# Pattern Matching in Scala


Pattern Matching is a shining feature in Scala language, which provides additional ability that is more powerful and  beautiful than `if` statement or `switch` control structure.


I will divide the introduction into four parts and walk through them as follows.

## Traditional Method
By this example and comparing to the traditional if-else solution, we get to know what pattern matching is about.

```scala
def toYesOrNo(choice: Int): String = 
if (choice==1) “yes”
else (choice==2)“no”
else “error”
```

```scala
def toYesOrNo(choice: Int): String = choice match {
 case 1 => "yes"
 case 0 => "no"
 case _ => "error"
 }


// toYesOrNo(1)=>"yes"
// toYesOrNo(0)=>"no"
// toYesOrNo(33)=>"error"
```

`_` means any case, otherwise you can also do the following:

```scala
def toYesOrNo(choice: Int): String = choice match {
 case 1 => "yes"
 case 0 => "no"
 case whaterver => "whaterver "
 }
```


## Type Matching
Other than matching values, you can also match types, as follows:

```scala
def f(x: Any): String = x match {
 case i:Int => "integer: " + i
 case _:Double => "a double"
 case s:String => "I want to say " + s
 }


// f(1) → “integer: 1″Typ
// f(1.0) → “a double”
// f(“hello”) → “I want to say hello”
```


## Functional approach to pattern matching
The following is a recursive solution to Factorial algorithm.

```scala
def fact(n: Int): Int ={
 if (n == 0) 1
 else n * fact(n - 1)
 }
```
What if we implement it by using pattern matching?

```scala
def fact(n: Int): Int = n match {
 case 0 => 1
 case n => n * fact(n - 1)
 }
```
We can even define the range of `n` like this:

```scala
 case n if (n>0)=>n * fact(n - 1)
```



## Pattern Matching and Set
This is a recursive version of sum of collection:

```scala
def length[A](list : List[A]) : Int = {
 if (list.isEmpty) 0
 else 1 + length(list.tail)
 }
```
This is fine. But why not challenging yourself by doing a pattern matching version of it:

```scala
def length[A](list : List[A]) : Int = list match {
 case _ :: tail => 1 + length(tail)
 case Nil => 0
 }
```
Where `Nil` is an empty set.
And `_::tail` is interpreted as “a list with whatever head followed by a tail”. In other words, divide the list into a `list.head` and a `list.tail`.



## Conclusion
Finally, with all tricks just learned, we conclude the post with an example : 

```scala
def parseArgument(arg : String, value: Any) = (arg, value) match {
 case ("-l", lang) => setLanguageTo(lang)
 case ("-o" | "--optim", n : Int) if ((0 < n) && (n <= 5)) => setOptimizationLevelTo(n)
 case ("-o" | "--optim", badLevel) => badOptimizationLevel(badLevel)
 case ("-h" | "--help", null) => displayHelp()
 case bad => badArgument(bad)
}
```
After understanding the Pattern Matching, in next blog post we will combine Pattern Matching with Case Class to see what sparks they will emit.

