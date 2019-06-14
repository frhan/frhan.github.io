---
layout: post
title: Java 8 Method Reference
categories: [Java,Java8]
description: Java 8 Method Reference
keywords: Development, Java
---

### Java Method References


Sometimes,a lambda expression does nothing but call an existing method.In those cases, it's often clearer to refer to the existing method by name. easy-to-read lambda expressions for methods that already have a name.

```java
public class Person {

    public enum Sex {
        MALE, FEMALE
    }

    String name;
    LocalDate birthday;
    Sex gender;
    String emailAddress;

    public int getAge() {
        // ...
    }
    
    public Calendar getBirthday() {
        return birthday;
    }    

    public static int compareByAge(Person a, Person b) {
        return a.birthday.compareTo(b.birthday);
    }}
```

```java
Person[] rosterAsArray = roster.toArray(new Person[roster.size()]);

class PersonAgeComparator implements Comparator<Person> {
    public int compare(Person a, Person b) {
        return a.getBirthday().compareTo(b.getBirthday());
    }
}
        
Arrays.sort(rosterAsArray, new PersonAgeComparator());
```

```java
Arrays.sort(rosterAsArray,
    (Person a, Person b) -> {
        return a.getBirthday().compareTo(b.getBirthday());
    }
);
```

```java
Arrays.sort(rosterAsArray,
    (a, b) -> Person.compareByAge(a, b)
);
```

Because this lambda expression invokes an existing method, you can use a method reference instead of a lambda expression:

`Arrays.sort(rosterAsArray, Person::compareByAge);`
