---
layout: post
title: Implementation of Binary Search Algorithm in go programming language
categories: [go,data-structure]
description: Implementation of Binary Search Algorithm in go programming language
keywords: development,go,data-structure
---
### Last few days, I am looking into the go programming language.
It seems like to me the C programing language with less complexity.As a very beginner of the language, I tried to implement the basic binary search algorithm in go.

here is the code --

{% highlight go %}

package main
import "fmt"

func BinarySearch(arr [] int, x int) bool{
  
  var lowerBound int = 0
  var higherBound int = len(arr) - 1

  for lowerBound <= higherBound {
    var midPoint = lowerBound + (higherBound - lowerBound) /2
    
    if arr[midPoint] < x {
      lowerBound = midPoint + 1
    }
    
    if arr[midPoint] > x {
      higherBound = midPoint - 1
    }
    
    if arr[midPoint] == x {
      return true
    }

  }
  return false;
}

func main() {
  fmt.Println("BinarySearch")
  arry := [] int{1,2,3,4,5}
  fmt.Println(BinarySearch(arry,4))
}

{% endhighlight %}