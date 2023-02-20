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


## Template Functions
a template function is a function that can work with any data type specified by the user. This allows for greater flexibility and code reusability. Here are some key points to keep in mind about template functions in Unreal C++:

1. Syntax: To define a template function in Unreal C++, you need to use the template keyword followed by a list of template parameters enclosed in angle brackets (<>) before the function declaration. For example:
```cpp
template <typename T>
void MyTemplateFunction(T myParam);
```

2. Usage: When you call a template function, you need to specify the data type you want to use as the template argument. For example:

```cpp
MyTemplateFunction<int>(42); // Calls the function with an int argument
MyTemplateFunction<float>(3.14f); // Calls the function with a float argument
MyTemplateFunction<FVector>(FVector::ZeroVector); // Calls the function with a vector argument
```

3. Implementation: The implementation of a template function needs to be included in the header file rather than in a separate source file. This is because the template code is generated at compile time, and the compiler needs to see the implementation when it generates the code for each data type used with the template. For example:

```cpp
// MyHeaderFile.h
template <typename T>
void MyTemplateFunction(T myParam)
{
    // Implementation goes here
}
```

4. Restrictions: There are some restrictions on what you can do with template functions in Unreal C++. For example, you cannot use templates to create virtual functions or member functions of a class template. You also cannot use templates to create template classes or functions with certain types of arguments, such as references to arrays or functions.

Overall, template functions can be a powerful tool for writing flexible and reusable code in Unreal C++. They allow you to write functions that work with any data type, without having to write separate code for each type.

## Components

An Actor can have one or more components, which are modular pieces of functionality that can be added, removed, or swapped out to modify the Actor's behavior, appearance, and interaction with the game world. Here are some key points to keep in mind about Actor components in Unreal Engine:

Every Actor has the [root components](./6_8_Root%20Component.md) as a default.

### Attachment
Components can be attached to the actor from the blueprint side of from the c++ side. The attachment of a component is giving the actor the visualization of the component, as well as some of the abilities of it.

### Class Default Object
In Unreal Engine, the class default object is a single instance of a class that is created automatically when the engine loads the class. The class default object is used as a template for creating new instances of the class, and it provides default values for the class's properties and functions.

The class default object is an instance of the class that is created and managed by the engine itself, rather than being created by the game code. It is used as a shared template for all instances of the class, so any changes made to the class default object will affect all instances of the class that are created afterwards.

This is important to know because for creating and attaching component to an actor, you have to create a default subobject as follows:

```cpp
//Header.h file
private:

    UPROPERTY(VisibleAnywhere)
    UStaticMeshComponent* ItemMesh;

```
```cpp
//Item.cpp

// constructor function
AItem::AItem()
{
    PrimaryActorTick.bCanEverTick = true;

    ItemMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ItemMeshComponent")); // Attach the static mesh and give it a name
    RootComponent = ItemMesh; //Delete the RootComponent and asign the StaticMesh to be the new root
}
```

There is a way to hardcode the static mesh variable and set it to a specific object, but it is usualy good practice to set is from the blueprint view.

