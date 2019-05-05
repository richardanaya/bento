- dynamic polymorphism
- dynamic dispatching via function overloading
- functional
- no null
- static typed

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
  entity.p.x = entity.v.x * timer.time;
  entity.p.y = entity.v.y * timer.time;
  
system Logging[desc Description](entity)
  println(entity.desc.name);

system Rendering[p Position](entity)
  # TODO - render rectancles with entity.p.x and entity.p.y

function main(string[] args) -> int32
  @ Create a resource for time
  @resource Time{.1}
  # Create two entities
  @entity Description{"player 1"} Position{0,0} Velocity{0,0};
  @entity Description{"player 1"} Position{0,0} Velocity{1.0,0};
  while true
    # Run logging and physics system in parallel the run rendering system
    @run Logging Physics -> Rendering;
  0
```
