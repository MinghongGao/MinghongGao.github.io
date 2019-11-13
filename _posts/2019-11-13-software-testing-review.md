---
layout: post
title: Software Testing - Review
---
## Week 7 - 1
Vulnerability
+ Fault
+ Unintended Functionality
	+ SQL Injection
	+ Buffer Overglow

C Stack and Memory

Fuzzing

Fuuzer--(generate inputs and feed)--> Program under test

## Week 7 - 2
Checksums and Codes
crc32 - packet body
+ check the integrity of the packet
Parsing Stack

Mutation Based Fuzzing
+ partial knowledge
 + somewhere In between randromly and with good knowledge(genration based fuzzing) 
 + Heuristic-Based Mutation
 + Success Depends on
	 + good quality inputs to mutate
	 + good heutistics to choose how to mutate these inputs

Generation Based Fuzzing

Fuzzing techniques
+ Coverage
	+ Generation > Mutation > Simple ("Dumb") Fuzzing
+ Difficulty to Implement (required knowledge of data format):
	+ Generation > Mutation > Simple Fuzzing

Memory Debuggers
+  Catch
	+ Out-of-bounds accesses to memory
	+ Use-after-free
	+ Double-free and Invalid-free
	+ Memory leaks
	+ Accesses to uninitialised memory

Undefined Behaviour
+ overflow(signed integer and floating number)

## Week 8 -1
Confidentiality

Overt Channels
+ openssl
 + cloudbleed

Implicit (Covert) Leakage
+ Timing

## Week 9 - 1
Symbolic Execution


