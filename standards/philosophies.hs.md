# Philosophies

The ideal of the FDK is to provide easy to use tools to improve your forging
goals and experience. We do this by teaching, enforcing, learning, documenting,
etc. our experiences with Halo 5's Forge tool. This initiative is headed by
**Ray Benefield**, a professional Innovation Solutions Architect and veteran
Software Engineer. The standards that are set by the FDK are strictly managed
by Ray, enforcing solid software engineering principles to ensure maximum
useability.


## SOLID Principles

The SOLID principles of Object Oriented Programming (OOP), improve software.
There are an abundance of articles written about the value of SOLID. Each
letter stands for a very particular principle, all of these principles seem to
fit extremely well in the Forge ecosystem.

### Single Responsibility Principle

###### References

[The Single Responsibility Principle by Robert "Uncle Bob" Martin](https://www.youtube.com/watch?v=Gt0M_OHKhQE)


### Open/Closed Principle


### Liskov Substitution Principle


### Interface Segregation Principle


### Dependency Injection Principle


## Composition over Inheritance

In Forge we don't really have the concept of Inheritance (behaviour taken from
a parent). However the value that is learned from this principle in terms of
how Composition can make our objects better is astronomical. The idea is that
rather than inheriting behaviour from "being" something, insteaad behaviour is
given by "having" something. This concept is enforced by the use of
[Aspects](../aspects). These aspects are responsible for a single
capability/behaviour of an object and manages everything related to that skill.


## Pub/Sub Models

In a world where there can be MANY objects that do different things, it isn't
feasible for a single object to be aware of every single other object it needs
to interact with. Because of this the model of Publishing messages and events,
with whoever cares Subscribing to those messages and events, serves to be a
powerful model. Our standards are strongly influenced by the fact that Objects
should not know every single object that cares about this. This also ensures
that any amount of subscribers can be a part of the event rather than the 1 or
2 that were initially planned.
