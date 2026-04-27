---
clipped: 2026-04-27
url: https://martinfowler.com/bliki/TestDrivenDevelopment.html
author: Martin Fowler
---

# Test Driven Development

Martin Fowler
testing
programming style
Test-Driven Development (TDD) is a technique for building
  software that guides software development by writing tests. It was
  developed byKent
  Beckin the late 1990's as part of
  Extreme Programming. In essence we follow three simple
  steps repeatedly:
Write a test for the next bit of functionality you want to add.
Write the functional code until the test passes.
Refactor both new and old code to make it well structured.
Although these three steps, often summarized asRed - Green -
  Refactor, are the heart of the process, there's also a vital initial
  step where we write out a list of test cases first. We then pick one of these
  tests, apply red-green-refactor to it, and once we're done pick the next.
  Sequencing the tests properly is a skill, we want to pick tests that drive us
  quickly to the salient points in the design. During the process we should add
  more tests to our lists as they occur to us.
Writing the test first, whatXPE2calls
  Test-First Programming, provides two main benefits. Most obviously it's a way
  to getSelfTestingCode, since we can only write some functional
  code in response to making a test pass. The second benefit is that thinking
  about the test first forces us to think about the interface to the code first.
  This focus on interface and how you use a class helps us separate interface
  from implementation, a key element of good design that many programmers
  struggle with.
The most common way that I hear to screw up TDD is neglecting
  the third step. Refactoring the code to keep it clean is a key part
  of the process, otherwise we just end up with a messy aggregation of
  code fragments. (At least these will have tests, so it's a less
  painful result than most failures of design.)
Further Reading
Kent's summary of thecanonical way to do TDDis the key online summary.
For more depth, head to Kent Beck's bookTest-Driven Development.
The relevant chapter of James Shore'sThe
    Art of Agile Developmentis another sound description that also
    connects it to the rest of effective agile development. James also wrote a
    series of screencasts calledLet's Play TDD.
Revisions
My original post of this page was 2005-03-05. Inspired by Kent's
    canonical post, I updated it on 2023-12-11
Topics
Architecture
Refactoring
Agile
Delivery
Microservices
Data
Testing
DSL
about me
About
Books
FAQ
content
Videos
Content Index
Fragments
Board Games
Photography
Thoughtworks
Home
Insights
Careers
Radar
Engineering
follow
RSS
Mastodon
LinkedIn
Bluesky
X
BGG
© Martin Fowler |Disclosures
