+++
date = "2017-07-14T08:27:03-07:00"
description = ""
draft = false
title = "Gophercon Day 2 Quick Notes"
weight = 20

+++

Not a real blog post, just recording notes from the talks I got to watch.

## Channels behind the scenes

@katya719


## Go Community

Write the docs

1. Answer questions
2. Write a blog post
3. Improve a website

## Advanced Testing from Hashicorp

Two parts of Testing


### Test Methodologies

Write code that can be tested well and easily.

**Subtests** 

Closures for managing hirearchial tests

**Table drive tests**

Used extensively at Hashicorp

* Low overhead for new test cases
* Use for even single/simple cases
* Embed name in test name in table. eg: tb := {"foo", 1, 2, 3} -> `t.Run(tb[0], func(t *testing.t)...`

**Test Fixtures**

`pwd` is always the package directory 

Relative path can be used to save test files.

**Golden Files**

Embed a `flag.Bool("update", false, "update golden files")`

Write a file, read it, and compare the diff.

Adding flags to tests is easy! `>_>`

**Configurability**

Over-paramterize structs to allow tests to fine tune their behavior

Make configurations unexported

Use Test Boolean variables

**Interfaces**

* Mocking points
* Smaller mocks can be implemented easier

[testing interface lib](github.com/mitchellh/go-testing-interface)


### Writing Testable Code

**Global state**

Avoid as much as possible

Instead use a configuration option for the test.

**Test Helpers**

Test helpers should never return an error, use the `t` struct to report error

**Repeat Yourself in Tests**

* Localized logic is more important than test lines of code
* Explicit test cases from copy pasta are better than logic spread across a bunch of files
 * 200 lines of test is better than 20 dense

**Package Functions**

* Break down functionality into packages/functions judiciously
 * But don't overcook it
* Try to test the Exported functions
* Test the internal functionality as only implementation details

**Internal Packages**

* Use as a mechanism to uncomfortably overpackage things.
* Under packaging leads to tightly coupled dependencies
 * Better to kill packages later than under package


**Networking Testing**

* Testing Networking? Make a real network connection!
* Easy to test: [any protocol, return listener, typesipv6 etc]
* No reason to mock net.Conn

**Testing Complex Structs**

* Use reflect.DeepEqual 

**Subprocessing**

Real:
* Executing the subprocess is nice. eg: `git`
* Guard the test to verify that the binary exists

Mock:
* Execute a mock instead of the actual target
* Example: os/exec testing
* Actual example is complicated...

**Testing Frameworks**

Frameworks called from a go test, set with a flag, 

## Evolving Desitributed Systems

@peterbourgon

"Weeks of programming can save hours of planning"

1. Design
2. Build

### Design

Start with shared doc with plans of design

Moved to Markdown document

Behaviors -> Components -> Implementation -> coda

"The Design of Design" Frederick P Brooks

* Design is a dialogue 

"Zen and the art of Motorcycle Maintenance" Robert Pirsig

### Build

Make it right.

Review(design) -> Implement -> Identify Problems -> Plan changes -> coda

Consider the cost of premature abstraction.

### Optimize

Design(tests with clear outcomes) -> Execute -> Capture(output) -> Implement(improvements) -> coda

### Instrumentation > Logs

USE: Utilization, Saturation, Error rate 

RED: Request rate, Error Rate, Duration

Iterative testing

`go tool pprof -alloc_objects ...`

Only dive into optimizations when you can demonstrate its value.

### Conclusions

Think, then act

Articulate clear scoping 

Observe and/or Decide Act

(Not Invented Here) isn't a four letter word

I think [Peter Bourgon](https://peter.bourgon.org/) is my new engineering hero..


## Go at the DARPA Cyber Grand Challenge

Offensive and Defensive operations

Network inputs from legitimate sources could not fail.

There is some buffering built into the network stack. 
    Added buffering after picking packets off the wire to handle bursts.

MySQL running on memory filesystem 

Team Xandra [Cyber Challenge](http://archive.darpa.mil/cybergrandchallenge/event.html#results)

## Go Package Management?

Gopkg.lock -> vendor/ is rough around the edges right now

Third space outside of `vendor/`; `go/vendor/{tagged package sets}`














