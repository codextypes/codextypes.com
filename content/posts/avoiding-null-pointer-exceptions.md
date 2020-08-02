---
title: "Avoiding Null Pointer Exceptions"
date: 2019-03-10
draft: false
summary: "Those sneaky, sneaky null pointers!"
---
There is a form of driving called “defensive driving”. Defensive drivers anticipate accidents 
and bad drivers. This lowers the chances of getting into accidents. It has saved me from 
several bad accidents.

Similarly, we can avoid the scary `NullPointerException` if we know how to anticipate it. Knowing
how to anticipate it will save us from bad coding accidents.

For example, what is wrong with this `if` check?

```java
if (aString.equals("yes")) { /* do stuff */ }
```

It’s assuming that `aString` has been initialized. If a string is not initialized, it will 
be null! This happens more often than you might expect. It is better to write this:

```java
if ("yes".equals(aString)) { /* do stuff */ } 
```

I edited a POJO recently that was meant to be a deserialized JSON object. The business
requirements said I needed to remove any leading or trailing whitespace. Thankfully, the
`trim()` method can do this for me in a single line! I placed it in the setter like this:

```java
public class Person {
  private String firstName;

  public String getFirstName() { 
      return this.firstName; 
  }

  public void setFirstName(String firstName) { 
    this.firstName = firstName.trim(); 
  }
}
```
Seems innocent enough. 😉

Imagine my frustration when converting a JSON to this object was throwing a 
`com.fasterxml.jackson.databind.JsonMappingException` with a not-so-helpful explanation of 
“N/A”. What was happening?

Apparently, if `firstName` is null in JSON, `setFirstName` was calling `trim()` on a null object!

In conclusion, what I need to do is check to make sure that the String parameter in
`setFirstName` is not null. There’s more than one way to check, but I chose a ternary operator:

```java
public class Person {
  private String firstName;

  public String getFirstName() { 
      return this.firstName; 
  }

  public void setFirstName(String firstName) { 
    this.firstName = (firstName == null) ? null : firstName.trim(); 
  }
}
```