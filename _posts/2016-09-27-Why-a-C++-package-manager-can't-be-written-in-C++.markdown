---
layout: post
comments: false
title: "Why a C++ package manager can't be written in C++"
---

Languages for core and UI
--------------------------
As any other computer program, a package manager has both a computing core and a user interface (UI).

The user interface in this case is not a GUI, but some files with a predefined syntax that allow users (programmers) to define, consume, and manage packages. For example, Maven for Java has ``pom.xml`` files, and NPM for node (javascript) has ``package.json`` files.

The computing core takes those files as input, and execute tasks as configured by such input, as fetching files from somewhere on the internet, or building some artifacts locally.


Reasons for Python
-------------------

Using Python as UI language for package definition can be a safe default:

- Python is already being used by many C and C++ developers for scripting. Companies often develop their own dev tools with python too.
- It is a very simple language, even if not previously known, a seasoned C or C++ developer can learn the basics of python very, very quickly. Template meta programming, undefined behavior, concepts, hardcore optimizations and zero cost abstractions, SFINAE, RAII... If learning python is an issue, Houston, we've got a problem.
- Its dynamic, interpreted nature, allows for a friendly and concise syntax for the users.

Of course there are other good options. A very good example is the widely used Homebrew project for Mac OSX, which uses Ruby language both for its UI and its core. Python might still be more popular among C and C++ developers, but Homebrew has proven that the implementation language is not a pre-requisite for success.

Given that python is taken as UI language, using also python for the core could have other advantages too:

- Python, with its simplicity and ecosystem is well known for allowing very fast prototyping and development, which allows quick iteration of the developed tool, quickly fixing bugs, a fast release cycle. 
- Performance of the tool is likely not an issue, when packages of hundreds of megabytes are retrieved from the internet, or full libraries are built locally.
- High python portability to many systems, architectures and platforms, which alleviates a lot of burden from the developers to distribute the tools.

It could be argued that having the core codebase in a different language would refrain potential contributors not knowing python to fix things and contribute features, but the reality in OSS projects is that project maintainers carry most of the development effort, so as long as the above reasons are good for them, the project will benefit from such language decision.


The big fallacy
-------------------

But **NONE** of them is the real reason why a C++ package manager can’t be written in C++. The reason is the big fallacy hidden in the title itself. Having a C++ package manager is a fallacy, such a thing cannot (in a sane mind) exist. 

For good or bad, what can exist are C and C++ package managers. It is not that such a package manager can or will handle packages for both languages separately, but that C libraries are also widely used in C++ projects. OpenSSL and ZLib, are just a couple of C libraries very popular in C++ projects.

This is a typical issue for C++ dev tools, they are rarely just C++ dev tools. CMake is a C and C++ meta-build system, and all popular IDEs, as Visual Studio or CLion handle both C and C++.

Now that this point is clear, we can see that the question “Which language to use in the core of the package manager?” has no good answer. It could be argued that the common denominator is C, and that according to some indexes, it is even more popular than C++. But that would certainly annoy, even infuriate to many C++ developers, and with a reason. Not being able to use many of the high level C++ features and the STL, that many times are absolutely zero-cost and even improve performance, can be frustrating. 

If the selected language was C++, the C developers will also be quite disappointed. There are famous cases as that of Linus Torvalds opinion with regards to C++. Putting language wars aside, it is true that there exist many excellent and useful C projects (linux, git, cpython…), so they cannot be just disregarded in this decision.


Conclusion
-------------------

So while “a C++ package manager can’t be implemented in C++” is true because of the described fallacy, it is possible to say that “a C and C++ package manager can be implemented in C++”. But as we have seen, trying to establish that **a C and C++ package manager must be implemented in C++** as an universal truth is also nonsense, as there is no logic base for such statement. 

So “in which language should it be implemented?”. For us, the above explained reasons clearly outweighed the possible disadvantages. Putting the decision we made months ago in perspective, we are still very happy with it and believe it was the good one: Python provides a unified language both for the UI and core, which users and contributors understand and like, while allowing us to be productive while developing new features, fixing bugs and releasing new versions. 

