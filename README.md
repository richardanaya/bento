- dynamic polymorphism
- functional
- no null
- static typed

```nim
comp Time
  time int64
  
comp Position
  x float32
  y float32

comp Velocity
  x float32
  y float32

sys Physics [Time;p Position,v Velocity](timer,entity)
  entity.p.x = entity.p.x * timer.time

fn main i int32 -> () 
  @ Position{0,0} Velocity{0,0}
  @ Position{0,0} Velocity{1.0,0}
```
