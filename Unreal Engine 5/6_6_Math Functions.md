# FMath
The FMath library in Unreal Engine is a collection of math functions that provide common mathematical operations and functions that are often used in game development, such as vector and matrix operations, trigonometric functions, and interpolation.


1. Clamp: clamps a value between a minimum and maximum value.
```cpp
float Value = 5.0f;
float Min = 0.0f;
float Max = 10.0f;

float ClampedValue = FMath::Clamp(Value, Min, Max);
// ClampedValue is now 5.0f, since it is within the range of 0.0f to 10.0f.
```

2. Lerp: performs a linear interpolation between two values.
```cpp
float StartValue = 0.0f;
float EndValue = 10.0f;
float Alpha = 0.5f;

float LerpValue = FMath::Lerp(StartValue, EndValue, Alpha);
// LerpValue is now 5.0f, since it is halfway between 0.0f and 10.0f.
```

3. DotProduct: calculates the dot product of two vectors.
```cpp
FVector Vector1 = FVector(1.0f, 2.0f, 3.0f);
FVector Vector2 = FVector(4.0f, 5.0f, 6.0f);

float DotProduct = FMath::DotProduct(Vector1, Vector2);
// DotProduct is now 32.0f.
```

4. TransformVector: transforms a vector by a given transform.
```cpp
FVector Vector = FVector(1.0f, 2.0f, 3.0f);
FTransform Transform = FTransform(FRotator(0.0f, 90.0f, 0.0f), FVector(1.0f, 2.0f, 3.0f), FVector(1.0f, 1.0f, 1.0f));

FVector TransformedVector = FMath::TransformVector(Transform, Vector);
// TransformedVector is now (-2.0f, 2.0f, 4.0f), since it has been rotated 90 degrees around the Y axis and translated by (1.0f, 2.0f, 3.0f).
```

## Sine and Cosine
 1. Character movement: the sine function can be used to create a smooth, oscillating motion for a character's movement. For example, you could use the sine function to create a bobbing motion for a character's head.

```cpp
float Time = FPlatformTime::Seconds();
float BobbingHeight = 10.0f;
float BobbingSpeed = 1.0f;

FVector HeadPosition = GetActorLocation() + FVector(0.0f, 0.0f, FMath::Sin(Time * BobbingSpeed) * BobbingHeight);
SetActorLocation(HeadPosition);
```

2. Camera movement: the cosine function can be used to create a circular motion for a camera around a central point. For example, you could use the cosine function to create a panning motion for a camera around a character.
```cpp
float Time = FPlatformTime::Seconds();
float PanRadius = 100.0f;
float PanSpeed = 1.0f;

FVector CharacterPosition = GetCharacterLocation();
FVector CameraPosition = CharacterPosition + FVector(FMath::Cos(Time * PanSpeed) * PanRadius, FMath::Sin(Time * PanSpeed) * PanRadius, 0.0f);
SetCameraLocation(CameraPosition);
```

