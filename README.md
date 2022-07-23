<div align="center">
<h1>Frontend Architecture</h1>
<p><i>A collaborative developer's guide</i></p>
</div>

## 1. Introduction

Frontend code deserves just as much architectural attention as backend code. There's more to it than choosing a directory hierarchy, a UI framework, and maybe a state-management library. Without a robust architecture, frontend apps crumble under the weight of years of feature work and developers who come and go.

There isn't a lot of robust content out there covering frontend architecture; this is a collaborative space designed to change that. Welcome and thanks for participating!

## 2. The problem

The prototypical frontend component, especially those using JavaScript frameworks like React, has everything:

- HTML elements with dynamic content
- Local state
- Input validation
- Remote APIs
  - Calls made directly to hard-coded URLs
  - Data transformations
  - Error handling
- And more

All of this in one component and one file! The result is code that's difficult to understand, test, maintain, and reuse.

## 3. Starting fresh

Let's start with the two principles that underly all best practices in software development: high cohesion and low coupling.

Note: We use the phrase **code constructs** in this guide to succinctly describe functions, classes, components, and packages/modules.

### 3.1. Principle: high cohesion

Cohesion is a measure of how focused a code construct's responsibilities are. A code construct with one responsibility is easier to understand, maintain, and reuse. The [Unix Philosophy](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well) calls this, "Do One Thing and Do It Well (DOTADIW)". 

Cohesion in action:

- Have you ever seen a really long function that's difficult to understand and intimidating to modify? That's low cohesion.
- Have you ever seen a short function that does one thing, does it well, and is reused frequently? That's high cohesion.

Read more about [cohesion on Wikipedia](https://en.wikipedia.org/wiki/Cohesion_(computer_science)). It's also the first concept in [Uncle Bob's SOLID Principles](https://en.wikipedia.org/wiki/Single-responsibility_principle).

### 3.2. Principle: low coupling

Coupling is a measure of how dependent one code construct is on another. More specifically, it's a measure of how connected one code construct is to the implementation details of another code construct.

Coupling in action:

- Have you ever had trouble unit testing a function because it makes calls to a specific API URL? That's high coupling.
- Have you ever had an easy time unit testing a function because it worked the same regardless of whether it ran in your local testing environment or in production? That's low coupling.

Read more about [coupling on Wikipedia](https://en.wikipedia.org/wiki/Coupling_(computer_programming)).

### 3.3. Revisiting the problem

Let's revisit the problematic frontend component from section 2 above.

1. It suffers from low cohesion: it has far too many responsibilities.
2. It suffers from high coupling: with that many responsibilities, it's sure to be heavily coupled. It has a long list of import statements and is nearly impossible to unit test.

The key to fixing this component is increasing cohesion and reducing coupling.

The rest of this guide shows you how.

## 4. Getting specific
