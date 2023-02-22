# Pawns

The pawn class is derived from the actor class but has more functionality.

In Unreal, after creating a new pawn and setting up the c++ files, you can create blueprint from that pawn.

## [Adding a Capsule](https://docs.unrealengine.com/5.1/en-US/API/Runtime/Engine/Components/UCapsuleComponent/)

A Pawn Capsule is a component in Unreal Engine that is often used as the primary collision representation for a character or pawn. It is a cylindrical or capsule-shaped collider that surrounds the character or pawn, providing a simplified but accurate representation of their physical shape and size.

The Pawn Capsule component is commonly used in combination with other components such as a skeletal mesh, animation blueprint, and movement components to create a fully functional character or pawn in a game.

When a Pawn Capsule collides with other objects in the game world, it generates collision events that can be used to trigger various behaviors or effects. Additionally, the Pawn Capsule is often used as the basis for character movement, with movement and physics calculations being performed based on the capsule's position and orientation.

Unreal engine has a `UCapsuleComponent`. UCapsuleComponent is a collision component in Unreal Engine that provides a capsule-shaped collision volume for an object, commonly used for representing characters or pawns.

```cpp
// Header.h

private:
    UPROPERTY(VisibleAnywhere)
    class UCapsuleComponent* Capsule; // Forward Declaration
```

```cpp
// CPP.cpp
#include "Components/CapsuleComponent.h"

// at the constructor:
    Capsule = CreateDefaultSubobject<UCapsuleComponent>(TEXT("Capsule"));
    Capsule->SetCapsuleHalfHeight(20.f);
    Capsule->SetCapsuleRadius(15.f);
    SetRootComponent(Capsule);
```

>  **Forward declaration** is a feature in C++ that allows a program to declare a class or function without providing a full definition of it. This allows the program to use the declared class or function without including the entire header file, which can help reduce compilation times. Forward declarations are typically used in header files to improve build times and reduce coupling between classes.

## [Skeletal Mesh Component](https://docs.unrealengine.com/5.1/en-US/API/Runtime/Engine/Components/USkeletalMeshComponent/)

Skeletal Mesh component in Unreal is a specialized type of Mesh Component that is designed to support skeletal animation. It allows the attachment of a 3D character model that is rigged with a skeleton and associated animations. Skeletal Mesh components can be used to create complex and dynamic animations, such as walking, running, and jumping, in video games and other real-time applications. They can be controlled using various animation systems, including Animation Blueprints and Montages.

```cpp
// Header.h
private:

    UPROPERTY(VisibleAnywhere)
    class USkeletalMeshComponent* SKMesh;
```

```cpp
// CPP.cpp
#include "Components/SkeletalMeshComponent.h"

// at the constructor:
    ObjMesh = CreateDefaultSubonject<USkeletalMeshComponent>(TEXT("SomeNameMesh"));
    ObjMesh->SetupAttachment(GetRootComponent());
```

## Controlling Pawns

AController allows us to select a Pawn to possess. All Pawn has a variable called `Auto Possess Player`. You can use a pawn and set this variable to `player 0` to set default pawn to be the pawn you created.

To set the pawn from c++ class you can set it as follows:
```cpp
// MyPawn.cpp

#include "MyPawn.h"

AMyPawn::AMyPawn()
{
    AutoPossessPlayer = EAutoReceiveInput::Player0;
}
```

## Configure Input from Controller
### Axis Mapping

Axis Mapping is a way to map an input axis, such as mouse movement or a joystick, to a specific action in the game. An axis is a continuous input, such as moving the mouse horizontally to rotate the camera left or right. The axis value is usually a float value that represents how far the input axis is being pressed or moved.

To bind a key to a function of a pawn in C++, you can use an Axis Mapping. Here's an example of how to create an Axis Mapping in C++ and bind it to a function of a pawn:
```cpp
// Header.h
private:
    UFUNCTION()
    void Rotate(float AxisValue);
```

```cpp
// CPP.cpp

void AMyPawn::Rotate(float AxisValue)
{
    // after binding, this function will be executed every singel frame
    // Rotate the pawn based on the input axis value
    FVector CurrentRotation = GetActorRotation().Euler();
    CurrentRotation.Z += AxisValue;
    SetActorRotation(FRotator::MakeFromEuler(CurrentRotation));
}

void AMyPawn::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    // Bind the "Rotate" input axis to the Rotate function of our pawn
    PlayerInputComponent->BindAxis(FName("Rotate"), this, &AMyPawn::Rotate);
}
```

### Setup Player Input Component

In this example, we override the `SetupPlayerInputComponent` function of the pawn, which is called when the pawn is possessed by a player. We use the `PlayerInputComponent->BindAxis()` function to bind the "Rotate" input axis to the Rotate function of our pawn.

## Adding Moving Input

The way to move pawns in with movement components. The component should be added to the pawn blueprint along with the code for the function that bind to the movement key:

```cpp
// CPP.cpp

void AMyPawn::MoveFroward(float Value)
{
    if(Controller && (Value != 0.f))
    {
        FVector Forward = GetActorForwardVector();
        AddMovementInput(Forward , Value); // take the direction and add the vector to the location of the pawn
    }
}
```

an example for [movement component](./7_8_Pawn%20Movement%20Components.md) is `FloatingPawnMovement`






