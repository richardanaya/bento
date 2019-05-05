# 🍱 Bento

Bento is a language for orchestrating data flow problems performantly and concurrently.

- static typed
- dynamic polymorphism via entity component system
- dynamic dispatching via function overloading
- no null

```
function main(string[] args) -> int32
  println("Hello World!")
```

```
bento -o hello hello.b
```

# Entity Component System

Bento is built for entity component systems, ECS systems are typically used for games but are usable for polymorphic data problems that want to parallelize operations of any type.

## simple physics engine

```julia
component Time
  delta_time float32
  
component Description
  name string
  
component Position
  x float32
  y float32

component Velocity
  x float32
  y float32

system Physics[Time;p Position,v Velocity](timer,entity)
  entity.p.x = entity.v.x * timer.time
  entity.p.y = entity.v.y * timer.time
  
system Logging[desc Description](entity)
  println(entity.desc.name)

system Rendering[p Position](entity)
  # TODO - render rectancles with entity.p.x and entity.p.y

function main(string[] args) -> int32
  # Create a resource for time
  @resource Time{.1}
  # Create two entities
  @entity Description{"player 1"} Position{0,0} Velocity{0,0}
  @entity Description{"player 1"} Position{0,0} Velocity{1.0,0}
  while true
    # Run logging and physics system in parallel then run rendering system
    @run Logging Physics
    @run Rendering
  0
```

## data processing


## polymorphic behavior

Inheritance can sometimes lead to extremely tricky scenarios such as the [OOP diamond problem](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem), using polymorphic behavior via components can simplify the expression of these problems.

# Why should't you use Bento?
There are a number of scenerios where Bento might not be of value
* Your data structure is extremely small. This language is probably just overkill and maybe something like C would be better.
* You have as many different types of data as you have entities. In cases of GUI applications, OOP might be a better fit.
* Parallelization isn't possible for you. A big part of this language is running systems concurrently. Your data flow problem might be expressed more simply without the concept of systems.
