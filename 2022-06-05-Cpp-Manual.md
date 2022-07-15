**Technical Note: From C++1998 to C++2020**

- [Introduction](#introduction)
- [Glossary](#glossary)
- [Motivation](#motivation)
- [Deep principles of the C++ language](#deep-principles-of-the-c---language)
- [Standards for the Language](#standards-for-the-language)
- [C++ from the point of view of the author of that programming Language (B. Stroustrup)](#c---from-the-point-of-view-of-the-author-of-that-programming-language--b-stroustrup-)
- [C++ guarantees](#c---guarantees)
- [Stages of processing C/C++ program](#stages-of-processing-c-c---program)
- [What is impossible in C/C++](#what-is-impossible-in-c-c--)
- [For people new to C++](#for-people-new-to-c--)
- [About C/C++ Preprocessor](#about-c-c---preprocessor)
  * [Include Search Order](#include-search-order)
  * [Include Naming](#include-naming)
  * [Predefined Identifiers and Macros](#predefined-identifiers-and-macros)
- [Language Rules](#language-rules)
  * [About Names Overloading in C/C++](#about-names-overloading-in-c-c--)
  * [Literal constants](#literal-constants)
  * [Prefixes for strings from C++11](#prefixes-for-strings-from-c--11)
  * [Function Call Nuances](#function-call-nuances)
  * [Requirements for C++ expressions](#requirements-for-c---expressions)
  * [Exceptions to the one definition rule](#exceptions-to-the-one-definition-rule)
  * [Basic integer types](#basic-integer-types)
  * [Basic integer types nuances](#basic-integer-types-nuances)
  * [Auto Type Deduction](#auto-type-deduction)
  * [Range based for loop (since C++11)](#range-based-for-loop--since-c--11-)
- [Technical Differences between C and C++](#technical-differences-between-c-and-c--)
- [Memory](#memory)
  * [Memory Types and pointers](#memory-types-and-pointers)
  * [Used Memory for Types and Their Layout](#used-memory-for-types-and-their-layout)
  * [New operator (heap memory allocation)](#new-operator--heap-memory-allocation-)
  * [Placement New](#placement-new)
  * [Pseudo Destructor](#pseudo-destructor)
  * [Aggregates](#aggregates)
  * [Data types with special guarantee in memory layout: POD or Plain Old Datatype (C++03)](#data-types-with-special-guarantee-in-memory-layout--pod-or-plain-old-datatype--c--03-)
  * [Data types with special guarantee in memory layout: Standard Layout (From C++11)](#data-types-with-special-guarantee-in-memory-layout--standard-layout--from-c--11-)
- [Built-in Type Conversion](#built-in-type-conversion)
  * [Prohibited conversions](#prohibited-conversions)
  * [The sequence of type conversions rules in C/C++](#the-sequence-of-type-conversions-rules-in-c-c--)
- [Namespaces](#namespaces)
  * [Basics about Namespaces](#basics-about-namespaces)
  * [Namespace lookup rules](#namespace-lookup-rules)
  * [Examples of using `using`](#examples-of-using--using-)
- [Exceptions](#exceptions)
  * [Basics about Exceptions](#basics-about-exceptions)
  * [Extra about exceptions](#extra-about-exceptions)
- [Overloading](#overloading)
  * [Functions and operator overloading precedence](#functions-and-operator-overloading-precedence)
  * [Template function overloading](#template-function-overloading)
  * [Resolving the overloaded binary operator for x(op)y.](#resolving-the-overloaded-binary-operator-for-x-op-y)
  * [Operators overloading rules in C++](#operators-overloading-rules-in-c--)
- [```typename``` keyword](#---typename----keyword)
- [Class constructor and destructors](#class-constructor-and-destructors)
  * [Logic behind executing constructors](#logic-behind-executing-constructors)
  * [Logic behind executing destructors](#logic-behind-executing-destructors)
  * [Deleting object of incomplete type](#deleting-object-of-incomplete-type)
  * [Generate/Suppress generation of special class members](#generate-suppress-generation-of-special-class-members)
  * [Some class special members (since C++11)](#some-class-special-members--since-c--11-)
- [Initialization](#initialization)
  * [C++ variable initialization](#c---variable-initialization)
  * [std::initializer_list<T>](#std--initializer-list-t-)
  * [Various constants flavors.](#various-constants-flavors)
    + [const (C++03)](#const--c--03-)
    + [constexpr (C++11)](#constexpr--c--11-)
    + [constinit (C++20)](#constinit--c--20-)
    + [consteval (C++20)](#consteval--c--20-)
- [Compute Optimization Relative Information](#compute-optimization-relative-information)
  * [Return Value Optimization](#return-value-optimization)
  * [Inline function call](#inline-function-call)
  * [Allowable reformulations](#allowable-reformulations)
  * [Compiler Implementation relative Questions](#compiler-implementation-relative-questions)
- [Lambda functions](#lambda-functions)
- [Move semantics](#move-semantics)
  * [The first scary thing](#the-first-scary-thing)
  * [The second scary thing](#the-second-scary-thing)
- [Virtual and Polymorphism in C++](#virtual-and-polymorphism-in-c--)
  * [General rules from C++03](#general-rules-from-c--03)
  * [Override (from C++11)](#override--from-c--11-)
  * [Final specification](#final-specification)
  * [Connection of virtual function with default values.](#connection-of-virtual-function-with-default-values)
- [Miscellaneous Features of C++11](#miscellaneous-features-of-c--11)
- [Miscellaneous Features of C++14](#miscellaneous-features-of-c--14)
- [Miscellaneous Features of C++17](#miscellaneous-features-of-c--17)
- [Miscellaneous Features of C++20](#miscellaneous-features-of-c--20)
- [Modules (from C++20)](#modules--from-c--20-)
  * [Single Module Interface File/Module Unit](#single-module-interface-file-module-unit)
  * [Module Interface File With Implementation inside it](#module-interface-file-with-implementation-inside-it)
  * [Module Interface File With Separate Implementation](#module-interface-file-with-separate-implementation)
  * [What you can not define in a module implementation file](#what-you-can-not-define-in-a-module-implementation-file)
  * [Using Modules](#using-modules)
  * [Splitting Modules](#splitting-modules)
- [Templates](#templates)
  * [Template syntax remarks](#template-syntax-remarks)
  * [Variadic templates](#variadic-templates)
  * [Reference Collapsing Rules](#reference-collapsing-rules)
- [Variants of Casting](#variants-of-casting)
- [Concepts (from C++20)](#concepts--from-c--20-)
  * [Define Concepts](#define-concepts)
  * [Use Concepts](#use-concepts)
- [Coroutines (C++20)](#coroutines--c--20-)
- [References](#references)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# Introduction

This is a long post in which we would like to share complete information regarding C and C++ programming languages. That note is less likely can be used as an introduction to the language. On the other hand, it's not a complete book [4]. That note is mainly based on materials from the Reference section and personal experience. We think that note can be helpful for people who won't upgrade their understanding of several language constructions or learn about new features from C++11/14/17/20.

# Glossary

*Upcast.* Cast to the base class.

*Downcast.* Cast to the derived class.

*RValue*. An rvalue evaluates a result that is stored only transiently. Something from which the address cannot be taken (in 99% of cases, these are unnamed temporary variables). And in fact, it can be encoded in the code of generated instructions for the processor. A good counterexample is something that is an rvalue but has the name `this`.

*LValue*. An lvalue evaluates to some persistent value with an address in memory in which you can store something. Informally that is something to the left of the operator equals. Each lvalue is implicitly converted to an rvalue. Normally, an lvalue reference is an alias for another variable


*XValue*. Something that would be destroyed very soon and an object for which it is reasonable to use move semantics to take data via `T&&` notation from C++11.

*Function signature.* The combination of the function name and the parameter list is called the signature of a function.

*Function prototype (function declaration).* A function prototype is a statement that describes a function sufficiently for the compiler to be able to
compile calls to it.

*Template type parameter.* Type placeholder used in class or function template, typically denoted by T.

*Template-type argument.* The type assigned to a type parameter T during instantiation. 

*Function Object.* A function object or functor is an object of a class that overloads the function call operator.
```cpp
class Volume
{
public:
  double operator()(double x, double y, double z) const { 
    return x * y * z; 
  }
};
```

*Pure virtual function.* The purpose of a pure virtual function is to enable the derived class versions of the function to be called polymorphically.
```cpp
class Shape {
public:
   virtual double area() const = 0;
};
 ```

*Abstract class.* A class that contains at least one pure virtual function.

*A shallow copy.* A shallow copy simply copies all members of an object one by one, even if these members are pointers to dynamic memory. 

*A deep copy.* A deep copy copies all dynamic memory referred to by any of its pointer members.

# Motivation

The C/C++ programming language represents a pretty thin abstraction over the underlying hardware. The level below C/C++ is Assembly for your computing device.

Why computing is critical is excellently motivated by prof. Charles E. Leiserson, MIT, in his undergraduate course about Algorithms and Data structures. We can not describe it better as he did. 

If you want to learn about that, please look into his lectures MIT 6.046J / 18.410J Introduction to Algorithms (SMA 5503), Fall 2005, publicly available.

Nowadays, in 2022, for some reason, interpretable programming languages are in fashion. We think that is primarily due to the fast learning curve and secondary because the heavy design of computing science systems goes into the past in the pretty dynamic world in which we are. 

Nevertheless, In some domains, the interpreter is not a choice when actual time matters.  

In general, we think the main problem with interpreters is the following:

- Interpreters provide algorithms that are 50'000 times slower than highly optimized C/C++/ASM code. The interpreter typically parsed the program's text line by line (that represented or in text form or extremely high-level instructions).

- Interpreters do not provide subtle interfaces to work with POSIX API and other OS-dependent APIs.
- During work with an interpreter, you don't have an interface to work your memory.
- The multithreading and thread synchronization implementation is pretty unobvious and may be suboptimal in the interpreter. (E.g., you can look into GIL in Python)
- Garbage Collector brings various limitations into the language - Pointer arithmetic is disallowed in any language with GC
- There are some subtleties with implementing function call (or method call) in some specific hardware. The function calls It's effective.
- Finally, the implementation of an interpreter is very likely just a collection of C/C++ libraries wrapped up into the program that can execute the command and therefore called an interpreter.
- The absence of a compiler makes handling problems in the code to be testable without a compiler. It has pros. - you do not spend time on a compilation, but there are cons. - now, the compiler will not tell you about errors in the code because there is no compiler.

The interpreter is great for prototyping, and sometimes it is enough. But any interpreter, any algorithm in it, can be beaten by C++/ASM implementation. So at least be aware of that.

Some language decisions:

- C++ does not have a universal class Object. It's so because, in C++, we don't need one: generic programming provides statically type safe alternatives in most cases. Also, there is no useful universal class, and in fact, using a universal base class implies the cost.

- Templates are not Generics (from C# or Java). Generics are primarily syntactic sugar for abstract classes. That is, with generics (whether Java or C# generics), You program against precisely defined interfaces and typically pay the cost of virtual function calls and/or dynamic casts to use arguments.

# Deep principles of the C++ language

Principles of language which B.Stroustroup put into the language in 1994 are still current, and the language still follows them [4]:

1. No implicit violation of static type-system.
2. Provide good support for user-defined types similar to built-in types.
3. The locality is good.
4. Zero-Overhead principle:
    
    a. What you don't use - you should not pay for.
    
    b. If something is built-in in the language, it's impossible to write it better by hand.

# Standards for the Language

Both compilers writers and people who use the C++ language as writers should obey the international standard ISO/IEC for the language. C++ Standardization has a long history:

1. C\+\+1998 standard - ISO/IEC 14882-1998
2. C\+\+2003 standard - A "bug fix release" of this standard was issued in 2003
3. C\+\+ 2011 standard - ISO C\+\+ standard (ISO/IEC 14882-2011)
4. C\+\+ 2014 standard - ISO C\+\+ standard (ISO/IEC 14882:2014) - completes C\+\+ 11 and fix various issues in it
5. C\+\+ 2017 standard - ISO C\+\+ standard (ISO/IEC 14882:2017) 
6. С\+\+ 2020 standard - ISO C\+\+ standard (ISO/IEC 14882:2020)

To be honest with you, we don't know how it is possible to write compilers or write programs without the standard of the language.

# C++ from the point of view of the author of that programming Language (B. Stroustrup)
Barge Stroustrup, in 2010, jokingly describes C++ as a language:
1. Support generic programming
2. Hybrid language
3. Multi-paradigm programming Language
4. Buffer Overflows
5. Too Big
6. Object-Oriented-Programming Language
7. Low level
8. Embedded system language
9. Random Collections of features
10. It's C!

# C++ guarantees
Fundamental types of C++ code guarantees:
1. **Basic Guarantee** - no leaks and standard libraries supported.
2. **Strong Guarantee** - whether the operation is completed.

All containers in C++98 provide a fundamental guarantee. And some operations (for example, `std::vector<T>::push_back`) give a Strong Guarantee.

# Stages of processing C/C++ program

1. Processing trigrams.

2. Joining strings through the backslash character.

3. Processing the program code by the preprocessor. The preprocessor can be built into the compiler, or it can be an independent program.

4. Lexical analysis of the program by splitting the program into tokens. An important part is that the compiler always tries to assemble the longest token of characters by processing the text from left to right, even if the result is an unbuildable program.

Tokens can be separated by white spaces. The concept of whitespace includes things like different keyboard spaces and comments at the compiler level.

In C++ (and in most programming languages), the tokens can be one of the following types:

a. Operators

b. Separators

c. Identifiers

d. Keywords

e. Constants

After the lexical analysis program consists of a sequence of tokens.

# What is impossible in C/C++

* *Address individual bits*. Few machines can directly address an individual bit. Even if the machine allows to do it, it is out of the scope of C/C++, to be honest. (Of course - you can operate on bits, but not directly)

* *Define your own operators.* B.Stroustroup said that the possibility had been considered several times, but each time he/they decided that the likely problems outweighed the potential benefits.


# For people new to C++
If you have arrived from another programming language and already understand C++, we would like to enumerate several not complicated things for you. Our vision of course even experiences people should back to basics from time to time.

1. These logical operators `&&` and `||` is called short-circuit evaluation. The bitwise operators `&` and `|,` however, do not short-circuit.

2. The difference between the two pointers is again measured in terms of elements, not in terms of bytes.

3. Every heap memory allocation `new` must be paired with a single `delete`, and every `new[]` must be paired with a single
`delete[]`. Any other sequence of events leads to either undefined behavior or memory leaks.

4. Substrings are always specified using beginning index and length, not beginning and ending indexes. Keep this in mind when migrating from other languages.

5. Never return the address of an automatic, stack-allocated local variable from a function.

6. When a class member function executes, it automatically contains a hidden pointer with the name `this`, which includes the address of the object for which the function was called. 

7. You can only call `const` member functions for' const' objects. You should therefore specify all member
functions that do not change the object for which they are called `const`.

8. Static member functions cannot be `const`. Because a static member function is not associated with any class object, it has no `this` pointer.

9. The primary purpose of operator overloading is to increase the ease of writing and the readability of code that uses your class.

10. The notation for calling the base class constructor is the same as that used for initializing member variables in a constructor.

11. Every derived class constructor calls a base class constructor. If a user-defined derived class constructor
does not explicitly call a base constructor in its initialization list, the default constructor will be called.

12. A table of virtual function pointers is created for each
class that contains virtual functions. The only time you should even debate whether the overhead of a virtual function table pointer is worth it is when you have to manage many objects of the corresponding type.

13. The general form of a pointer to a function definition is as follows: `return_type (*function_pointer_name)(parameter_types);` [4, p.733].

14. Names starting with a double underscore (__) or an underscore followed by an uppercase letter (e.g., _Foo) are reserved by the compiler implementations.

15. C/C++ postfix operators have higher priority than unary operators.
```cpp
*p++; // *(p++)
```

16. C/C++ unary operators have higher priority than binary operators. 

17. Operators "==", "!=" have higher priority than logical connectives.

18. The C++ standard guarantees that the life of a temporary object (if it is **lvalue**) is extended to the life of any reference that refers to it, **including the constant**. 

19. References to rvalue objects (objects whose address cannot be obtained) do not extend the lifetime of temporary objects. Most likely, the compiler won't let you compile. However, the compiler can only detect simple constructions.

20. Create a temporary object, and call a method from this temporary object that will return a reference to itself. The compiler will no longer be able to determine this.
In simple cases, based on this trick, you can capture returned temporary objects by constant reference to reduce the number of copy constructors.

21. In nested statements, an `else` always belongs to the nearest preceding `if`. The potential confusion here is known as the *dangling else problem*.

# About C/C++ Preprocessor

C++ 1998 and C++2003 use the C89 preprocessor, although the C language also has evolved: Tradition C, C89, C95, C99, C11, C17.

Preprocessor macro extensions in C/C++ have the following property. Once an extension replaces a macro call, the macro call search process starts from the beginning of the expanded extension for further replacement.

During this process, macros that are referenced in their own expansion are not re-expanded, and that preprocessor macro extension does not lead to infinite recursion.
`#define sqrt(x) (x<0 ? sqrt(x) : sqrt(-x))`

For C/C++ preprocessor, any undefined identifiers that appear after the conditional directives `#if` and `#elif` are replaced
with the number 0.

## Include Search Order
The original C specification says that the original directory in which the compiled file is located is used to look for a user-defined include file. The reality is that it is necessary to clarify the rules according to the specification of the toolchain used. Or understand the essence of the experiments.

## Include Naming

1. A standard header file whose name begins with the letter ```c``` is equivalent to a standard header file in the C library. (B. Stroustrup, Spec. Edition, p. 487, 16.1.2)
2. For each "C" standard library ```"X.h"``` header file, there is a corresponding C++ standard header file ```<cX>``` in C++.
3. But "X.h" defines function names in the `std` namespace and also **imports those names into the global namespace**.
4. And "cX" defines function names only in the `std` namespace. ([1], 9.2.2, page 247).

## Predefined Identifiers and Macros

`__func__` - In C99, a predefined identifier with the name of the current function. C++11 officially supports that too.

`__LINE__`, `__FILE__` - current line number, and current source file name

`__DATE__`, `__TIME__` - date and time of file translation

`__STDC__ ` - compiler conforms to the C standard

`__VA_ARGS__ ` - only C++ and C99 formally support that. Built-in name that can be used for macros with an arbitrarily number of the argument. When the macro is invoked, all the tokens in its argument list `...`, including any commas, become the variable argument. C++11 officially supports that too.

`__cplusplus` - C++ version

`__STDC_VERERSION__` - version of standart C.

```cpp
#include <stdio.h>
int main()
{
#ifdef __cplusplus
 printf("C++ version %li\n", __cplusplus);
#elif defined(__STDC__)
#if defined(__STDC_VERERSION__) &&__STDC_VERERSION__ > 199901L
 printf("C99 standart\n");
#elif defined(__STDC_VERERSION__) &&__STDC_VERERSION__ > 199409L
 printf("C89 with additions 1\n");
#else
 printf("C89\n");
#endif
#else
 printf("C not standartizied\n");
#endif

  return 0;
}
```

# Language Rules

## About Names Overloading in C/C++

In C and other programming languages, the same identifier can be associated with more than one object at a time. This situation is called *name overloading* or *name hiding*.
In C++ (Take a look, for example, C++ 2003 Standard, chapter 13), this concept is introduced in the C language. 

It is an error to create two declarations of the same name in the same overload class in the same visibility block or at the top level.

| # | **Overloading class name**       | **Identifiers included in the class**                                                                         |
|---|-----------------------------------|----------------------------------------------------------------------------------------------------------------|
| 1 | Preprocessor Macro Names          | The names used by the preprocessor are independent of any other identifiers.                |
| 2 | Operator labels/tags              | The labels used immediately follow the `goto` statement.                                                          |
| 3 | Structures, Union, and Enums tags | They are part of a structure, union, or enumeration and immediately follow the keywords: ```struct```, ```union```, ```enum```. |
| 4 | Components namespace              | Defined in the namespace(or name scope) associated with the corresponding structure or union type.             |
| 5 | Another namespace                 | Name of the following objects: *Variables*, *Functions*, *Typedef names*, *Enumeration constants*.                 |

C++ introduces structure and union tags, and enumeration names implicitly declared via `typedef` in the namespace "Another" where in fact there are also usual variables are locating.

However, tag names can be hidden by subsequent variable or function declarations or by an enumeration member of the same name in the same scope. 
If you explicitly use a ```typedef``` for a structure followed by a variable declaration, it will lead to an error.

It is interesting that according to ISO/IEC 14882 C++ 2003, 3.3.7. In any order, functions/variables take precedence over type tags.

## Literal constants

In C/C++, in a literal expression, you can encode the type of literal:

| # | **Type**      | **Suffix** | **Alternative suffix** |
|---|---------------|------------|------------------------|
| 1 | long          | l          |                        |
| 2 | long long     | ll         | LL                     |
| 3 | unsigned      | u          | U                      |
| 4 | unsigned long | ull        | ULL                    |
| 5 | float         | f          | F                      |
| 6 | double        | no suffix  |                        |
| 7 | long double   | l          | L                      |
| 8 | std::string   | s          | Since C++17            |

## Prefixes for strings from C++11

Starting from C++11, you can use the following prefixes for strings:

| # | **Suffix** | **Desciption** |
|---|------------|----------------|
| 1 | L'a'       | wchar_t symbol. For Windows it's UTF-16, for Linux it's UTF-32. |
| 2 | u'a'       | ucs2 symbol. Pretty like UTF-16, but surrogate pairs are not supported in UCS-2.      |
| 3 | u"a"       | UTF-16 string. With support for surrogate pairs.                      |
| 4 | U'a'       | ucs4 (UTF-32) symbol. |
| 5 | U"a" | ucs4 (UTF-32) string                    |
| 6 | u8 "UTF8 string"      | UTF-8 string            |
| 7 | R"(asd\n)"  | Raw string. Analogue of Python's r"""str str""". Multiline is supported for such lines.        |
| 8 | R"*(asd\n)*"  | Raw string literal with custom delimiters.         |

The UTF-8 and UTF-16 are variable width encodings for characters, and not all letters can be represented by a single
character.

## Function Call Nuances

1. There are two kinds of the function call in C++ only: *ordinary function call* and *member function call*. A static member function (9.4) is an ordinary function. (С++ ISO/IEC 14882 2003-10-15)

2. In functions with `void` return types or when the return type is absent e.g. in constructors/destructors, you can have the absence of a ```return``` statement in a function body. It is equivalent to an explicit ```return;``` at the end of the function body.

3. But due to (C++2003, 6.6.3) *"Flowing off the end of a function is equivalent to a return with no value; **this results in undefined behavior in a value-returning function**."*

4. In C++, the ```main``` function cannot be called recursively.

5. Starting from C++11 there is a suffix syntax for function return type. It is not primarily about templates and type deduction; it is about scope. One more example of when it was useful (http://www.stroustrup.com/C++11FAQ.html)
```cpp
template<class T, class U>
auto mul(T x, U y) -> decltype(x*y) {
  return x*y;
}
``` 
We use the notation auto to mean "return type to be deduced or specified later."

6. A non-constant reference cannot refer to a temporary variable.

7. Although temporary objects can only be passed as `const T&` or `T.` However, calling non-const methods on temporary objects is allowed. The initializer for const T& does not need to be an lvalue and even be of type T. In such cases, a temporary variable is created to hold the initializer, lasting until the end of the scope of the reference.


8. Due to ISO C++2003. 7.5.3 there is the following requirement for linkage aspect of functions: *Every implementation shall provide for linkage to functions written in the C programming language, "C", and linkage to C++ functions, "C++".* To link functions in C++ style:
```cpp
extern "C++" void f() 
```
In fact, lLinkage rules cover not only name mangling but also the call convention.


## Requirements for C++ expressions

1. In C++98/03 you cannot modify a variable more than once without a sequence point in C++03/98. *Sequence point* - semicolon, function return, function jump, and some others. Please check the specification. 

2. In C++11 introduces the term *order of evaluation*. The term *sequence point* is no longer used. But the rule is the same.

3. Even in C++17 the statement when you modify the value more than once is a bad practice. But in fact, the C++17 standard added the rule that all side effects of the right side of an assignment are fully committed before evaluating the
left side and the actual assignment. That means that the following statement is legal starting from C++17:
```cpp
int k = 0;
k = k++ + 5; // Valid from C++17
```
## Exceptions to the one definition rule

You can read about that in detail in [1], 9.2.3 p. 248

There can be more than one definition of the following things:
1. class type (Clause 9)
2. enumeration type (7.2)
3. inline function with external linkage (7.1.2)
4. class template (Clause 14)
5. non-static function template (14.5.6)
6. static data member of a class template (14.5.1.3)
7. member function of a class template (14.5.1.1)
8. template specialization for which some template parameters are not specified (14.7, 14.5.5)

That same definitions are acceptable when:
1. They are in different translation units
2. They are identical token by token
3. The meaning of token is the same in both translation units (Checking this is not included in the capabilities of the programming language itself but is assigned to the toolkit)

All exceptions to the One Definition Rule are described in C++2003, p.23, §3.2/5.

## Basic integer types

In C and C++98/03/11 there are three representations of signed integers of n bits that are allowed for implementation:

* two's complement (twos-complement-notation) [-2**(n-1), +2**(n-1)-1]. Positive numbers are represented in the usual way. The most significant bit of the sign is set to 0
negative numbers are obtained as (reverse bits(number)+1) in ASM instruction notation for x86 sounds like a NEG operation
1000000..000 is the maximum negative number that has no positive equivalent.

* one's complement (ones-complement-notation) [-2**(n-1)+1, +2**(n-1)-1]
Negative numbers are the complement of all bits of the corresponding positive number. In this representation, positive and negative zero are possible.

* signed integer representation (sign-magnitude-notation) [-2**(n-1)+1, +2**(n-1)-1]
The representation of the modulus of negative and positive numbers is identical. The sign of the number is stored in the most significant bit.

But starting from `C++20`, there is only one signed integer representation, and it's twos-complement-notation.

About enums:
* Special dedicated type for enumerating integer constants from C89/99/11, C++98/03/11 is called `enum`. There are some subtleties with it:

* In C98/C99, then `enum` type is a synonym for integer with type `int`.
* Unlike C98/C99, the C++ language treats each enumerated type as a specific type and from integers as well.

In reality, that underlying type for C++ has some underlying integer type to actually store values, but it has not been specified.

Starting from C++11 now we have two type of enums: **Strongly typed enums(or scoped enumerations)** and usual **enums (or unscoped enumerations)**. Strongly typed enums do not support implicit conversion to int. They support their own namespace. It's possible to specify for them the underlying type. The underlying default type for strongly typed enums is `int`. Example:
  ```cpp
  enum class Color : int{red,green,blue};
  ```

For ordinary enums in C ++ 11, as in C ++ 98, nothing is said about the underlying type by default. If the underlying type is specified, you can make a forward declaration for enums.

B.Stroustrup, in his blog, notes that it is now possible to explicitly (optionally) use the name of a regular and scoped enum as a namespace to refer to its elements, as it were, through the namespace of a new type.

## Basic integer types nuances

1. The compiler's use of `unsigned` or `signed` in the absence of an explicit type specification is not defined for `char`. 

2. The compiler's use `unsigned` or `signed` in the absence of an explicit type specification is not defined for bit fields.

3. In general, the result of doing the right shift for signed integer types in the case of negative numbers is undefined before C++20. The compiler implementer can perform either a logical right shift or an arithmetic shift ([2], p. 252). Since C++20 right-shift on signed integral types is an arithmetic right shift, which performs sign-extension.

## Auto Type Deduction

The `auto` in C++98/03 was an explicit memory type for local objects, but starting from C++11, it's a type automatically deduced similar to `template` arguments. 

Also, `auto` never deduces to a reference type, always to a value type. This implies that the value still gets copied even when you assign a reference to `auto`. To make the compiler deduce a reference type, you can use `auto&` or `const auto&` [4, p.309].

The `auto` works in usual functions for variables and for arrays. For auto, the deduction is identical to the output for `template` function arguments.
```cpp
auto v1(expr); // direct initialization
auto v2=expr;  // copy initialization
int arr[] = {1,2,3};
for (auto x:arr) {
  printf("%i\n", x);
}
```

You need to be careful when using braced initializers with the `auto` keyword.
```cpp
auto x1 = {1,2,3,4}; // x1 is an initializer_list<int>

// Bracket/Uniform initialization via using {} in the form of list initialization does not allow narrowing
```

Auto can be used jointly with `constant` `volatile` type qualifiers (cv) and with reference and pointers. Examples:
```cpp
int ii= 1;
const auto * p_ii = &ii;
const auto& p_ref = ii;
```

## Range based for loop (since C++11)

Starting from C++11 there is a new syntax for `for` loop named as "range based for loop". Example:
```cpp
for (auto i : v) 
  std::cout << i;
```
Range-Based for Loops valid for any type supporting the notion of a range. One of the following constructions should be valid:
* *obj.begin()* and **obj.end()*
* *begin(obj)* and **end(obj)*

# Technical Differences between C and C++

1. Old C style function declarations are not allowed in C++
```cpp
double alt_style( a , real ) /* Obsolete function definition */
    double *real;
    int a;
{
    return (*real + a);
}
```

2. C programs should not use names that are keywords in C++ if one wants to be compatible with portability.

3. C++ style comments `//` only appeared in C99.

4. C++ has new operations ```.*, ->*, ::``` which are not in C

5. Different memory for char literal in C and in C++
```cpp
sizeof('a') == sizeof(char) // C++
sizoef('a') == sizeof(int)  // C
```

6. C++ 1998 uses the C89 preprocessor, although the C language has changed: Tradition C, C89, C95, C99, C11

7. Struct tags in C++ are included in the "other names" namespace.
In this space are
* variables
* functions
* typedef names
* enum constants

Therefore, ```struct n{}; typedef double n;```is correct in C but not in C++.

7. Although for C++ type tag names (struct, union, enum) are implicitly declared using `typedef`, they can still be hidden by variables in the same scope `S S;`.

8. C99 has pointer qualifier `restrict`, which is not in the official specification of C++98/03/.

9. Support of ```varying array``` array. In C99, the last member of a structure can be a flexible array, which is also possible in C++.

10. In C99, but not in C++, there is a ``` flexible arrays```. That arrays with a size specified via a non-const variable. In C99, to pass such arguments to a function, use the notation `void g(int pp[*], int k){}`.

11. Different initialization of the char array. In C++, the array must be of sufficient size to hold the "\0" character
```cpp
char a[3]="12"; char aEquiv[]="12";  // ok in C/C++
char a[3]="123";                     // ok in C, but not in C++
```
11. C99 has named initializers for structures and positional initializers for arrays. C++03 does not.

12. The definition of ```struct``` and ```union``` in C++ have block scope.

13. ```const``` declarations are ```static``` by default in C++, but ```extern``` in C (Appendix C. C++2003)
7.11.6, C++2003:
*"A name declared in a namespace scope without a storage-class-specifier has external linkage unless it has internal linkage because of a previous declaration and provided it is not declared const. Objects declared const and not explicitly declared extern have internal linkage."* It also follows from this paragraph that declarations of non-const variables declared on namespace level have extern linkage by default in C++.

14. C++ declaration ```void f()``` is equivalent to void ```f(void)``` in C. The declaration in C ```void f()``` state that function has an indefinite number of arguments.

15. If the array is multidimensional, then in all cases, only the leftmost index can be omitted to determine the array's size. Also, in C99, component-wise initialization is allowed, which is not permitted in C++98/03.

16. In C, but not in C++, you can write, although this is strange: ```sizeof(struct S{int a;});```

17. Implicit cast from integer type to enum is allowed in C but not in C++. C++ 2003-10-15. page 113. 7.2.5: *"The type of an enum is an integer type that must support all underlying values. In C, enum has a synonym for int."*

18. In C++, converting a void pointer to any reference type requires an explicit cast operation. And in C, this is done implicitly.

19. Unconditional branching through ```goto``` is allowed in the middle of a nested block in C (while initialization of automatic variables is not guaranteed), this is not allowed in C++ in general, but there is an exception. The exception is for POD types - you may skip their initialization. However, there are no guarantees for initialization of them.

20. In C++, there are more stringent requirements for inline functions - an ```inline``` function must be declared as such in all source files. In C99 this is not the case.

21. In C++, an ```inline``` function, in terms of code, can have an address and static variables inside. In C it is not allowed.

22. In C99, the compiler must see the function definition, i.e., the function should be defined so that it is inlined in ```*.h```. The compiler can choose to actually what to do:
* inline calls
* not inline
* partially inline.

23. C++ allows declaration in conditions, and it's not allowed in C.

24. There is no such type as a reference in C. (References are described in "С++2003, 8.3.2. References").

25. There are no overloaded functions in C.

26. C++ has default parameters, and they are not allowed in C.

27. In C++ there is a namespace mechanism with namespace, and it does not exist in C.

28. In C you can use ```exit()``` and ```abort()``` with no problems, but in C++ the destructors of local objects are not called.

29. Overloading of operators and functions is allowed only in C++.

30. C does not support General-Purpose-Programming with templates.

31. C99 has a predefined identifier ```__func__```. This identifier is implicitly defined by the compiler at the beginning of the function body as static const char ```__func__[] = "function-name"```. Such identifier was absent in C++98/03.

32. In C++, operators that are not presented in C language usually have the highest precedence, except for ```throw``` which is only above the comma operator ```,```.

33. In C, there must be at least one element in the initialization list when a structure or array is initialized. 

34. Prior to C99, i.e. in C89, C89 with the extension, there was a restriction on where automatic variables can be defined - only at the beginning of a local block. In C++98/03 already, you can declare local variables anywhere.

# Memory

## Memory Types and pointers

1. An ordinary string literal has the type "array of n const char" and static storage duration.

2. About a pointer to constant data and a constant pointer [2], p. 105. In principle, a possible trick to remember this is to read the expression from right to left and to which "const" type or variable is closer to that and apply this modifier.
```cpp
int* const const_pointer;
const int* pointer_to_const;
```

3. Quite a lot of important information is contained in "C++2003 5.3.3 Sizeof" including the following:
* ```sizeof(char)``` with all variations of char is always one byte.
* `sizeof(bool)` and `sizeof(wchar_t)` is implementation-defined.

4. Also, `sizeof` of structures in C/C++ is equal to the amount of memory to store all components, space for padding between components, and space for padding after structures. 

5. The `sizeof` operator applied for an array of structures and to other types, the following rule must be fulfilled: *The size of an array of N elements in bytes is equal to N times the size of the array element.*

6. In C/C++, a function pointer expression can be used to call a function without explicitly dereferencing the pointer, i.e., you can call the function via using the function pointer via `(*f)()` or via `f()`.

## Used Memory for Types and Their Layout

1. The representation of an object in memory is a sequence of bits. The representation does not have to include all the *bits*, but the size of an object is the number of units of memory it occupies. 
The amount occupied by one char character is taken as a memory unit. The number of bits in character is specified in the CHAR_BIT macro in C Language. All objects of the same type by C/C++ rules occupy the same amount of memory. In practice, however, one char is "always" one byte, i.e., the 8 bits number.

2. Computers are classified into two categories in the order of bytes in a word:
- *Right to left*, or *Little - Endian* - the address of a 32-bit word matches the address of its least significant byte (Examples of CPU architectures are Intel x86, Pentium)
- *From left to right*, or *Big - Endian* - the address of a 32-bit word matches the address of its high-order byte (Motorola). Some systems support two modes at the same time. 

3. In some computers, data can be located in memory at any address; in others, alignment conditions are imposed on certain types.

4. A typical data type to store pointers to some object/data is a pointer. To store (or serialize the value of pointer) in some integer variable, you can use ```uintptr_t```. The ```uintptr_t``` integer type was introduced in C99. The ```uintptr_t``` is sufficient to store a pointer to any data, but formally not to a function.

5. A special value in C/C++ called a null pointer equal to a null pointer constant. A null pointer can be converted to any other type of pointer.

5. A null pointer in C/C++ is an integer expression that yields zero. Or such an expression cast into a pointer. The expressions below will not result in a compilation error, as much as we would like to:
```cpp
      void y(int*){}
      y(0);
```
6. In C++11, instead of NULL, you can use `nullptr`. That keyword stands for null pointer variable with type `std::nullptr_t.`

7. When using `union` for a mixture of structures that start the same way, there is a guarantee in C/C++ of an identical physical mapping of components "from this beginning".

8. In C and C++, the components of the variable of structure type ```struct``` has addressed. There are the following guarantees:
* The component addresses are in ascending order. 
* The address of the first component is the same as the address of the beginning of the structure. And it is regardless of what endian the computer has where the program will run.

9. Structs are not allowed to perform comparisons with `==` or with `>`. The fundamental nature of this restriction in C/C++ is because, for objects, there may be holes in their memory layout that are filled randomly.

10. In C++, for the definition (not just declaration) of a variable in global scope, you can use `extern int a = 0;`. But in fact, `extern` is ignored.
It's due to (7.11.6, C++2003):
```
"A name declared in a namespace scope without a storage-class-specifier has external linkage unless it has internal linkage because of a previous declaration and provided it is not declared const. Objects declared const and not explicitly declared extern have internal linkage."
```
It also follows from this paragraph that declarations of non-const variables declared on namespace level have ```extern``` linkage by default in C++.

12. A compile-time string literal in C/C++ is statically allocated so that it is safe to return one from a function.

## New operator (heap memory allocation)

In C++, before the introduction of the exception mechanism, the `new` operator returned 0 when the memory allocation failed. 
In the C++ standard, `new` by default throws a `std::bad_alloc` exception. As a rule, striving for similarity to the standard is best. Better to modify the program to catch `bad_alloc` rather than check the return for 0. In both cases, doing anything other than throwing an error message is not easy on most systems. See paragraph 5.3.4. Subparagraph 13.
http://www.ishiboo.com/~nirva/c++/C++STANDARD-ISOIEC14882-1998.pdf

For Visual Studio compiler: 
1. `new(std::nothrow)` - does not throw an exception 
2. regular `new` - throws an exception. You can customize the behavior using linker options: http://msdn.microsoft.com/en-us/library/kftdy56f.aspx


## Placement New

There are such variations of the new operator:

1. Usual placement `new`. Creation of an object, but using the already prepared address space. If the implementation needs to store some meta-information, then it can be the case that `b != address`. Example:

```cpp
#include <new>
int *b = new(address) int(init_value);
```

2. Overloaded operator new as a new global function. Example:
```cpp
void* operator new(size_t sz) {return a.allocate(sz);}
void operator delete(void* ptr)
```

3. Overloading `new` with custom parameters. The first argument to the operator is the size in bytes and calculated automatically via `sizeof`. After that, there is a list of arguments that you decide clients should pass. Example:
```cpp
void* operator new(size_t sz, Arena& a, float b) 
{ return a.allocate(sz);}

new(arg2, arg3) SOMETYPE()
```

4. Operator overloading in a class. You can define new/delete within a class. It's good practice to make new/delete `static`.
However, the operator will be implicitly static even if static is not explicitly specified.

## Pseudo Destructor
When you need to call the destructor explicitly, and when you understand what you're doing, you can actually call in the C++ destructor via using **pseudo-destructor**. Moreover, the **pseudo-destructor** can be virtual. Of course, you need to do that in very rare cases.

```cpp
#include <stdio.h>
#include <utility>
class A {
public:
   A()          {printf("A()" "\n");}
   virtual ~A() {printf("~A()" "\n");}
};

class B : public A {
public:
   B()           {printf("B()" "\n");}
   ~B()          {printf("~B()" "\n");}
};
int main()
{
 A* a= new B;
 a->~A();
}
```

## Aggregates 
Formal definition from the C++ standard (C++03 8.5.1 §1):
*An aggregate is an array or a class (clause 9) with no user-declared constructors (12.1), no private or protected non-static data members (clause 11), no base classes (clause 10), and no virtual functions (10.3).*

Aggregate types are unique in that objects of such types can be initialized in C++98/03 using the curly brace syntax, just as structures are initialized.

## Data types with special guarantee in memory layout: POD or Plain Old Datatype (C++03)

An aggregate class is called a POD if it has no user-defined copy assignment operator and destructor and none of its nonstatic members is a non-POD class, array of non-POD, or a reference.

If you want to write a more or less portable dynamic library that can be used from C and even .NET you should try to make all your exported functions take and return only parameters of POD-types.

The lifetime of objects of non-POD class type begins when the constructor has finished and ends when the destructor has finished. For POD classes, the lifetime begins when storage for the object is occupied and finishes when that storage is released or reused.

For objects of POD types, it is guaranteed by the standard that when you memcpy the contents of your object into an array of char or unsigned char and then memcpy the contents back into your object, the object will hold its original value.

As you may know, it is illegal (the compiler should issue an error) to make a jump via goto from a point where some variable was not yet in scope to a point where it is already in scope. This restriction applies only if the variable is of non-POD type.

It is guaranteed that there will be no padding at the beginning of a POD object.

## Data types with special guarantee in memory layout: Standard Layout (From C++11)

C++11 introduces relaxed POD type definition; new standard layout types. To have a standard layout, the following rules should be satisfied for your type:

* no virtual functions
* no virtual base
* zero or more base classes of standard-layout class types
* no two base classes of the same type
* all data members should have the same access control
* all data members are defined in the most base class or most derived class.
* no restriction for static member functions and static members

# Built-in Type Conversion

Before going into technical details about type conversion, let me be honest - it's hard to remember them, so possibly it is better to observe the big picture first:
```
The general requirement when converting integer types is the mathematical equivalence of the source and target values.
```

Now let's go into subtle technical details.

## Prohibited conversions

1. Converting a pointer to a function, a pointer to a data, and the other side direction is not allowed in C/C++.
2. Built-in conversion to a `struct`, or to the `union` is not allowed.
3. C++ treats `enum` as distinct from each other and from integer type as well.
4. In C, implicit conversion from integer to enumerated types is also allowed because in C, `enum` are C, but in C++, it is prohibited.
4. In C and C ++, implicit conversion from enumerated types to integer types is allowed.
6. Converting a pointer to a function to a pointer to data and the other side is not allowed in C++.


## The sequence of type conversions rules in C/C++
1. Trivial transformation. Conversion to identical types. A conversion from "function ..." to "function pointer ...."
2. If an overflow occurs during conversion to a signed type, then the value is considered overflowed and technically **undefined**.
3. If an overflow occurs during conversion to an unsigned type, the final value equals the "unique value" mod $2^n$ of the result. When using two's complement presentation, converting to/from signed to unsigned integers of the same size does not require any bit change.
4. If the final type is shorter than the original and both types are unsigned, the conversion can be performed by discarding the appropriate number of most significant bits. The rule is also applicable to integer types in 2-s complement notation.
5. When converting from float values to int, the final value should be equal to the initial value if possible. The nonzero fractional part is discarded. 
(The result is **undefined** if the value cannot even be approximated)

6. In C, conversion to floating-point types is possible only from arithmetic types. During converting from double to float, the final value must equal one of the two values closest to the original value. 
(The choice of rounding is implementation-dependent)

7. If it is impossible to convert from double or int to float, then the value is **undefined**.
(Example: If the range of the target double type does not match)

8. Conversion from the type array of type T to a pointer to type T is performed by substituting the pointer for the first element of the array.

9. A value of any type can be converted to ```void```.

10. Conversion to ```void *``` and back guarantee the restoration of the original pointer value

11. In C, ```void *``` can be **implicitly** converted to a pointer to any type. In C++, **an explicit cast** is required. (Appendix C, 4.10, C ++ 2003 standard)

12. On the operands of unary operations, ordinary unary conversions are performed. The goal is to reduce the number of arithmetic types.
   * An array of type T $\to$ pointer to the first element (not applied for arguments of ```operator &``` and ```sizeof``` operators).
   * Function $\to$ function pointer
   * Conversions from an integer type of rank below int $\to$ to int
   * Conversions from unsigned integer types lower than int, int represent all values $\to$ values are cast ​​to integers
   * Conversions from unsigned integer types lower than int, but int does not represent all $\to$ values are cast ​​to unsigned int
13. On the operands of a binary operation, the usual unary conversions are performed separately for each argument, and after that, the regular binary conversions are applied.
14. If some operands of the binary operator have the type `long`, `double`, `double`, `float`, and the second operand has a rank lower, then it is cast to the type with the highest rank.
15. If both operands are unsigned, then both are cast to a higher rank unsigned type.
16. If both operands are signed, then both are cast in the signed type of the higher rank.
17. Unsigned operand and lower-ranked signed operand $\to$ unsigned type.
18. Unsigned operand and signed type operand of higher rank $\to$ signed type.
19. If the prototype is controlled by an ellipsis `...`, i.e., the function obtains varying argument numbers, then the usual unary conversions are performed on the operands. Also, besides that, `float` is always promoted to `double`. The float is not converting into a double if there is no ellipsis and the call is fully prototype-driven.


# Namespaces

## Basics about Namespaces

The namespace is a mechanism for reflecting logical grouping. If some declarations can be combined according to some criteria, they can be placed in the same namespace to reflect this fact. 

**Namespace advantages:**
* Logical structure reflection
* Avoidance of name conflicts
* Express a coherent set of tools 
* Prevent users from accessing unnecessary tools 
* Do not require significant additional effort when using

**Namespace disadvantages:**
* Waste of time analyzing the assignment of objects to different namespaces
* Various additional nuances: 
  - A local variable or a variable declared via `using` hides external variables in relation to the block of visibility.
  - When libraries that declare many names are made available through the `using` directive, it is important to understand that unused name conflicts are not considered errors.
  - Elements of the same namespace can be in different files.


## Namespace lookup rules
A namespace is a named scope. Unlike a class definition, a namespace is open to new features being added to it. The `using` directive applies more to namespaces than to classes.

1. If the function is not found in the context of its use, then an attempt is made to search in the namespace of the arguments. This rule does not pollute the namespace.
```cpp
namespace NameSpace {
  structType{};
  void func(Type x)
  {}
}
...
func(NameSpace::Type());
```
This mechanism is called an Argument-dependent lookup (ADL). It's useful, for example, when calling some overridden operator on your type in a situation where you decide to define an operator in the namespace your type is in.

Some nuances I've come across: [https://stackoverflow.com/questions/45713667/unqualified-lookup-in-c](https://stackoverflow.com/questions/45713667/unqualified-lookup-in-c)
Various nuances of working with namespaces are covered in the appendix [1] B.10, page 924

2. A locally declared name and a name declared with a `using` directive hide a non-local declaration.

3. Local name declaration takes precedence over NS name, but the global declaration does not take precedence over variables imported from NS::*

4. Collisions of unused names are not treated as errors

5. Global names are in the "global namespace". It's just global. It differs from all namespaces (including the unnamed one). 
The global namespace differs from those defined through namespace only because it is not necessary to write its name. 
It's only worth thinking about when you need to use ::global_var when you have a problem (3). The operator `::` stands for scope extension. 
With this construction, you will always look first in the global namespace and then in the namespaces imported into the global namespace.

6. If the name is declared in the enclosing scope or the current scope, then the name can be used without problems, without a full qualifier.
7. Continuous repetition of a qualifier distracts attention. Verbosity can be eliminated using the declaration:
7.1 Creating a synonym for a variable through `using NS::x;` It's called **using declaration**.
7.2 Creation of synonyms for all variables from namespace - through `using namespace NS;`. It's called **using directive**.

8. Placing 7.2 inside another NS opens up the way to combine/mix features from different namespaces.

9. Creating an unnamed namespace implies auto-generating its name by the compiler and insertion `using namespace GEN_NAME;` to the source file with that unnamed namespace.

10. Names explicitly declared in a namespace and also made available with using declarations i.e. via `using NS::x;` take precedence over names made available via using directives i.e. `using namespace NS;`

11. Namespaces can be nested. To create an alias, you can use a construct like the following:
```cpp
namespaceAA = NameSpace::NameSpace2;
```
12. Namespace Search Rules in case of using nested namespace

Example with a variable "i" in ANSI ISO IEC 14882, C++2003, 3.4.1, (6) (page 30).
```cpp
namespace A {
  namespace N {
    void f();
  }
}
void A::N::f() {
    i = 5;
}
```
The following scopes are searched for a declaration of i:
1) innermost block scope of A::N::f, before the use of i
2) scope of namespace N
3) scope of namespace A
4) global scope, before the definition of A::N::f

Some relative things are here: https://en.cppreference.com/w/cpp/language/unqualified_lookup

13. One subtle addition to function names. 
Function names obtained from ADL are looked up in the namespaces of their arguments in addition to the scopes and namespaces considered by the usual unqualified name lookup.

## Examples of using `using`

```cpp
// Make cout available without qualification
using std::cout; 
// Make all names in std available without qualification
using namespace std;

// Defines Big as a type alias
using Big = unsigned long long;
// Defines BigWithTypedef as an alias for long long (Typedefs in C++20 are obsolete).
typedef unsigned long long BigWithTypedef; 
```

# Exceptions

## Basics about Exceptions
When a program is constructed from separate modules, and especially when these modules are in independently different libraries, it is convenient to divide error handling into two parts:
* Generation of information about the occurrence of an error situation that cannot be resolved locally.
* Handling Errors Found Elsewhere

*Error handling code can be shorter and more elegant using a return value, but this solution does not scale well.*

Generally, separating error handling code from "normal" code is a good strategy. Throwing an exception may leave the object in an invalid state.

Throwing an exception can be a source of memory and other resource leaks. It's best to rely on the properties of constructors and destructors and their interactions with exception handling to deal 
appropriately with an object. (Escape from a block by throwing an exception cleans up all created local automatic things in reverse order of creation.). Writing correct exception-safe code using explicit tries can be a difficult task.

## Extra about exceptions

* You can group exceptions by inheritance relation.
* Exceptions at the time of generation are copied. The const modifier in the catch block does not affect anything. However, the presence of a `T&` or `T` type signature is affected. The latter causes the copy constructor to execute. For `throw T();` you can't see the copy constructor run in VS 2012. But can be seen for:
```cpp
{T e; throw e;}
```
* Exiting a destructor by throwing an exception is against the requirements of the standard library.
* The process of calling destructors for automatic objects constructed on the path from a try block to a throw expression is called "stack unwinding."
* If a destructor called during stack unwinding exits with an exception, terminate is called (C++2003, 15.5.1). So destructors should generally catch exceptions and not let them propagate out of the destructor.
* If an exception is thrown but not caught, `std::terminate` is called. You can set your behavior with `std::set_terminate`.
* It is possible to rethrow an exception with `throw;`.
* When an exception is thrown in a constructor, the object's destructor is not called.
* If an exception is thrown in the destructor during the call to the destructor during exception handling, then this is considered an error in the exception handling mechanism, and `std::terminate()` is called. 
To distinguish the behavior of executing destructor due to normal call of the destructor or during stack unwinding, you can use: `uncaught_exception()` in the destructor.

* The basic errors classes are `exception`, `logic_error`, `runtime_error`. Some others class: `bad_alloc`, `bad_cast`, `bad_typeid`, `bad_exception`, `out_of_range`, `invalid_argument`, `overflow_error`, `ios_base::failure`.

* If a function tries to throw an exception it didn't declare, it will result in a call to `std::unexpected`, which by default pulls std::terminate (p.429, Stroustrup, special edition)

```cpp
intf(); /* Can throw any exception */
int f() throw(); /* Throw no exceptions */
int f() throw(x2, x3); /* Throws only exceptions x2, x3 */
```

Starting from C++11, it's possible to use an empty exception specification `throw()` defined in an alternative way via  `noexcept`.

```cpp
void g1(int) throw() {}
void g2(int) noexcept {}
```
If you see a `noexcept` in a functions header, you can be sure that this function will never throw an exception.

Construction of interception of exceptions from the initialization list. Example:
```cpp
#include <stdio.h>

class C 
{ 
public:
  C() try : a()
  { puts("C()");  }
        catch(...)
  { puts("WOW!"); }
  int a;
};

int main()
{
  C c;
  return 0;
}
```

----

# Overloading

## Functions and operator overloading precedence

The function's return type is not part of the function's signature. To decide which function overload
to use, the compiler looks only at the number and types of the function parameters and arguments.


1. Exact type matching, or the matching achieved by trivial conversion (array name to a pointer, function name to function pointer, type `T` to `const T`).
2. Correspondence is achieved by promotion of integral types and promotion of real numbers to integers. (`char` to `int`, `float` to `double`).
3. Correspondence achieved by standard conversions (`int` to `double`, `double` to `int`), pointers to derivatives to pointers to base classes. Pointers to arbitrary types to pointers to `void*`.
4. Correspondence achieved with user-defined transformations
5. Correspondence due to ellipsis `...` in the function definition.

If a match can be achieved in **two ways** at the same criteria level, the challenge is considered ambiguous and is rejected.

Also, overload the function with Xvalue Reference `A&&` has priority under constant reference `const A&`.

Very popular fix the standard behavior of the compiler, not trying to find an overloaded function in B:
```cpp
class B  {
public:
  void f(int i) { cout << "f(int)\n"; }
};

class D : public B {
public:
    // fix "strange" behaviour
    using B::f;
    void f(double d) { cout << "f(double)\n"; }
};
```

## Template function overloading
Template function overloading searches for a set of suitable specializations according to steps (1-4) described below:

1. All specializations that can potentially be called.
2. If any specialization is the more specialized of the two, the less specialized is discarded.
3. Overloading allowed for functions from steps 1-2 and regular functions
4. If a regular function and a template function match equally well, the regular function takes precedence.

The call is considered an error if the function passed 1-4 is not found.

## Resolving the overloaded binary operator for x(op)y.

1. If X(type of x) is a class. Find out if the operator is defined as a member of class X or a base class of X.
2. View operator declaration in the context of x(op)y expression.
3. If X is declared in namespace N, look for operator declaration in namespace N.
4. If Y(type of y) is declared in namespace M, look for operator declaration in namespace M.

## Operators overloading rules in C++

Please check the details in Standard. C++ 2003. p. 233. 13.5.1 - 13.5.7. 

According to the Standard, operators cannot be overloaded as static methods of a class. It is possible to overload them:
* as functions 
* as non-static class methods. (The operators `=`, `[]`, `->` can be overloaded only in this way).

Next, you cannot overload the following operators: `.`, `::`, `.*`, `->*`, `sizeof`, `typeid`, `?:`.

# ```typename``` keyword
The typename keyword must be used in three tasks.

1. Replacing the keyword class with the word typename in the argument type declaration for a template class/function/method.

```cpp
template <typename> struct S{}
```

2. Accessing type names through the scope of the class that is the template argument.
```cpp
template <class T> struct S {
  typename T::SomeType a;
}
```
Comment by B. Stroustrup *"In some cases, a smart compiler could guess, but in general it's not possible"*.

3. The typename keyword is required if the type name depends on the selected template parameter.
```cpp
template <class T> T findMax(const std::vector<T>& vec){
  typename std::vector<T>::const_iterator max_i = vec.begin();
  for (typename std::vector<T>::const_iterator i = 
  vec.begin() + 1; 
  i != vec.end(); 
  ++i)
  {
    if (*i > *max_i)
      max_i = i;
  }
  return *max_i;
}
```
There is also a very detailed description of the `typename` keyword here:
[http://stackoverflow.com/questions/610245/where-and-why-do-i-have-to-put-the-template-and-typename-keywords](http://stackoverflow.com/questions/610245/where-and-why-do-i-have-to-put-the-template-and-typename-keywords).

# Class constructor and destructors

## Logic behind executing constructors
The order of working out the initialization of a class object in C++ is described in C++ Standard - ANSI ISO IEC 14882 2003; 12.6.2, p.230.

The order of initialization of classes and execution of constructors:

1. Depth-first, left to right constructors of virtually inherited classes whenever they are located in the inheritance tree.

```cpp
#include <stdio.h>

class A {
public: A(){printf("A()\n");}
};

class B:virtual public A {
public: B(){printf("B()\n");}
};

class C: /*virtual*/ virtual public A {
public: C(){printf("C()\n");}
};

class Branch {
public: Branch(){printf("Branch()\n");}
};

class D : public Branch, virtual public B, virtual public C {
public: D(){printf("D()\n");}
};

int main()
{
    D d;
    return 0;
}
```

Surprisingly, it will not be Branch() that will be printed first, but the output will be like this:
```
A()
B()
C()
Branch()
D()
```

2. Execution of constructors of directly base classes in the order from left to right from the class description (and not in the order specified in the initialization list).

3. Initialization of class members in the order specified in the class description (again, not in the order specified in the initialization list).

4. Execution of the function body of the constructor.

5. The constructor also introduces an implicit conversion. To suppress implicit conversion, the constructor must be declared with the `explicit` parameter. ([1], p.333)

6. In C/C++, when using custom conversions via constructors without `explicit` keyword or defined `type conversions` - only one level of implicit conversions is allowed.

## Logic behind executing destructors

When processing the destructor, identical actions behind the logic of constructor's execution is performed but in reverse order.

1. Working out the body of the destructor for class members
2. Destructor of direct non-virtual base classes
3. If the object is the object of the "deepest" class in the inheritance graph, then virtual base destructors are called

## Deleting object of incomplete type

Deleting an object with an incomplete type. 
```cpp
class My;
My* ptr;
delete ptr; // undefined behaviour for incomplete types
```
For POD and an object without a destructor, something like C runtime free will be done, which does not need to know about the object's size. 
In this case, you're lucky, and you can typically delete dynamically allocated objects, but in general, it results in undefined behavior. (5.3.5 Delete C++2003).

## Generate/Suppress generation of special class members

You can explicitly force the compiler to generate default code for a method for which this behavior can take place through `=default`. You can disable using (any) function/method by specifying `=delete`.

## Some class special members (since C++11)
```cpp
class X { 
public:
  // "ordinary constructor": create an object
  X(Sometype);            
  // Default constructor
  X();                    
  // Copy constructor     
  X(const X&);            
  // Move constructor  
  X(X&&);                 
  // Copy assignment: clean up target and copy     
  X& operator=(const X&); 
  // Move assignment: clean up target and move     
  X& operator=(X&&);      
  // Destructor: clean up
  ~X();                   
};
```

# Initialization

## C++ variable initialization

1. There are a lot of types of initialization in C ++

```cpp
const int v1(expr);   // direct initialization
int v2 = expr;        // copy/assignment initialization
int arr[] = {1,2,3};  // bracket initialization
int a {15};           // bracket initialization
int count(4);         // functional notation for initialization
int z{};              // zero initialization
```

2. Static variables are initialized to zero for the corresponding type. If the initialization list is empty, the array and structure variables are initialized to zero.

3. A reference in C++ shall be initialized to refer to a valid object or function. In particular, a null reference cannot exist in a well-defined program.

4. Types of initialization in C ++
* zero_initialization
* default_initialization
* value_initialization

More about initialization: 8.5, 8.5.1 Initializers from C++2003-10-15.

5. If, for an array or structure, the number of initialization values is less than the dimension of the array or structure, the rest of the elements are initialized with the default value for the corresponding type (as in the case of initialization of static variables).

6. In C++98/03, a `union` cannot have as a member an object with a user-defined constructor.

## std::initializer_list<T>

In C++98 constant member arrays and heap, arrays are impossible to init, but in C++11, there is an idea to bring bracket initialization to everything.
```cpp
int a[] {1,8,8}
```
Here {1,8,8} - is an initialization list. This construction implicitly casts to `std::initializer_list<T>`. Ctor with initialization list argument has priority during overloading. 

Type deduction in template functions does not work for `std::initializer_list` type. But for auto works fine.  **It is one place where auto != template**. Example
```cpp
// gcc -x c++ -std=c++11 t.cpp
#include <stdio.h>
#include <initializer_list>
 
template <class T> 
void f1(T a) {}

void f2(std::initializer_list<int> a) {}
int main()
{
//  f1({1,2,3}); // DOES NOT COMPILE
  f2({1,2,3});
  auto f3 = {1,2,3};
  return 0;
}
```

7. In [1], 10.4.6.2 for C++2003: *"You can initialize a class member that is a static constant of an integral
type. If and only if you do so, you need to declare this member once somewhere."*.

## Various constants flavors.

### const (C++03)
The keyword `const` prevent `const` objects from getting mutated. But `const` - can be initialized by something that is not a constant expression.

Const member function functions cannot change the state of the object.

### constexpr (C++11)
`constexpr` - indicating that it should be possible to evaluate the function at compile time if given constant expressions as arguments. The main idea of B. Stroustrup is that it brings type-rich programming in compile-time. The deep reason that includes this into language is that many communities ask B. Stroustrup to have something which will make table-lookup easier in languages. And because it's near impossible to be faster than table lookup, this concept can make sense.

C++11 `constexpr` functions had to put everything in a single return statement. C++14 `constexpr` functions, not necessarily had to put everything in a single return statement. Example: 
`constexpr int sum(int a, int b) {    return a + b; }`

A `const` differs from a `constexpr`. 

`constexpr`  - can be conceptually initialized only really by a const at compile time.
```cpp
constexpr int a = 12;
```
### constinit (C++20)
### consteval (C++20)

# Compute Optimization Relative Information

## Return Value Optimization
In a return statement, a compiler is allowed to apply the return value optimization (RVO), provided the returned name is the name of a locally defined automatic variable.

## Inline function call

Working with inline functions is described here: https://isocpp.org/wiki/faq/inline-functions. How to work with inline functions
```cpp
// inline.cpp
// empty
// inline.h
#include <stdio.h>
void f();

inline void f()
{
     printf("F inline");
}
```
And
```cpp
// main.cpp
#include "inline.h"

int main()
{
     f();
     return 0;
}
```

## Allowable reformulations
In C++ and C, the order in which subexpressions are evaluated is not defined `A(F(), G())`. 

The compiler is allowed to evaluate the operands of a binary operation in an arbitrary order and perform optimizations depending on the associativity and commutativity of the operation.

## Compiler Implementation relative Questions

What does it mean `A(*B)`? It can be declaring a variable or calling a function. This ambiguity makes the C grammar Context-Sensitive and not LALR(1).

In C++, access control is later than ambiguity.
```cpp
class A {
public:
  int a;
private:
  int a;
};
A z;
z.a = 1; // Compilation error
```

# Lambda functions

Lambda expressions offer a convenient, compact syntax to quickly define callback functions. Basic syntax:
```cpp
[] (int x, int y) { return x < y; }
```
* []. The opening square brackets are called the lambda introducer.
* (int x, int y). lambda parameter list between round parentheses. You may omit the empty parameter list for lambda functions without parameters and write: `[] {...}`.

*Closure* in math set with its boundary (*functional analysis*) or family function, which can be achieved via constructing all possible formulas under basis function (*discrete math*).

But in C++ *lambda closure* is functional object (instance of the class) with defined:
  `ret_type operator()(<list of arguments>) const`

The compiler creates that object during parsing lambda expression. So Lambda's in fact generate C++ classes with `operator()`. 

It's possible to add the keyword `mutable` to the definition of a lambda expression right after the parameter list. Doing so causes the compiler to omit the `const` keyword from the function call operator of the generated class.

You can refer to variables with static storage duration in lambdas. They all are captured.

You can use lambda to capture values "by value". In such a case, captured vars will be copied to a function object (closure).

Example: `[captureVar1,captureVar2](int arg1){}`

You can capture variables by reference. `&` - in context of lambda `&` means capture by reference, not dereferencing operator. Example: `[&captureVar1,&captureVar2](int arg1){}`

It exists notation to capture all non-static vars by value, or by reference:

`[=](int arg1){} // capture all not-static vars by value`

`[&](int arg1){} // capture all not-static vars by reference`

Next, a notation exists to capture all non-static vars by value or reference and specify something for other variables. Example of capture all not-static vars by reference, but by value capture Param2:

`[&,Param2](int arg1){}`

The capture default (`=` or `&`) if used, should always come first. [4, p.752].


Lambda return type can be deduced if lambda is one expression in C++11. Or you can explicitly specify it.

`[=](int arg1)->trailing_return_type{return trailing_return_type();}`

If lambda has more than one expression, then the return type must be specified via the trailing return type in C++11, and it will be deduced in C++14. A similar trailing syntax can be applied to auto and member - functions.

You can capture only local vars, not member variables of the object. Also, you can allow lambda to modify captured values.

```cpp
        int x = 12;
        auto a = [=]() mutable  ->void  { x = 1; };
```

You can capture this pointer explicitly
```cpp
auto a = [this]() ->void  { aa = 1; };
```
or implicitly, because default capture also makes this available.
```cpp
auto a = [=]() ->void  { aa = 1; };
```

Even though the lambda closure will be an object of a class another class, its function call operator will still have access to all protected and private members of Finder provided with `[this]` pointer to the object.

Even lambda is not a function pointer, and it is not an anonymous function, but **capture-less** lambdas can be implicitly converted to a function pointer.

In C++14, there is an extra feature with a name is **"init capture"**. It allows performing arbitrarily declaration of closure data members:

```cpp
auto interpolate =
[min = toFloat(0), max = toFloat(255)](int value)->float { return (value - min) / (max - min);};
```

Starting from C++14, you may not want to specify types of arguments. It's called *generic lambdas*. A *generic lambda* is a lambda expression where at least one placeholder type such as `auto`, `auto&`, or `const auto&`. That turns the function call operator of the generated class into a template call operator. Example:

```cpp
auto test = [](const auto& x){std::cout << x;};
```

Starting from C++20, the same `auto` syntax can be applied for generic functions. Both of that things are just a shorthand for template methods.

Starting from C++20, it's possible to be more explicit about the type and define what is called **Lambda Templates**. 

Example:

```cpp
auto multiply = []<class T>(T a, T b) {return a*b;};
```

# Move semantics
The move brings objects to a valid but unspecified state. Objects, in fact, can be reused after movement.

Move semantics is one of the main innovations of C++11. The move is useful for objects that store part of their state in a heap. 

Moving is never slower than copying and usually faster. For some objects, there are only move semantics, for example, thread.

It doesn't make sense to implement a move if (1) its speed is worse or the same as copying, (2) This operation is not on the critical execution path in the program. You shouldn't use `std::swap` to implement the move. It doesn't make any sense.

In C++98/03:
  LValue - something from which you can take the address. (variables, or lvalue reference)
  RValue - something from which you can not take the address (in 99% of cases, these are unnamed temporary variables)
  A good counterexample is something that is an rvalue but has a name - `this`.
    LValue reference - regular references
    Lvalue may bind to LValue reference
    Rvalue may bind to LValue const reference

In C++11:
RValue reference - T&& (C++11). They behave like LValue references. The goal is to have a moving candidate.

Rvalue may bind to a non-const rvalue reference. Lvalue may not bind to an rvalue reference.

**Important rule: move from lvalues ​​is never executed. It is copied.** The construction `void f(T&&)` takes precedence over `void f(T&)` if both can be called.

C++11 considers `noexcept` - calling any destructor, memory allocation. Move self to self - usually not checked because this is not normal behavior.

## The first scary thing
The move constructor should be written carefully. The fact is `T&&`, although there is an rvalue reference,
in the context of the body that `T&& x` see, x is already an lvalue. The most confusing thing about C++11.

Therefore, for example, in the initialization list in ctor, you need to write `Base(std::move(rhs))`.

`std::move` - turn any lvalue expression into an rvalue reference. `std::move` could be called rvalue_cast. In fact std::move() does not move anything. Simplified implementation:
```cpp
template <typename T>
T&& move(T& x) noexcept { return static_cast<T&&>(x); }
```

## The second scary thing
There is a special construction `T&& Param` Definition in the template the rule is valid only for constructions of the form
```cpp
template <class T>
void f(T&& arg)
{}
```
That construction is processed by special rules:
arg is Lvalue => deduced to `void f<T&> (T& arg)`
arg is Rvalue => deduced to `void f<T> (T&& arg)`

Universal reference(Term by Skott Mayers) binds everything:
```cpp
template <class T>
void f(T&& arg)
{}
```

* std::move - unconditional reference value cast.
* std::forward - conditional cast for universal references (universal references -- no official term, coined by Scott Myers)

# Virtual and Polymorphism in C++

## General rules from C++03
To get runtime polymorphic behavior, the member functions must be `virtual`, and objects must be manipulated through pointers or references. 

For a function to behave "virtually" its definition in a derived class must have the same signature as it has in
the base class. The only exception is for the return type that should be the same or as described below. The derived class version of a "virtual function" may return a pointer or a reference to a more specialized type than the base. The technical term used in relation to these return types is *covariance*. [4, p.576].

When you're calling a function using the scope resolution `operator::` that ensures that the virtual mechanism built in the language **is not using**. This call will be resolved at compile time.

When manipulating an object directly (rather than through a pointer or references) and its exact type is known by the compiler, then, in that case, runtime polymorphism is not needed, and the call will be done without using vptr's.

A virtual function invoked from a constructor, or a destructor reflects that the object is partially constructed.

## Override (from C++11)
The **override specification** of a virtual function guarantees that you have not made any mistakes in the function signatures at the time of writing. It safeguards you and your team from forgetting to change any existing function overrides when the signature of the base class function changes.

The use of override is optional, but being explicit allows the compiler to catch mistakes, such as misspellings of function names or slight differences between the type of virtual functions.

So it can be a situation when the function is intended to override something, but due to a mistake, it is a new virtual function. But in the case of, using `override` will remove this problem. Better to not repeat virtual in a derived class, but if you want to be explicit, use `override`. B. Stroustrup:
*"That it’s illogical that virtual is a prefix and override is a suffix. This is part of the price we pay for compatibility and stability over the decades".*

Curiously, override is not a keyword; it is what is called a contextual keyword. E.g. It can be used as an identifier."

```cpp
struct Base
{
    Base(){puts("Base()");}
    Base(const Base&){puts("Base(const Base&)");}	
    virtual void f(){} // declare functions in a base class that can be redefined in each derived class
    virtual void g(){} // declare functions in a base class that can be redefined in each derived class
};
 
struct A: Base
{
    A(){puts(__func__);}
    A(const A&a): Base(a) {puts("A(const A&)");}
    virtual void f(){} // By default, a function that overrides a virtual function itself becomes virtual
    void g(){}         // By default, a function that overrides a virtual function itself becomes virtual
};
 
struct B: Base
{
    B(){puts(__func__);};
    B(const B& b) : Base(b) {puts("B(const B&)");}
   // Better to not repeat virtual in a derived class, but if you want be explicit use "override"
   // final provides prevent further overriding
   void f() override final {}	
   int override = 7;
};
```

## Final specification
The **final specification** prevents a member function from being overridden in a derived class. This could
be because you want to limit how a derived class can modify the behavior of the class interface. There is no contradiction in combining override and final. This states that you disallow any further overrides of the function you are overriding. [5, p.578]. 

It is also possible to specify an entire class as **final**.
That will enforce that no further derivation from the final class is possible.

A function's access specifier determines whether you can call that function. It plays no role whatsoever, though, in determining whether you can override it. 
The consequence is that you can override a private virtual function of a given base class.

## Connection of virtual function with default values.

If you call the function through a base pointer, you will always get the default argument value from the base class version of the function. Any default argument values in derived class versions of the function will have no effect.

# Miscellaneous Features of C++11

1. `emplace_back` - construct object directly in place in memory of the container
2. `vector::shrink_to_fit` method
3. `noexcept` specification - like throw() specification for functions from C++98, but it allows more optimization
4. `static_assert(expr)`. A special declaration that results in a compilation error if the constant expression expr evaluates to false.
5. `alignas` operator from (C++11) enforce alignment. `alignas` allocates an object with the requirement to allocate it with alignment suitable for another type. Example:
```cpp
alignas(int) char buff[1024]; 
```
6. `alignof(x)` - alignment operators built into the language. Example:
```cpp
  std::cout << alignof('c');     // print alignment for char's
```
7. Default Member Initializers (C++11). 
When a class data member is defined, we can supply a default initializer called a default member initializer. The default value is used whenever a constructor doesn't provide a value. This simplifies code and helps us to avoid accidentally leaving a member uninitialized.
```cpp
class X {
  int i = 4;
  int j {5};
};
```

8. User-defined literals or UDLs (C++11). Unsurprisingly, literals with user-defined suffixes are called user-defined literals or UDL.
```cpp
long double operator "" _w(long double);
int main() {
    1.2w; // calls operator "" _w(1.2L)
}
```

9. `[[noreturn]]` attribute. Placing [[noreturn]] at the start of a function declaration indicates that the function is not expected to return. Example:

```cpp
struct S { 
[[noreturn]] virtual inline auto f(const unsigned long int* arg)-> void const {}
};

[[noreturn]] void exit(int); 
```

10. Anonymous unions
```cpp
  union {
     float f;
     uint32_t d;
  };
  f = 3.14f;
```

11. Type Alias.
Starting from C++11 there are "Alias Templates" or "Smart Typedefs". Using declarations can now be used for "partially bound" templates:

```cpp
// Usual namespace alias from C++98.
namespace AA = std;

// Usual typedef
typedef AA::vector<int> VecInt1;

// Alias for bind some types. From C++11
using VecInt2 = AA::vector<int>;  

template <class T>
using MyAllocVec = std::vector<T, MyAllocator>; 
// MyAllocVec is alias template
```

They cannot be partially specialized and can be used wherever `typedef` is used.

12. Interestingly, that `static` local variable in C++11 **garantees thread-safe initialization**. It was not the case in C++03. So static variables local variables are guaranteed to be initialized only once,

13. Delegating constructors. This constructor calls the previous constructor in the initialization list.

14. Starting with C++11, destructors are normally implicitly `noexcept`. Even if you define a destructor without a
`noexcept` specification, the compiler will normally add one implicitly [4,p.635].

# Miscellaneous Features of C++14

1. ```[[deprecated]] attribute (C++14)```
This indicates that the use of the name or entity declared with this attribute is allowed, but discouraged for some reason. Compilers typically issue warnings. For example:
```[[deprecated]] void func(int);```

2. Return Type Deduction
```cpp
auto f() {
   return 42;
}
```

3. Binary Literals.
In C/C++ you can use decimal literals (`123,456`), hexadecimal literals (`0xFF, 0Xff`), and octal literals (`071`). Starting from C++14, there is support for Binary Literals. You can write a binary integer literal as a sequence of binary digits (0 or 1) prefixed by either `0b` or `0B`.

```cpp
unsigned char a = 0b00110011;
```

4. Variable templates. Example:
```cpp
template<class T>
inline constexpr T pi = T(3.14159)
```

5. Delimiter inside numeric literals. You can use the single quote character. Example:
```cpp
long long d {10'000'000LL};
```

6. C++14 has changed the recommended way to create a `unique_ptr`. Now the recommended way is to employ the `std::make_unique<>()`.

# Miscellaneous Features of C++17

1. Structured Binding (C++17)
```cpp
struct Entry {  
   string name;   
   int value; 
};
auto [n,v] = read_entry(is)
```

The `auto [n,v]` declares two local variables n and v with their types deduced from read_entry() return type. This mechanism for giving local names to members of a class object is named a structured binding.

2. Deduce template parameters from constructor arguments.
```cpp
// Example program
#include <iostream>
#include <string>
template <class T>
class A {
public:
    A(T arg)
    {
      (void)arg;
    }
};
```
Starting from C++17 it's possible to just write `A a(123);` instead of `A<int> a(123)`. Before C++17, such a feature was supported only for template functions but not for template classes. That feature is called Class Template Argument Deduction.

3. Compile-Time If (C++17)

Only the selected branch is instantiated via using some compile-time expression. This solution offers optimal performance and locality of the optimization.

```cpp
// Example program
#include <iostream>
#include <string>
#include <type_traits>
template<typename T> void update(T& target) 
{
 if constexpr(std::is_pod<T>::value)         
    simple_and_fast(target); // for "plain old data"     
 else       
    slow_and_safe(target);   // ... 
}

int main() {
   return 0;
}
```

4. The new macro `__has_include ` to test that header file is presented. Example of usage: `#if __has_include(<optional>)`.

5. C++17 introduces byte type to work directly with bytes `std::byte` defined in `<cstddef>`.

6. In C/C++ language in `switch` construction, if not explicitly use `break` instruction, instruction flow will fall through after the first `case` statement without reevaluating the predicate. The C++17 added a language feature to signal to the compiler and the person reading your code that you are intentionally using a fallthrough. Example:
```cpp
switch (number)
{
case 1:
 ;
 [[fallthrough]];
case 29:
case 78:
 ;
 break;
//...
}
```

7. *Initialization Statements in if/switch/range-based for.*
The syntax for define local variable and consequence `if` statement was so common enough that in C++17 have been added a specialized syntax for it. 
```cpp
if (auto my=2; my >= 1 || lower <= 2) {
  ;
}
```
The same syntax has been added for `switch` statement.
```cpp
switch (initialization; condition) { ... }
```

```cpp
for ([initialization;] range_declaration : range_expression)
 // loop statement
```

8. The `std::optional` is a class template, just like `std::vector`. The optional object optionally contains a value. To check that `std::optional` has value in it, you have three ways:
* convert the `optional` object to a bool.
* call the `has_value()` member function.
* compare the `optional` object to `std::nullopt`.


9. The type `std::string_view` has been introduced in C++17. It can be used instead of `const std::string&` for input string
parameters. Initializing or copying a string_view is very cheap.
Similar to `std::string_view` there is a `std::span<const T>` that can be used instead of `const std::vector<T>&`.

10. Inline variables. Inline variables have been supported only since C++17.
```cpp
class Objects
{
 static inline size_t s_object_count {};
};

class ObjectsOld
{
 static size_t s_object_count;
};

// somewhere in cpp unit
size_t ObjectsOld::s_object_count;
```

11. The exception specification has been deprecated in C++11 and removed from C++17.

# Miscellaneous Features of C++20

1. `[[no_unique_address]]` attribute allows empty non-static data members to share space with another subobject of a different type.

2. Spaceship operator

The three-way comparison operator denoted `<=>` is a new comparison operator. It's the informal name: spaceship operator.
The term "spaceship operator" was coined by Randal L.Schwartz because it reminded him of the spaceship in the 1970s text-based strategy video game Star Trek. [4,p.100].

```cpp
operator <=>(const Y&)
```
After defining what is called spaceship operator compiler generates based on that various s (<, >, <=, >=), comparison operators automatically.

The `<=>` operator can return one of the following return types:

* std::strong_ordering. It's a enumeration type of available values - std::strong_ordering::less, std::strong_ordering::greater, std::strong_ordering::equal. In mathematical sense it should be used when relation is totally ordered.

* std::partial_ordering. It's a enumeration type of available values - std::strong_ordering::less, std::strong_ordering::greater, std::strong_ordering::equivalent, std::strong_ordering::unordered.

* std::weak_ordering. It's a enumeration type of available values - std::strong_ordering::less, std::strong_ordering::greater, std::strong_ordering::equivalent.


3. `[[likely]]` and `[[unlikely]]` attributes are applicable for `case` branches in the switch statement to give a compiler a hint to optimize certain branches.

```cpp
switch(value) {
  case 1:
    break;
  [[likely]] case 2:
    break;
}
```

4. `std::format()` to replace sprintf and ostringstream. After importing C++20 <format> module, you can use `std::format` in the following way:
```cpp
std::cout << 
  std::format("diameter required for {} is {:.2f}.\n", x, y);
```

Slightly simplified general form of the format specifiers is the following: `[[fill]align][sign][#][0][width][.precision][type]`.

5. Compile time information about current source file `source_location::current()`. Defined in `<source_location>`.

6. Attribute `[[nodiscard(reason)]]` applied for function and describes the consequence of discarding the return object from the function call.

7. Starting from `C++20`, there is only one signed integer representation, and it's twos-complement-notation.

8. Staring from C++20, the template function can be written a bit shorter. That syntax is called "Abbreviated Function Templates". If you want your template to instantiate functions where multiple parameters have the same type or related
types, you still have to use the old syntax. It is so because every occurrence of `auto` in the function parameter list of an abbreviated function template introduces an implicit, unnamed template type parameter.

```cpp
template <typename T>
T sqr(T x) { return x * x; }

// Abbreviated Function Templates
auto sqrNew(auto x) { return x * x; }
```

9. If you overload `operator ==` C++20 compiler automatically generates `operator !=`.

10. From C++20 the right-shift on signed integral types is an arithmetic right shift, which performs sign-extension. It's not an undefined behaviour.

# Modules (from C++20)

Standart `#include` preprocessor directive helps organize project but at a considerable cost. The desirability of modules due to B.Stroustroup was already well known in 1980.

Modules will come from C++20 to upgrade the understanding of header files. And there are reasons to include it in standards.B.Stroustroup mentions two things:
- Google reports x2-4 improvements in compile-time
- Microsoft reports x5-x50 times improvements in compile time

Modules result in reduced compilation times. The order in which you import modules never matters.

The C++20 has introduced the mechanism to form self-contained
subcomponents of related functionality, called a module. Important conceptual things:

* A module can *export* any number of C++ entities (functions, constants, types, and so on)
* An exported entity by one module can be used in any source file that *imports* that module.
* A module can *export entire other modules*. 
* The combination of all entities that a module export is called the *module interface*.

In real life compiler is not yet fully supported modules (At the moment of 2022), so please be careful.

Modules usage has many features so that we will go example by example.

## Single Module Interface File/Module Unit

```cpp
// math.cppm.
// There is no consensus yet on what file extension to use for module files.
// *.cppm is c++ module file/module unit.

// 1. At the start of every module file is a module declaration
export module simple;
// 2. "export module ..." means that this is module interface file
// 3. Within a module name you may use dots to string together multiple identifiers. Module names are the only names in C++ in which this is allowed.
// 4. All import declarations must appear after the module declaration 


// 5. To export an entity from a module, you simply add export.
export auto square(const auto& x) { return x * x; }
export enum class Oddity { Even, Odd };
export auto getOddity(int x) 
{ 
  return isOdd(x) ? Oddity::Odd : Oddity::Even; 
}
// 6. Only module interface files may contain export declarations.

// 7. You can also export multiple entities all at once by grouping them into export block.
export
{
  const double a{ 1.2 }; 
  const double b{ 1.5 }; 
}

// 8. Module-local function (not exported)
bool isOdd(int x) { return x % 2 != 0; } 
// 9. Only entities that are exported by a module can be used in files that import the module
```

## Module Interface File With Implementation inside it
First of all you may delcare export symbols and implement them inside module interface file.
```cpp
export module simple;
export // The module's interface
{
 auto square(const auto& x);
}

// The implementation of the module's functions
auto square(const auto& x) { return x * x; }

// You can, but you do not have to add export
// Still valid:
// export auto square(const auto& x) { return x * x; }
```
## Module Interface File With Separate Implementation

The module interface file then includes the prototypes of all exported functions. Their definitions, along with any
module-local entities can be moved to one or more *module implementation files*.

In a module file, all import declarations must appear after the module declaration and before any other.
```cpp
// mymodule.cppm – Interface test file
export module mymodule;
import <string>;
export std::string to_string(unsigned int i);
```

```cpp
// mymodule.cpp – Interface implementation file

// 1. Unlike module interface files, a module implementation file does not begin with the export keyword. 
// 2. You are not even allowed to repeat the export keyword here in front of the definition of to_string
module mymodule;
import <string>;
std::string to_string(unsigned int i)
{
  return std::to_string(i);
}
```
Every module implementation file implicitly:
* Imports the module that it belongs to.
* Gains access to all declarations, even those that are not exported. [5,p.396]

## What you can not define in a module implementation file
Some entities must always be defined in a module interface file:

1. The definitions of all exported templates,
2. A function definition with `auto` return type deduction. For auto return type deduction to work, the compiler needs the function definition to be part of the module interface.

## Using Modules

Compiling a module interface creates a binary representation of all exported entities for the compiler to consult when processing files that import the module quickly.

You import the module by `import mymodule;` declaration. You do not put angle brackets around the name of your modules, and add you should use a semicolumn at the end of the expression.

Unlike for header files, the name that you use to *import* a module is not based on the name of the file that contains the module interface. It is based on the name that is declared in the `export module mymodule;` declaration.

After import module, you can (only) use these exported entities. Example:

```cpp
import <iostream>;
import simple;

int main()
{
 std::cout << "a squared: " << square(a) << "\n";
}
```

When you import a module into a file not part of the same module, you do not implicitly inherit all imports from the module interface file. In other words, when you import a module, you do not implicitly gain complete access to all other modules that that module relies on.

If you add export in front of an import declaration in module interface files (E.g. `export import <string>;`), then any file that imports a module implicitly inherits all import declarations that are exported from that module as well.

## Splitting Modules

1. *Simulating Submodules.* C++20 does not formally support the concept of nested submodules, but they can be simulated quite
easily. The possibility to use dot (`.`) in the names of modules allows adapting it to make it easier to see the relation between modules and their submodules. Dots were explicitly allowed in module names to facilitate such hierarchical naming.

2. *Use Module Partitions.* Submodules can be imported
individually by the rest of the application because they are just modules. Module partitions are only visible within a module.
```cpp
// internals.cpp – Module implementation file for the internals partition

// 1. The module declaration of a module partition file is almost similar to that of any other module file
// 2. Except that the name of the partition is added after the name of the module, separated by a colon.
// 3. It is not allowed to export any entities

module mymodule:internals;
unsigned int from_c(char c)
{
 // Same switch statement as before...
}
```

To then use the internals partition and its function in the module implementation file you have to import the partition.
```cpp
// mymodule.cpp – Implementation
module mymodule;

// Module partitions can only be imported into other files of the same module, and only using import :partition_name;
import :internals;

unsigned int from_abc(std::string roman)
{
  // Use from_c(char) from the :internals partition.
}
```

Outside the module, a partitioned module can only be imported
as a whole (through `import mymodule;`). Individual partitions can never be imported outside of the module.

You can partition Module Interface as well.
```cpp
//a.cppm
export module mymodule:parta;
//...
```
```cpp
//b.cppm
export module mymodule:partb;
//...
```
```cpp
// mymodule.cppm – Primary module interface file
export module mymodule;
export import :parta;
export import :partb;
```

# Templates

1. In addition to type, template parameters include Non Type Parameters, which can have the type of integral constant, reference, and a pointer to a given function. Pointers to data of function must have an external link type. As of C++20, a template parameter can be of any fundamental type (bool, float, int, and so on), enumeration type, pointer type, and reference type. [4, p.380]. The compiler needs to be able to evaluate the arguments corresponding to all non-type parameters
at compile time.

2. You can use `template` to create a specialization for the array with a fixed size.
```cpp
#include "stdio.h"

template<class T>
void p(T a){ puts("not array"); }
//
template<class T>
void p(T a){ puts("not array"); }
//
template<class T, int sz>
void p( T (&t)[sz] ) { puts("array"); }
//
int main(int argc, char *argv[])
{
     intq[3];
     p(q);
     return 0;
}
```
3. Very rarely, but sometimes while using templates inside templates, there is a need for the `template` qualifier is needed in case of difficulty in understanding.
```cpp
template <typename S, typename T>
T* allocate(S& storage, int numberOfElements)
{
     T*res = 0;
     // res = storage.alloc<T>(numberOfElements);
     res = storage.template alloc<T>(numberOfElements);
     return res ? true : false;
}
```
For more info: please view at "B.13.6 template" in Special Edition, Biern Stroustrup.

4. An empty `template<>` is syntactically reserved for explicit specialization and cannot be used to create a template without parameters.

5. A template specialization can be complete (type int), or partial (the type that uses T as the basis for something else). However, the general template must be declared before any partial or complete specialization. Also, partial specialization only works for classes but doesn't work for functions. Example:
```cpp
template <class T>
struct Single
{
  Single() : var(T()) {}
  T var;
};

template <class T>
struct Single<T*>
{
  Single() : var(T()) {}
  T var;
  int extra_for_ptr;
};

template <>
struct Single<int>
{
  Single() : var(int()) {}
  int var;
  int extra_for_int;
};

int main()
{
  Single<int> a;
  a.extra_for_int = 1;
  Single<int*> b;
  b.extra_for_ptr = 1;
  
  return 0;
}
```

## Template syntax remarks
When instantiating a template, starting from C++11 not necessary to make a space in `>>`. In the case of specifying an integral type in a template parameter and wishing to perform right-shift `>>`, you should enclose the expression in parentheses starting from C++11. 

Example of using `>>`:
```cpp
template <class T, int size>
class AA
{};
AA<std::vector<int>>, 2> obj;
```

Derivation of the template from the list of function arguments
from longer to shorter form A->B->C. On the complex rules of the admissible derivation of template arguments, functions see [1], 13.4.

```cpp
template <class T>
void swap(T* a, T* b)
{
   Ttemp = *a;
   *a = *b;
   *b=temp;
}
//A
template<>
void swap<float>(float* a, float* b)
{
   float temp_temp = *a;
   *a = *b;
   *b = temp_temp;
}
//B
template<>
void swap<>(double* a, double* b)
{
   double temp_temp = *a;
   *a = *b;
   *b = temp_temp;
}
//C
template<>
void swap(int* a, int* b)
{
   int temp_temp = *a;
   *a = *b;
   *b = temp_temp;
}

int main()
{
   int a = 0, b = 0;
   swap(&a, &b);
   return 0;
}
```

Default template arguments type must occur at the end for class or variable template. However, for function templates, it's not a requirement because, for functions, there is a rich type deduction template mechanism.

For compilation purposes, you may want to request explicit template instantiation. Explicit instantiation of a class template instantiates all members. It's possible to instantiate only individual template class member functions too.

Example of syntax:
```cpp
template class MyVector<int>;
template void f<int>(int&);
template void g(double&);
template void MyVector<int>::size();
```

Also, one more complication - there must be exactly one definition of the corresponding specialization. So if you instantiate a template explicitly in one translation unit, you should not explicitly instantiate it in another.
Example of syntax:
```cpp
extern template class MyVector<int>;
extern template void f<int>(int&);
extern template void g(double&);
extern template void MyVector<int>::size();
```


Let's assume you define template class Array, e.g. in the following way:
```cpp
template <typename T>
class Array
{
public:
  explicit Array<T>(size_t size);
  ~Array<T>();
  Array<T>(const Array<T>& array);
private:
  T* m_elements; // Array of type T
  size_t m_size; // Number of array elements
};
```

Using the complete(full) template identifier within a template definition scope is not essential. So the following is the legal code:
```cpp
template <typename T>
class Array
{
public:
  explicit Array(size_t size);
  ~Array();
  Array(const Array& array);
private:
  T* m_elements; // Array of type T
  size_t m_size; // Number of array elements
};
```
The same is applied during template class member definitions. After name resolution operator `::` you don't need to repeat the full template class specification. [4, p.638]
```cpp
template <typename T>
Array<T>::Array(size_t size) 
: m_elements {new T[size] {}},m_size {size}
{}
```

## Variadic templates
The motivation is to have the ability to work with a varying number of template parameters. The smallest example:
```cpp
template <class T...>
void f(const T&...arg)
```

Example of performing printf in variadic template style:
```cpp
template<typename T, typename... Args>
void printf(const char *s, T value, Args... args)
{
    while (*s)
    {
        if (*s == '%')
        {
            if (*(s + 1) != '%')
            {
                std::cout << value;
                s += 2;
                printf(s, args...);
                return;
            }

            ++s;
        }

        std::cout << *s++;
    }    
}
```

**First thing:** In variadic template for ellipses `...` you can put spaces anywhere around it. And `...` are used in fact, for various purposes.

**Second thing:** the only way to get the next template argument is to recursively call a function whose template parameters are specified as ```<TExtractType, RestTypes...>```. So if you have ever seen functional programming languages, that construction looks pretty close to that.

* `class ...Args` - parameters pack in template parameters list with optional name.
* `(Arg&&....params)` - function arguments parameters pack.
* `Args...` - unpack parameters. Used inside the body of th function.
* `sizeof...(Args)` - sizeof of parameters in terms of number of elements in Args. (It'not the size in bytes).

Variadic templates has been introduced in C++11, the last trick with variadic template is called *fold expression* has been introduced in C++17. Unary syntax for fold expression:
```cpp
template<typename... Args>
bool allLeftFold(Args... args) { return (... && args); }

template<typename... Args>
bool allRightFold(Args... args) { return (args&& ...); }
```

## Reference Collapsing Rules
In C++ you can not declare a reference to reference, but when reference collapsing occurs during template types substitution, there are the following rules:

`T&&` => `T&` - valid from C++03

`T&, &&` => `T&` - valid from C++11

`T&&, &` => `T&` - valid from C++11


`T&& T&&` => `T&&` - valid from C++11

So the C++ standard allows reference collapsing in templates. Example:
```cpp
template <class T>
void f(T& val)
{
val = 0;
}

int i = 0;

// during compiletime 
// f<int&>(int&&) => converts into => f<int&>(int&)
f<int&>(i); 
```

# Variants of Casting 

`const_cast` - removes `const` and `volatile` modifiers from a pointer.

`static_cast` - casting one type to another using standard or user-defined conversions.

`dynamic_cast` - the argument to dynamic_cast can be a null pointer - the result of this operation is a null pointer. The argument to dynamic_cast must be a polymorphic type. This requirement simplifies the implementation. The result of dynamic_cast need not be a polymorphic type. If it is impossible to understand what the type needs to be converted to (diamond-shaped inheritance with duplicates), a null pointer will be returned. It will also return a null pointer for the simpler base case when casting is failed.

`reinterpret_cast` - force casting instructions

`C-style type casting` - tries to use static_cast, if not, uses reinterpret_cast. Further, if necessary, uses `const_cast`. 

**Private inheritance** - in addition to the invisibility of variables by the user of the derived class of members of the vase class, also does not allow the use of implicit type casting.
```cpp
struct A{int a;};
struct B:private A{int b;};

int main()
{
  B b;
  { A& ba = b;     }  // error
  { A& ba = (A&)b; }  // ok    

  return 0;
}
```

# Concepts (from C++20)

## Define Concepts

A concept is a named set of requirements. It's possible in general, to distinguish three categories of requirements [4,p.512]:
* Syntactic requirements. Some expressions should be compilable.
* Semantic requirements. 
* Complexity requirements.

The only requirements that we can express with C++ concepts are syntactic ones. Explicitly specify any and all non-obvious semantic and complexity requirements of a concept right now should be done in the form of code comments or other documentation. First, let's describe example how concepts are defined:

```cpp
template <typename T>
concept Small = sizeof(T) <= sizeof(int);
```

1. Concepts are never instantiated by the compiler. They never give rise to executable code. 
2. Concepts should be seen as functions that the compiler evaluates at compile time to determine whether a set of arguments satisfies the given constraints.
3. A *constant expression* is any expression that the compiler can evaluate at compile time. 
4. The constraints in the body of a concept definition are logical expressions connected with `&&` or `||`.


You can define concept in terms of another concepts. Example:
```cpp
template <typename I>
concept Integer = SignedInteger<I> || UnsignedInteger<I>;
```

So concept is defined in the following way:
```cpp
template <parameter list>
concept name = constraints;
```
Next, to express the actual syntactical requirements of a **concept** you should use require expression.
```cpp
requires { requirements }
requires (parameter list) { requirements }
```
All the compiler does with requirements is check whether they form valid C++ code or not. The body of a requires expression consists of a sequence of requirements. Each requirement ends
with a semicolon and is one of the following types:

* **A simple requirement.** 
Example:
```cpp
template <typename Iter>
concept RandomAccessIterator = BidirectionalIterator<Iter>
 && requires (Iter i, Iter j, int n)
 {
   //int n; // Error: not an expression
   i + n; i - n; n + i; i += n;
   i < j; i > j; i <= j; i >= j;
 };
```

A simple requirement consists of an arbitrary C++ expression statement and is satisfied if the corresponding
expression would compile without errors. All variables you use in these expressions must either be global variables or variables introduced in the parameter list. You cannot declare local variables in the usual way.

* **A compound requirement.**
Example:
```cpp
template <typename T>concept NoExceptDestructible = requires (T& value) { { value.~T() } noexcept; };
```

A compound requirement is similar to a simple requirement; only 
besides asserting that a given expression must be valid, a compound requirement can also prohibit this expression from ever throwing an exception and/or constrain the type that it evaluates to. There is no semicolon after the expression inside the curly braces of a compound requirement. There is no semicolon after the expression inside the curly braces of a compound requirement. All possible types of compound requirements:
```cpp
// expr is a valid expression
{ expr };
// expr is valid and never throws an exception
{ expr } noexcept; 
// expr is valid and its type satisfies type-constraint
{ expr } -> type-constraint;
{ expr } noexcept -> type-constraint;
```

* **A type requirement and nested requirement.** Example:
```cpp
template <typename S>
concept String = requires
{
 typename S::value_type;
 requires Character<typename S::value_type>;
}
```

## Use Concepts

The general outline for a constrained template thus becomes as follows:
```cpp
template <parameter list> requires constraints
template body;
```
Example of using concept to restrict template using:
```cpp
template <typename T> 
requires MyConcept<T> && std::destructible<T>
const T& function(const T& a, const T& b) 
{ return a > b ? a : b; }
```

Starting from C++20 there is a shorthand notation for using concept:
```cpp
template <MyConcept T>
const T& function(const T& a, const T& b) 
{ return a > b ? a : b; }
```

# Coroutines (C++20)
The execution of function includes the ability to peform the following:
* created stack frame
* execute function
* return value
* delete stack frame

The Coroutines conceptually the same as functions, but they allow two extra actions:
* suspend execution.
* resume execution.

Coroutines in some sense are stackless they reuse stack frame of the caller.

`co_return` - return from coroutine. The `return` statement is prohibited in coroutine. Example:
```cpp
task<int> func(int a, int b)
{
  co_return x;
}
```
`co_await` - suspend coroutine while waiting for another computation to finish.

`co_yeild` - returns a value from coroutine to the caller. Suspend execution of coroutine, until subsequently calling the coroutine.

To execture coroutine until it's not ready:
```cpp
task<int> x = func(1,2)
while (!x.is_ready())
  x.resume();
return x.result();
```

# References

[1] The C++ Programming Language Special Edition, B.Stroustrup

[2] The C Programming Language, Harbison Steel

[3] The continuing evolution of C++. Bjarne Stroustrup https://www.youtube.com/watch?v=ooehrkYkGdA

[4] Beginning C++20. From Novice to Professional. Sixth Edition. Ivor Horton, Peter Van Weert.

[5] C++17 Standard Library Quick Reference. Peter Van Weert and Marc Gregoire.

[6] C: A Reference Manual, 5th Edition 5th Edition. Samuel Harbison, Guy Steele Jr.
