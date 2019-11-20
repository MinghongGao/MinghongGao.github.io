---
layout: post
title: Software Testing - Review
---
## Week 1 - 1

What is software testing and why do we do it ? 

* For finding errors and incresing confidence that there are no errors
* Ensure software meets specification
* Software is robust
* Protect against vulnerabilities
  What is a successful test case ?
* Tests that didn't pass!




## Week 1 - 2

**Equivalence partitioning:** set of tests in which each element is as good as each other for the purpose of test
**Properties:**

1. Coverage: the union of all equivalance classes = input domain
2. Disjoint: a single test belongs to only 1



## Week 2 - 1

Input domain 
Equivalence Tree
6 guide lines 

## Week 2 - 2

boundary shift(boundary fault)  -> Boundary Analysis

## Week 3 - 1

### Control Flow Testing

Control Flow Graph 
Criteria:

* **Statement Coverage:** Every statement should be exercised at least once
* **Branch Coverage (or Decision Coverage):** Every alternative in a branch should be exercised at least once
* **Condition coverage:** Each conditon in a branch condition is made to evaluate to TRUE and FALSE at least once. E.g `if (a && b)`, a must evaluare to True and False at least once, and so must b.
* **Decision-Condition Coverage:** Combination of branch and condition coverage
* **Multiple-Condition Coverage:** All possible combinations of condition outcomes within each branch should be exervised at least once.
* **Path Coverage:** Every execution path of the program should be exercised at lease once. In other words, all possible combinations of branch condition outcomes should be exercised at lease once.
  > **Path coverage (cont)**: loops have infinite number of paths. Thus, often choose a boundary number (N) of times a loop can be executed and then test it up until N.

Branch Coverage - > Statement Coverage

## Week 3 - 2

### Data Flow Testing

**Definitions:** A statement defines a variable by assigning value to the variable, e.g., x = 5, scan(x)
**Reference:** A statement makes a reference to a variable either as an:

* L-value: a value is stored to the variable, e.g., x=5
* R-value: get value of a variable, e.g., ... = 3 * x
  **Undefine:**  A statement undefines a variable whenever the value of the variable becomes unknown, e.g., when scope of a local variable ends. 

Data flow anomalies
**U-R anomaly:** occurs when undefined variable is referenced, e.g., Object A;....; B = A;
**D-U anomaly:** occurs when a variable is defined but not referenced before it becomes undefined. This usually indicates that wrong variable has been defined/undefined.
**D-D anomaly:** occurs when a variable is defined twice before it is referenced.
**Notes:** compilers have options to detect these

### Data Flow Graph

* $d_n(x)$(define): e.g., x=5
* $u_n(x)$ (use/reference): e.g., y = x + 1
* $k_n(x)$ (kill/undefine): e.g., free(c)
* $c_n(x)$ (computational use): e.g, ... = x * 3
* $p_n(x)$ (predicate use): e.g., if(x>2)
  > Data flow graph is a control flow graph annotated with data notaions attached to each CFG node.

A **definition clear path p** with respect to a variable x is a sub-path of the control-flow graph where x is defined in the first node of the path p, and is not defined or killed in any of the remaining nodes in p.
A **definition $d_m(x)$ reaches a use $u_n(x)$** if and only if there is a sub-path p  that is definition clear(with respect to x, and for which m is the head element, and n is the final element)

**Coverage-based Criteria**
**All-Defs:** test at least one path from the single definition of a variable to at least one use of it
**All-Uses:** test paths traversing from definition of a variable of all uses reachable from the definiton.
**All-Du-Paths:** test all definition clear paths for all DU pairs  

Control Flow Testing wouldn't be enough. Remember the division by zero example?

Data Flow Testing is to complement by testing the effect of data flowing through the whole program

## Week 4 - 1

### Dynamic Data-Flow Analysis



## Week 4 - 2

### Mutation Analysis

Couping Effect:

* If test suite finds small faults, then it will find larger faults

1. Make X copies of the program
2. Insert 1 small syntacyic change into each copy
3. Run test suite of all X fault versions
4. Mutation Score = #kill/#total mutants(X)
5. Find unkilled mutants, **determine if they are equivalanet(Hard)**, and if not, add tests to kill them

  Equivalent mutants:

* Return x --> Return x++

Not all mutants can be killed

## Week 5 - 1

