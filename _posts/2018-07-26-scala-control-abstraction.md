---
layout: post
title: Scala Control Abstraction
excerpt: Scala Control Abstraction
keywords: scala, functional programming, control structure, repeat until, custom, by-name
---
> পড়তে সময় লাগবে ১০ মিনিট

`Scala` তে খুব বেশি `built-in control structure` নেই, কারণ আমরা খুব সহজেই নিজস্ব `control structure` তৈরি 
করতে পারি। এখানে আমরা তেমন একটি `control structure`, `repeat-until` লুপ তৈরি করব। 

আমরা আমাদের `repeat-until` তৈরি করব ধাপে ধাপে, এবং সেইসাথে `scala` এর কিছু `feature` এর সাথেও পরিচিত হব। 
আমাদের `implementation` শেষ হবার পর আমরা নিচের মত করে কোড লিখতে পারব। 

```scala
var i = 0
repeat {
  println("Hello, world!")
  i = i + 1
} until (i < 10)
```

উপরের কোড দেখে আপনাদের কি মনে হচ্ছে না যে `repeat-until` `scala` তে `built-in`? 

চলুন দেখি কিভাবে আমরা এই `control structure` টি `implement` করতে পারি।  

###  প্রথম ধাপঃ repeatN
প্রথম ধাপে আমরা `implement` করব `repeatN` ফাংশান। চলুন দেখি `repeatN` এর টাইপ সিগনেচার।

```scala
def repeatN(f: () => Unit, n: Int): Unit = ??? 
```

টাইপ সিগনেচার দেখে আমরা বুঝতে পারছি যে `repeatN` হল এমন একটি ফাংশন যেটা ২টি `parameter` নেয়, একটা
কোড ব্লক `f` (`parameter` ও `return value` ছাড়া ফাংশন) ও একটা `integer n`, এবং `repeatN` ঐ কোড ব্লকটিকে `n` সংখ্যক বার `execute` করে। `Implement` করার পরে 
আমরা `repeatN` কে নিচের মত করে ব্যবহার করতে পারব।  

```scala
repeatN(() => {
    println("Hello, world!")
  }, 3)
```

উপরের কোড টি তিন বার `Hello, world!` প্রিন্ট করবে। চলুন দেখি `repeatN` এর `implementation`:

```scala
def repeatN(f: () => Unit, n: Int): Unit = {
  if (n > 0) {
    f()
    repeatN(f, n - 1)
  }
}
```

