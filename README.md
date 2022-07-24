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

**Note 3.a**: We use the phrase ***code constructs*** in this guide to succinctly describe functions, methods, classes, components, packages, and modules.

### 3.1. Principle: high cohesion

Cohesion is a measure of how focused a code construct's responsibilities are. A code construct with a single, focused responsibility is easier to understand, maintain, and reuse. The [Unix Philosophy](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well) calls this, "Do One Thing and Do It Well (DOTADIW)". 

Cohesion in action:

- Have you ever seen a really long function that's difficult to understand and intimidating to modify? That's low cohesion.
- Have you ever seen a short function that does one thing, does it well, and is reused frequently? That's high cohesion.

Read more about [cohesion on Wikipedia](https://en.wikipedia.org/wiki/Cohesion_(computer_science)). It's also the first concept in [Uncle Bob's SOLID Principles](https://en.wikipedia.org/wiki/Single-responsibility_principle).

### 3.2. Principle: low coupling

Coupling is a measure of how dependent one code construct is on another. More specifically, it's a measure of how connected one code construct is to the implementation details of another code construct.

Coupling in action:

- Have you ever had trouble unit testing a function because it makes calls to a specific API URL? That's high coupling.
- Have you ever had an easy time unit testing a function because it worked the same regardless of whether it ran in your local testing environment or in production? That's low coupling.

Read more about [coupling on Wikipedia](https://en.wikipedia.org/wiki/Coupling_(computer_programming)). It's also the final concept in [Uncle Bob's SOLID Principles](https://en.wikipedia.org/wiki/Dependency_inversion_principle).

### 3.3. Revisiting the problem

Let's revisit the problematic frontend component from section 2 above.

1. It suffers from low cohesion: it has far too many responsibilities.
2. It suffers from high coupling: with that many responsibilities, it's sure to be heavily coupled. It has a long list of import statements and is nearly impossible to unit test.

The key to fixing this component is increasing cohesion and reducing coupling.

The rest of this guide shows you how.

## 4. Best practices

The next step is to take the principles of high cohesion and low coupling and turn them into specific, actionable practices. For each of these practices we illustrate how to implement them with different frontend technologies.

**Note 4.a.**: The sections below use a ***pseudo-language*** and a ***pseudo-framework*** to demonstrate best practices. If the pseudo-code is a little too far off from what you're using to build your frontend application, then don't worry: each section includes implementations using your favorite frontend technology.

### 4.1. Composition

### 4.2. Dependency injection

Dependency injection is a design pattern where a code construct **receives** its dependencies rather than hard-coding them internally. This reduces coupling and usually increases cohesion. 

Consider a frontend component that displays a user's profile information.

```tsx
function ProfileComponent(userID: string) {
  // Retrieve profile information
  user = fetch("https://api.mycompany.com/api/users/" + useriD)

  // Render the component
  return (
    <div>
      <p>Name: {user.firstName} {user.lastName}</p>
      <p>Email: {user.email}</p>
    </div>
  )
}
```

This component has two problematic dependencies.

1. It's coupled to the `https://api.mycompany.com/api/users/` URL. 
2. It's coupled to a function `fetch` that makes a remote HTTP call.

This component is very difficult to unit test and will require modification if we want to fetch the user from something other than `https://api.mycompany.com`.

[Here's how to fix it.](/docs/dependency-injection.md)