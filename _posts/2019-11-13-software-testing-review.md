---
layout: post
title: Software Testing - Review
---
## Week 7 - 1

Difference between ordinary program testing and security testing:

**Program Testing:** seeks to uncover program _**faults**_, exhibited by failures: when the program’s observable behaviour differs from what it was intended or required to do.

**Security Testing:** seeks to uncover security _**vulnerabilities**_: typically extra functionality that allows an attacker to do something unwanted.

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
