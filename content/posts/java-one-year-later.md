---
title: "Java One Year Later"
date: 2020-03-18
draft: false
summary: "A retrospective is overdue!"
---
It’s been a little over a year since I started developing in Java full-time again. A retrospective
is overdue!

# Workplace takeaways

**Communication.** This may not seem like a Java-related skill, but I cannot overstate how many times
stopping to ask questions, even if they seem a bit silly, saved our entire team hours of unnecessary
work. On the converse, I can tell you how frustrated I’ve felt when work was duplicated because of
the lack of communication or, even worse, wrong communication. 😅 Thankfully, I’ve been blessed with
a team that is overall communicative and has been increasingly so in the last few months. Go team!!!
😎

**Convention over configuration is nice, but shared knowledge is prime!** Spring Boot gives
developers a huge break by inserting smart defaults whilst allowing for easy overriding. Couple
this with Spring Data JPA and sensible namespacing and you have yourself a web application setup
that rivals the likes of Ruby on Rails and Django. However, good tooling does not equal superior
code. If your team doesn’t actually understand the APIs and patterns of a
convention-over-configuration setup, it is better in my opinion to aim for a lower level setup,
such as JDBC with Spring Framework 5 or even Servlets, until sufficient training or knowledge
sharing can take place in your team.

# What’s happened in the Java universe

During this time, Java has noticeably evolved to the point that, by next year, I expect many
developers’ boilerplate code to signficantly differ from how it looked last year.

**Java 13 and 14 have rolled out with some notable changes.**
[Records](https://openjdk.java.net/jeps/359) are a preview feature to simplify immutable objects,
eliminating the need for manually creating getters & setters or depending on a 3rd party library to
do so.

```java
public record Customer(
    String name, 
    String address, 
    String phoneNumber) {}
```

[Text blocks](https://openjdk.java.net/jeps/368) are also in preview, Python style:

```java
var explanation = """
Winter fights to stay.
Sweet Spring always wins her way.
Flowers bloomed today!

Source:
https://www.familyfriendpoems.com/collection/spring-haiku-poems/
""";
```

And [switch expressions](https://openjdk.java.net/jeps/361) finally `break` 😁 us away from the 
older, cumbersome syntax. They are also standard and no longer in preview as of Java 14. Here’s an
example of the arrow syntax:

```java
private static double getMaximumDose(String ageGroup) {
    int result = switch (ageGroup) {
        case "infant", "toddler" -> 0.5;
        case "preteen" -> 1.0;
        case "teen", "adult", "senior" -> 2.0;
        default -> -1.0;
    };
    return result;
}
```

**Java 8 is still a big deal**, and is going to continue to be a big deal for quite a while.
[According to Snyk](https://snyk.io/wp-content/uploads/jvm_2020.pdf), 2 in 3 developers still use
Java 8 in 2020, 6 years after its release. Oracle plans to commercially support Java 8 until 2030
[for a price](https://www.infoworld.com/article/3532358/oracle-extends-extended-support-for-java-8.html).

**Java EE is now [Jakarta EE](https://jakarta.ee/)** thanks to Oracle donating its APIs, but
forbidding the use of the `javax` namespace.

[Micronaut](https://micronaut.io/) made its debut as a potential Spring rival in the serverless
space. One very fascinating feature for Micronaut is dependency injection happening
*at compile time* instead of at runtime.

**Kotlin** is now the
[2nd most popular JVM language](https://snyk.io/wp-content/uploads/jvm_2020.pdf).