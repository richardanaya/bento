- dynamic polymorphism
- functional
- no null
- static typed

```zig
component Time
  time int64
  
component Position
  x float32
  y float32

component Velocity
  x float32
  y float32

system Physics [Time;p Position,v Velocity](timer,entity)
  entity.p.x = entity.p.x * timer.time
  
system Logging [desc Description](entity)
  println(entity.desc.name)

system Rendering [p Position](entity)
  # Todo: render rectancles with entity.p.x and entity.p.y

function main i int32 -> () 
  @entity Position{0,0} Velocity{0,0}
  @entity Position{0,0} Velocity{1.0,0}
  while true
    @exec (Logging,Physics) -> Rendering
```