### Modular Testing

**Observability**

* It's hard to see whether our test is correct or not
* There is not way to observe what's going on

**Controllability**

* We got test we would like to run, but it's difficult or impossible  to actually control our system to get into the state we find interest

**Relation**
High Observability + high Controllability -> Easier to see the effect of tests

Low Observability + high controllability -> Harder to see the effect of tests
Observability + Controllability = Testability
**Example:**
Web Applications are hard to observe and control

**Roles**

* initializer
* Transformer
* Observers

Using finite state machine to model our tests 

* **state coverage:** at least one test for each state
* **Transition Coverage:**  at least one for each transition
* **Path coverage:** 

## Week 5 - 2

### Object-oriented testing

Polymorphism

* Effectively share tests for super classes


## Week 6 - 1

Test oracles
The output of the program should be

* a program
* a process
* a body of data
* that determines if actual output from a program has failed or not

Types of oracle:

* Human oracle
  		+ using human knowledge
  		+ flexiable but least efficient
* Alternate implementations (golden program)
  		+ Previous implementation
* Real data, solved examples
* Heuristic oracles

BinarySearch oracle:

* Compare to a linear search (what if target is at multiple locations?\*\**)
* Another BinarySearch
  		+ people tend to make same errors
* Construct input so that we know the location of the target
* index =  binarySearch(list, target), if index >= 0 Assert(list\[index] == target) else index = -1

Categories of oracle:

1. Active Oracle: Given the input, can tell what the output should be. And finally compare them -- replicates behaviour(always exist)
2. Passive Oracle:  Given input and output,  then tell if it's correct or not. -- only checks behaviour(non-determinisim works wel, needs to have good relation between input and output, not always exist)

Metamorphic oracle

## Week 6 - 2

## Week 7 - 1

Difference between ordinary program testing and security testing:

**Program Testing:** seeks to uncover program **_faults_**, exhibited by failures: when the program’s observable behaviour differs from what it was intended or required to do.

**Security Testing:** seeks to uncover security **_vulnerabilities_**: typically extra functionality that allows an attacker to do something unwanted.

> Something unwanted:
>
> 1. Causing the program to crash: availability
> 2. Causing the program to corrupt data: integrity
> 3. Causing the program to reveal sentitive data: confidentiality
> 4. Causing the program to take excessive amount of time to execute: availability and performance
> 5. Causing the program to execute attacker-contolled functionality

Vulnerability

* Fault
* Unintended Functionality
  * SQL Injection
  * Buffer Overglow

C Stack and Memory

Fuzzing

Fuuzer--(generate inputs and feed)--> Program under test

x y 
3 1

## Week 7 - 2

Checksums and Codes
crc32 - packet body

* check the integrity of the packet
  Parsing Stack

Mutation Based Fuzzing

* partial knowledge
* somewhere In between randromly and with good knowledge(genration based fuzzing) 
* Heuristic-Based Mutation
* Success Depends on
  		 + good quality inputs to mutate
  		 + good heutistics to choose how to mutate these inputs

Generation Based Fuzzing

Fuzzing techniques

* Coverage
  		+ Generation > Mutation > Simple ("Dumb") Fuzzing
* Difficulty to Implement (required knowledge of data format):
  		+ Generation > Mutation > Simple Fuzzing

Memory Debuggers

* Catch
  		+ Out-of-bounds accesses to memory
  		+ Use-after-free
  		+ Double-free and Invalid-free
  		+ Memory leaks
  		+ Accesses to uninitialised memory

Undefined Behaviour

* overflow(signed integer and floating number)

## Week 8 -1

Confidentiality

Overt Channels

* openssl
* cloudbleed

Implicit (Covert) Leakage

* Timing

## Week 9 - 1

Symbolic Execution

* to prove
* use symbols
* We did two things
  		+ Simplification
  		+ Entailment

Constraint Solvers

* variables, each with a domain
* Relationships between variables
* If a set of constraints satisfiable?
* What is a solution
* Do one set of constraints  entail another?

Test Oracles

* assert statements
  		+ also custom program annotations
* memory-safety violations:
  		+ out-of-bounds memory accesses
  		+ Null-pointer dereferences
  		+ etc.
* undefined behaviour
  		+ signed integer overflow
* golden program
  		+ compare generated constraints on output	

## Week 10 - 1

Limitations

