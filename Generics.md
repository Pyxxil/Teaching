# Generics

(Just a small note here: Java isn't my strongest language, I understand C++ much better, so some of the following is not likely to be what would be considered *good* practice in Java but it's the idea that counts anyways, right?)

## Introduction
So, you’re confused on what ‘Generics’ are. Don’t worry, most people are to some extent. It may surprise you, but even I struggled with them at some point (who knew I couldn’t know something? Consider me shocked too).

Generics are kind of straight forward once you understand them, but of course that’s always the biggest hurdle isn’t it? Anyways, let’s take a step back first.

## Method signatures

What is a parameter in regards to a method?
Let’s take this method to figure this out:

```java
public class Equality {
    public boolean equals(String a, String b) {
        // Yes, I am aware this is not how you compare strings
        return a == b;
    }
}
```

In this code, add has two parameters — namely, a and b. These parameters are what help make up what we call the **signature** of a method. A method's signature can be created in many ways, in the number in type of parameters, it's return type, etc.

Java method signatures are built upon the following principles:
 - The method name
 - The methods number and type of parameters

In future, when I talk about a method signature I will refer to it in the following way:

``` methodName_Param1Type_Param2Type_... ```

Where there could be any number of Parameter types, each joined with an underscore. The above ``` equals ``` has the following signature for example:

``` equals_String_String ```

Now, this is all well and good, but the question now becomes -- why is any of this important? And that is an astute point, reader. So let's quickly move on.

Generic's are a way for us to alter a signature without having to actually rewrite the method multiple times, essentially reimplementing the method each time. This would be bad, as it defeats the purpose of the DRY (Dont Repeat Yourself) princple. What if, for example, we also wanted the above method to work with integers? Well, we could do the following:

```java
public class Equality {
    public boolean equals(String a, String b) {
        return a == b;
    }

    public boolean equals(int a, int b) {
        return a == b;
    }
}
```

Well, that's not too bad -- we only realistically added 4 lines. This new method would have the signature ``` equals_Int_Int ```, but outside of that it's essentially no different to the previous definition of equals.

Then we also want to think about if in future we also wanted to be able to check equality of floating point values? Lists? Our own types? Well, now you'd have to add a new method for each of those. And what happens if we at some point decide that we not only want to be able to check equality of int's to int's, but int's to float's, or vice versa?

Do you see why this could become cumbersome? Even with having to only add 4 new lines every time, it can eventually spiral out of control. Not just in the amount of code you now have, but the amount of code you now need to *maintain* if something goes wrong.

## Generics to the Rescue!
What if I told you you could do all of this, without having to rewrite all of that extra code, and still have the same functionality? This is what Generics are. Take the following code:

```java
public class Equality<T> {
    public boolean equals(T a, T b) {
        return a == b;
    }
}
```

This is a generic class. The signature for equals no longer exists. Remember how I said that the method signature consists of the *types* of its parameters? Well, what is type T? The answer to that is -- it depends! Take the following:

```java
public class Main {
    public static void main(String[] args) {
        Equality<Integer> integersEqual = new Equality<>();
        System.out.println(integersEqual.equals(new Integer(1), new Integer(1))); // Out: true
    }
}
```

The signature for ```Equality<Integer>.equals``` is ``` equals_Integer_Integer ```. But wait, we never defined a method called equals that takes two Integer's as parameters! you say. You'd be both correct, and incorrect simultaneously. We never explicitly declared a method with that signature, but the java compiler did. When it saw that you provided a type argument to your Equality class in ``` Equality<Integer> integersEqual... ``` you told the compiler to make that specific class. A class that now replaces every instance of T inside it with Integer, essentially akin to how in a method if you pass an argument you get to see that argument within the method itself.

So, the compiler actually did some programming itself. It made a program that has that signature, which we can then freely call ourselves. We could even do the following:

```java
public class Main {
    public static void main(String[] args) {
        Equality<Integer> integersEqual = new Equality<>();
        System.out.println(integersEqual.equals(new Integer(1), new Integer(1))); // Out: true

        Equality<Double> doublesEqual = new Equality<>();
        System.out.println(doublesEqual.equals(new Double(1), new Double(2))); // Out: true
    }
}
```

And this would have the compiler not only generate the above signature, but one for Doubles as well -- ```equals_Double_Double```.

## Let's get crazy
So, we've seen that this works with a single type parameter. But what if we wanted to compare Integers and Doubles together? Well, let's just try what you'd do if you wanted to add another parameter to a method -- seperate the types with a comma:

```java
public class Equality<T, T1> {
    public boolean equals(T a, T1 b) {
        return a == b;
    }
}
```

If you compile the above you'll see that it indeed compiles just fine. In fact, it only requires some small modifications to our original code:

```java
public class Main {
    public static void main(String[] args) {
        Equality<Integer, Integer> integersEqual = new Equality<>();
        System.out.println(integersEqual.equals(new Integer(1), new Integer(1))); // Out: true

        Equality<Double, Double> doublesEqual = new Equality<>();
        System.out.println(doublesEqual.equals(new Double(1), new Double(2))); // Out: true
    }
}
```

Which is not ideal, but still better than what we would have to do otherwise.

You'll also notice we had to call our second type T1, and the reasoning for this is the same reason we can't have the same paramater names -- they would conflict. While it is allowed for T and T1 to be the same type, it is not allowed for them to have the same name.

So, with this new addendum, we can now compare an Integer and a Double like so:

```java
public class Main {
    public static void main(String[] args) {
        Equality<Integer, Double> integersEqual = new Equality<>();
        System.out.println(integersEqual.equals(new Integer(1), new Double(1))); // Out: false
    }
}
```

Now, obviously the 'false' there is not ideal, but that's due to Java and not the actual implementation here (as in, the point still stands on not having to rewrite the code, despite it giving an incorrect value here it does quite often lead to deduplication of code).

So, that's generics. Mostly. There are other things that you can do, standards you can follow, etc. However, that should be enough to get you started along your journey's.

Good luck with the rest of your learning ;) <3
