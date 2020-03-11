---
layout: post
title: Hexagonal Architecture - Introduction
---

This article will introduce you to the Hexagonal Architecture.  
[Github link](https://github.com/ayshiff/hexagonal-architecture-typescript)

The Hexagonal Architecture is based on a principle:

```
Allow an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.
```

It means that we have to **isolate the business logic** from the rest of the application.
The domain (business logic) is the center of our architecture.

## First principle

The first principle is that we have to isolate our codebase into three main parts:

- **Application**: This is the part where the user interact with the app, control the domain.
- **Domain**: This is our business logic.
- **Infrastructure**: This is the part where we have the code that communicate with the database or the code that drives the HTTP calls.

![Schema](https://blog.octo.com/wp-content/uploads/2018/07/archi_hexa_06.png)

The main benefits of this architecture is that it split our problems. At any time, we can focus on a specific part to understand them more.

We will take the example from `Alistair in the “Hexagone”`, by Thomas Pierrain (@tpierrain) et Alistair Cockburn (@TotherAlistair) in 2017.
This simple CLI app will print some poems in the terminal.

To show you how the app will be strutured we will have:

![Schema](https://blog.octo.com/wp-content/uploads/2018/07/archi_hexa_01.png)

Interaction application / domain -> As we said before we want that our domain logic can be driven by our user or by automated tests. The user just want to ask for poems (business logic).

Interaction domain / infrastructure -> From the domain point of view, we don't care about the origin of the poems (database, file...). We care about testing our application regardless of this origin.

## Second principle

Dependencies always go to the outside.
To drive the application as well by tests or by hand (user), the application part **must** depend on the domain part.
In the same way, to test the application as well by providing a database, file... the infrastructure part **must** depend on the domain part.
Thanks to the interface (**inversion of dependencies**).

## Third principle

We isolate borders with interfaces.
The domain defines **Ports** where the outside word can plug **Adapter** which must respect the **Ports** shape.

## Conclusion

Our app can now be drived by user, tests, bash scripts, etc... and it can be developed and tested in isolation from the execution system and database.
You can find the code referring to this article [here](https://github.com/ayshiff/hexagonal-architecture-typescript).

This article is mostly inspired by [this](https://blog.octo.com/architecture-hexagonale-trois-principes-et-un-exemple-dimplementation/) octo talk.
Thanks to them for their great article.
