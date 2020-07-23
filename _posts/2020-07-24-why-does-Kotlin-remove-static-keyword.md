---
layout: post
title: "Why does Kotlin remove \"static\" keyword ?"
date: 2020-07-24 23:33:32 +0700
categories: Programming
---

In Java, the static keyword is used primarily for memory management. We can apply static keywords to variables, methods, blocks or nested classes. Put simply, a static keyword makes that component part of the class, not an instance of the class.

In Java, static can be:

- Static property: Declare static properties.
- Static method: Declare static methods.
- Static block: Used to initialize static data members.

Kotlin is fully backward compatible with Java, but not everything is preserved in Java. For example, here is the keyword `static`. So, for what reason do Kotlin developers want to remove this powerful keyword?

![img](https://images.viblo.asia/7064bfde-cb0d-44e1-bff6-4d5d3cb5eaf4.png)

## Kotlin is not as restrictive as Java

In Java, everything must be declared inside a class. Even a class must correspond to a .java file. This creates a problem when we want to declare static components, not depending on the instance of the class and can be shared in many places. Because of the need to place static components inside classes, we need to add static keywords to distinguish components at the class level with components at the instance level.

But not so Kotlin, it allows us to declare both the outside of the class as constants, variables and functions outside of the class. Components outside the class will default to static as top-class levels, on par with classes. Therefore, we do not need to declare static components inside classes anymore, so we do not need static keywords.

## Static does not comply with OOP style

Kotlin is an object-oriented programming language (OOP). In OOP, something that is not an object is a big limp. Classes are not objects but only instances of the class are objects. In Java, we have objects that are instance members, and classes with static components. Why is it so when we can only need objects as instances?

![img](https://images.viblo.asia/796d86c3-86df-4170-a2f3-4be1dd9698e3.jpg)

Kotlin proposes that `companion object`nest static classes are in the main classes. When the main class is called for the first time, an instance of this class is created that contains the internal properties and methods that the main class instance can call. The use is almost identical to static in Java but it is obviously a real object rather than a static class member. Developers consider this to be more optimal than Java's static member usage.

In Java, static components are treated very differently than normal object components. This means you cannot do things like implement interfaces or include them on a Map or pass them as parameters to the get method. Meanwhile `companion object`allow for this. That is also an advantage.

If you want the properties, the methods `companion object`are properties, static methods to use with Java, we can add annotations `@JvmStatic`in front to be able to call from Java code as static members.

## Kotlin is a Product-oriented language

Mixing static and "dynamic" components in the same class is not a good idea because it will make the class very long with extremely messy static classes declared on the top day. Using Singleton instead of static is also a much preferred option. However, in Java, declaring a Singleton is very verbose.

Kotlin has provided all the tools for this to make the product development process faster and more efficient. The keywords object, companion object, const are given to solve those complex problems.

With an object, we can quickly declare a Singleton class, all parameters inside it act as static components. With companion objects, we can put static class members in one place. With const, we can declare constants with primitive data types.

## Summary

`Static` is not the keyword to use in modern programming languages. Kotlin is a modern language and aims to develop software products efficiently, quickly, providing many useful features to replace completely and effectively, much more flexibly than `static`in Java. Through this article I hope you understand why Kotlin left one of the most important keywords in Java. If there are any errors, we hope to receive your comments to improve this article.
