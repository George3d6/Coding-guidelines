# Coding guidelines


## 1. When do I write code

"I hate code, and I want as little of it as possible in our product." – Jack Diederich

### 1.1 Code is bad, never write code

Unless you write it due to immediate benefits coming down the line it's going to be a liability not an asset, it's going to make the project it's part of larger, and, as such, harder to maintain and modify.

* The first exception to the above rule is when prototyping sutff in a new project/fork, that is bound to require code addition, but as long as it doesn't polute any other product it doesn't do any harm.

* The second exception to the above rule is when the code is when, by far, the easiest way to add a feature or fix a problem is writing code

When you are forced to add code to an existing project, try to leave it cleaner than you found it (try to remove some useless or too verbose code, try to remove useless comments, remove unused files or excesive directory structure ...etc). This way adding code to a project will do less damage.

### 1.2 Dependencies are also bad, never add depencies unless it's the only way to avoid writing code

Never add a dependency unless you find yourself in a situation where you'd have to write code in order to not add that dependency (e.g. Do add dependencies for and HTTP server, do not add dependencies for a syntactically prettier version of map)

Further more, when adding a dependency to production code, try to check it's integrity. Look at the dependencies of the dependencies and pick the dependency with the least, most stable and veted dependencies.

* Note: When I say "dependency" here this could be anything from a command line tool in your production environment to a library or a ready to ship codebase.

### 1.3 Whenever you add code or dependencies, review it

This means having code reviews when you add code to the main products and also having code reviews when a new product that you were working on is ready to hit the market.

Humans are very good at reading and writing code, coincidentally they also seem to be decent at checking code for errors, both through higher level logic and semi-automatic pattern recognition. If you have humans at your disposal use them to proof-read the code and suggest improvements.



## 2. How do I write code

### 2.1 Use immutability and constant variables

* A constant variable is one that can't be reasigend to. By default, all variables should be const, declaring a normal variable as a const
can be spotted at compile time, delcaring a const variable withot the modifier can lead to horrible bugs.

* An immutable value is one that cannot change. In certain languages this is the same as constant-ness (e.g. Rust and C++), in others (e.g. Python and Javascript) there are different mechanisms for making a value immutable (e.g. Object.freeze()). Immutable values are good for the same reason constant variables are, further more, they can help the compiler otpimize code and they can be used in parallel code without a lock. As such, use immutable values whenever you can.


### 2.2 Diferentiate between pure and inpure functions

* A pure function is easy to reason about, it's equivalent to a mathematical function. It has a domain D and codomain C and need to be able to map all values from D to the exact same values regardless of the environemnt in which it runs or the values in the program external to the function. If wirtten properly, most pure functions should require no testing (since they are easy to reason about, mathematically if need be) or be very easy to test (since they are self contained). They can also run in parallel easily, since they affect no global state. They also guarantee 100% CPU utilization in most cases (since they include no IO). There's no downside to a function being pure and many upsides, so whenver you modularize code try getting in as many pure functions as possible.

* An inpure function lacks the aforementioned advantages of a pure function. It can throw an exception, return a result, crash the program and acts differently depending on the environemnt. I would further classify these functions into three different categories (which aren't mutally exclusive):
	1. Functions that access external state without modifying it

	2. Functions that access external state and may modify it

	3. Functions that perform I/O (this includes working with shared memory, network memory and pipes)

### Code formatting

* Formatting rules should be encapsulated by a simple config file and formatting tool, otherwise, they are too hard to enforce. For existing formatting rules please see the `formatting` directory.