এখানে `repeatN` একটি [higher order function](https://docs.scala-lang.org/tour/higher-order-functions.html), 
যার প্রথম `parameter` একটি `function` (যা কোন `parameter` নেয় না এবং কোন কিছু
`return` ও করে না) ।  যখন আমরা `f`কে  `call` করি, শুধুমাত্র `f` এর `body execute` হয়। 


### দ্বিতীয় ধাপঃ better repeatN
`repeatN` এর একটা জিনিস আমার পছন্দ হয়নি, তা হলঃ

```scala
() => {
  println("Hello, world!")
}
```

ভাল হত যদি আমরা প্রথমের `() =>` অংশটুকু বাদ দিতে পারতাম (এটা দিয়ে বুঝানো হচ্ছে যে এই কোড ব্লকটি কোন `parameter` নেয় না), 
এবং নিচের মত করে ব্যবহার করতে পারতাম।

```scala
repeatN({
  println("Hello, world!")
}, 3)
```

`Scala` তে [by-name parameters](https://docs.scala-lang.org/tour/by-name-parameters.html) ব্যবহার করে আমরা সেটা করতে পারি। 
`by-name parameter` তৈরি করার জন্য আমরা `parameter` টাইপকে `() =>` এর পরিবর্তে শুধু `=>` দিয়ে পরিবর্তন করব। নিচের মতঃ

```scala
def repeatN(f: => Unit, n: Int): Unit = ???
```

চলুন দেখি নতুন `repeatN` কিভাবে `implement` করা যায়।

```scala 
def repeatN(f: => Unit, n: Int): Unit = {
  if (n > 0) {
    f
    repeatN(f, n - 1)
  }
}
```


### তৃতীয় ধাপঃ কন্ডিশন সহ repeat  
এই ধাপে আমরা `implement` করব `repeatC` - যেটাকে আমরা নিচের মত করে ব্যবহার করতে পারি।  

```scala
var i = 0
repeatC {
  println("Hello, repeat with condition")
  i = i + 1
} (i < 5)
```

`repeatC` এবং `repeat-until` এর মধ্যে একমাত্র পার্থক্য হল, `repeatC` তে `until` `keyword` টা নেই (যার কারণে এর implementation 
কিছুটা সহজ)। চলুন দেখে নেওয়া যাক `repeatC` এর `implementation`। 

```scala
def repeatC(b: => Unit)(c: => Boolean): Unit = {
  b
  if (c) repeatC(b)(c)
}
```

এখানে দুটি বিষয় লক্ষণীয়। 
* `repeatC` একটি [recursive function](https://alvinalexander.com/scala/scala-recursion-examples-recursive-programming)
* `parameter` গুলি দুটি `group` এ নেয়া হয়েছে, যাতে আমরা `,` ব্যবহার না করে `()` দিয়ে `parameter` গুলোকে আলাদা করতে পারি।  

### চতুর্থ ধাপঃ until সহ প্রথম প্রচেষ্টা 

`until keyword` ছাড়া `repeat`, `fluent` শোনায় না, তাই আমরা এবার `until keyword implement` করার চেষ্টা করব।  

```scala
def until(f: => Boolean): Boolean = f

var i = 0
repeatC {
  println("Hello, repeat until (almost)")
  i = i + 1
} (until (i < 5))
```
এখানে `until` তেমন কিছুই করছে না, শুধুমাত্র যে `condition` `parameter` হিসাবে পাচ্ছে সেটাকেই `execute` করছে। 
এবং আমরা এখানে আমাদের আগের `repeatC` ফাংশানই ব্যবহার করতে পারছি। 

এখানে যে জিনিসটা আমার পছন্দ হচ্ছে না তা হল, `until` অংশটুকু `parantheses` এর ভিতরে। 
যদি আমরা `(until (x < 4))` এর পরিবর্তে `until (x < 4)` লিখতে পারতাম, তাহলে আমাদের `implementation` এখানেই শেষ হয়ে যেত। কিন্তু 
এখন আপনি সেটা করতে গেলে `compile fail` করবে (কেন বলতে পারবেন?)। 

### পঞ্চম ধাপঃ Anonymous object 

নিচের কোডটুকু খেয়াল করুন। 

```scala
class Foo {
  def bar(f: => Boolean) = f
}
val foo = new Foo()

foo.bar(3 > 2)  // evaluates to true  
foo bar (3 > 2) // evaluates to true  
```

`foo object` এর `bar method` আমরা দুইভাবে `call` করতে পারি, `.` দিয়ে, অথবা স্পেস দিয়ে।  

এখন আমরা যদি আবার আমাদের `repeat-until` এর `general structure` টা খেয়াল করি - 

```
repeat { } until ( )
```  

কাজেই আমরা যদি `(until (x < 4))` এর পরিবর্তে `until (x < 4)` লিখতে চাই, তাহলে আমাদের `repeat` দিয়ে একটা অবজেক্ট তৈরি করতে হবে, 
যার একটা `method` থাকবে `until`, অনেকটা নিচের মত। 

```scala
def foo(body: => Unit) = new {
  def bar(condition: => Boolean): Unit = {
    if (condition) body
  }
}
```

`scala` তে `new {}` দিয়ে আমরা একটি `anonymous object` তৈরি করতে পারি। কাজেই উপরের `foo` যা করছে তা হলঃ 

* `new {}` দিয়ে একটি `object` তৈরি করছে, যার `constructor parameter` এ একটি কোড ব্লক পাঠানো যায়। 
* ঐ `object` টিতে `bar` নামে একটি `method` আছে, যেটা `parameter` হিসাবে আরেকটি কোড ব্লক নেয়। 
* যদি `condition` কোড ব্লক টি `true evaluate` করে, তাহলে `bar` ফাংশান, `body` নামক কোড ব্লকটি (যেটা আমরা `constructor parameter` 
   হিসাবে পাঠিয়েছি) `execute` করবে.           

আমরা নিচের মত করে `foo` এবং `bar` কে ব্যবহার করতে পারব। 

```scala
foo {
  println("Hello, World!")
} bar (2 > 1) // this will print 'Hello, World!' since 2 > 1 evaluates to true
```

### শেষ ধাপঃ repeat until 

উপরের সবগুলি ধাপ বুঝতে পারলে এখন `repeat-until implement` করা আমাদের জন্য খুবই সহজ। নিচে তা দেওয়া হল।  
 
```scala
def repeat(b: => Unit) = new {
  def until(c: => Boolean): Unit = {
    b
    if (c) until(c)
  }
}
```

এবং এখন আমরা আমাদের লক্ষ্য অনুযায়ী নিচের মত করে `repeat-until` ব্যবহার করতে পারব।  

```scala
var i = 0
repeat {
  println("Hello, World!")
  i = i + 1
} until (i < 10)
```

### পরিশিষ্ট

আমরা প্রধানত `scala` এর নিচের `feature` গুলি ব্যবহার করেছি `repeat-until` `implement` করার জন্য। 

* [higher order function](https://docs.scala-lang.org/tour/higher-order-functions.html)
* [by-name parameters](https://docs.scala-lang.org/tour/by-name-parameters.html)
* `parameter group`
* `anonymous object`


`repeat-until` দেখানোর উদ্দেশ্য হল, কিছু `language feature` ব্যবহার করে কিভাবে আমরা সহজেই `built-in control structure` এর মত 
`control structure` তৈরি করতে পারি। এইরকম `control structure`, `api` কে `fluent` করে তুলতে অথবা `DSL implement` করতে কাজে লাগে।

     
