# Moving Objects

## Set actor location
```cpp
SetActorLocation(FVector(0.f , 0.f , 50.f));
```

## Set Actor Rotation

Takes 3 argument - the values of angle rotation about an axis (x,y,z) of the actor
Teleport Physics - if you parts attach to this actor that use physics, then a change in the rotation will effect those things if the teleport physics set to false.
```cpp
SetActorRotation(FRotator(0.f , 45.f , 0.f));
```

FRotator is like an FVector, But takes the three angle values for rotation about an axis.

## Add Actor World Offset\Rotation

Setting the actor's position or rotation in relation to its **last position**. It is different from the `SetActorLocation` and `SetActorRotation` function because those are in relation to the origin of the world.

```cpp
AddActorWorldOffset(FVector(1.f , 0.f , 0.f));
```

## Moving Rate

For creating a movement that is **independent** of the frame rate check [this file](./6_5_DeltaTime.md) about the `DeltaTime` variable.

## Actor's Variables and Functions

While writing the Actor C++ class, one of the key features is writing your own functions and variables of the class

In C++, the *private*, *public*, and *protected* keywords are used to specify the access level of class members, including variables and functions. These access levels determine which parts of the class are visible and accessible to other parts of the code.

In the context of the *AActor* class in Unreal Engine, the private, public, and protected sections are used to specify the access level of the class members. Here's an overview of what each section means:

* **Private**: Members declared as private are accessible only within the class itself. They cannot be accessed from outside the class or from derived classes. In the context of AActor, private members may include variables and functions that are used internally by the class and are not intended to be accessed from outside the class.

* **Protected**: Members declared as protected are accessible within the class itself and its derived classes. They cannot be accessed from outside the class hierarchy. In the context of AActor, protected members may include variables and functions that are used internally by the class and are intended to be accessed by derived classes.

* **Public**: Members declared as public are accessible from anywhere in the code, including outside the class hierarchy. In the context of AActor, public members may include variables and functions that are intended to be accessed from other parts of the code, such as other classes or Blueprint graphs.

Here's an example of how the private, public, and protected sections might be used in the AActor class:

```cpp
UCLASS()
class AActor : public UObject
{
    GENERATED_BODY()

private:
    int32 PrivateVariable;

protected:
    int32 ProtectedVariable;

public:
    UFUNCTION(BlueprintCallable)
    void PublicFunction();
};
```

In this example, we have declared three variables and one function in the AActor class. PrivateVariable is declared as private and can only be accessed within the AActor class itself. ProtectedVariable is declared as protected and can be accessed within AActor and any derived classes. PublicFunction is declared as public and can be accessed from anywhere in the code, including outside the AActor class hierarchy.

It's important to use the access levels appropriately to ensure that your code is well-organized, easy to read, and secure. Private members should only be accessed internally by the class, protected members should only be accessed by the class and its derived classes, and public members should be used to expose the interface of the class to other parts of the code.

For more information about the Actor's functions and variables and the way to expose them in Unreal Engine internal UI go to [this file](./6_7_Exposing%20Var%20and%20Funcs.md).