* Path explosion
  		+ one condition -> double the branches
* Constraint Solving
  		+ Constraints get too large as programs get larger
  		+ Analyse per-function
  			+ But misses inter-function dependencies
* Unsolvable constraints
  		+ External Calls
  			+ `x = some_func();`
  		+ Non-linear
* Loops
  		+ Troublesome for proofs

Dynamic Symbolic Execution
Combination of Fuzzing and Symbolic Execution

* **Simultaneously** execute both concretely and symbolically
* Then **negate path constraints** obtained symbolically to **generate new inputs** to take different paths
* Combine the advantages of both:
  		+ random testing
  		+ symbolic execution
* However, is best for finding bugs rather than for doing proofs

Disadvantage:
	Divergence: when a new test we generate takes a different path to the one we expect

Finish of Security Testing

Reliability Block Diagrams

* Failure and Reliability
  		+ Reliability: probability that component doesn't fail (over some period)
  		+ F(C): Probability that component C fails during the time period
  		+ R(C): Component C's reliability
  			+ R(C) = 1- F(C)

Failure: Serial Block

* one fail -> other fail

Failure: Parallel Block

* one fail does not lead to whole fail

## Week 10 - 2

Reliability - Random Testing
**Definition**: **Reliability** is the probability that a system will operate without failure for a specified time in a specified environment

**Definition**: A **failure** is the departure of the results or execution of a program from its requirements

* program crash
* incorrect output
* response time too slow
* etc.

Operational Profile

* Probability distribution of program inputs, used for random testing to measure reliability
* Captures the program's expected environment
* Includes:
  		+ The **type** of the input
  		+ **How often** new inputs arrive/ are generated

Random Testing:
Advantages:

* Good simulation of reality, assuming correct operational profile
* Unbiased - free of human bias
* Cheap to generate lots of inputs, necessary for good reliability estimates
* Doesn't need source code i.e. is a black-box technique

Disanvantages:

* Difficult to achieve high coverage
* Difficult to see low-probability failures
* Requires a good operational profile

Why not e.g. control-flow testing to measure reliability ?

* More Expensive than tandom testing
* Doesn't capture reality - Assuming all path is executed with the same probability

## Week 11 - 1

Markov Models
Transition Matrix

* Associativity

## Week 11 - 2

Reliability Growth Models
Failure Intensity

* exponential decay

Simple Execution Time Model

* Models **change in reliability** over time of a program during development
  		+ (e.g. during testing and debugging phase)
  		+ image a program subjected to random testing to detect faults
* **Assumptions:**
  		+ Based on **execution time**
  		+ Program execution **stops when a fault occurs** and is **restarted once  the fault is fixed**
  		+ Removal of each fault lowers the failure intensity by a **constant amount**
  		+ Uniform operational profile

Fault Detection & Failure Intensity
Failure Intensity & Execution Time
Calculating Failure Intensity 

* $\lambda= \frac {1}{Interval}$
* Average Failure Intensity

Failure Intensity vs Faults

* Number of faults: $\mu$
* Intercepts: 
  		+ $\lambda_0$:  initial failure intensity
  		+  $\nu_0$: totals faults
* $\lambda(\mu)=\lambda_0(1-\frac{\mu}{\nu_0})$

Failure Intensity over Time

* $\lambda(\tau)=\lambda_0e^{-\frac{\lambda_0}{\nu_0}\tau}$

![](/images/screenshot-from-2019-11-15-15-39-20.png)

## Week 12 - 1

### Exploting Stack Buffer Overflows

Modern Protection:

* Non-executable stack
* Address Space Layout Randomisation (ASLR)

## Week 12 - 2

Error Seeding
Estimating Total Number of Faults in a Program

* Goal: estimate, N, the total number of faults in a program
* Randomly seed the program with some number E of faults
* Test or inspect the program to uncover some faults:
  		+ Suppose  we find P seeded faults
  		+ Suppose we also find Q unseeded faults
* Assumption: both kinds(seeded and unseeded) faults are equally likely to be found:
  	$$\frac {P}{E} = \frac {Q}{N}$$
  Therefore:
  	$$N = \frac {Q\times E}{P}$$

## Exam

Security Testing:

* Stack Buffer OverFlow 
  		+ Influences and Consequences
* Signed Integer Overflow
* Timing attack(implicit)
