# DeltaTime

By scaling things with DeltaTime variable, you can achive a constant rate of moving, although the frame rate (FPS) of the game can change.

Example:
Setting actor's to a new position every frame at the `Tick` funciton as follows:
```cpp
SetActorsWorldLocation(FVector(1.f , 0.f , 0.f));
``` 
will move the actor one unit (1 cm) every frame. For 120 FPS will be 120 cm per second, and for 30 FPS will be slower!

You can set a variable of `MovementRate`:
```cpp
float MovementRate = 50.f; // cm/sec
// MovementRate * DeltaTime = MovementPerFrame
// units -> [cm/sec] * [sec/frame] = [cm/frame]
```
If multiply by the DeltaTime variable, it scales to movement units per second:
```cpp
SetActorsWorldLocation(FVector(MovementRate * DeltaTime , 0.f , 0.f))
```
