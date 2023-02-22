# Pawn Movement Components

Unreal Engine provides several built-in pawn movement components that can be used for different types of movement:

UFloatingPawnMovement: This is a simple component that provides basic floating movement for the pawn. It can be used for things like flying or swimming.

UCharacterMovementComponent: This is a more complex component that provides realistic movement for characters. It includes features like acceleration, deceleration, gravity, and jumping.

USpectatorPawnMovement: This is a movement component that is designed for spectator cameras. It allows the camera to move smoothly and quickly without the physics constraints of a typical pawn.

UFlyingMovementComponent: This is a specialized movement component that provides airplane-style movement for a pawn. It includes features like banking and yaw control.

UNavMovementComponent: This is a movement component that is used for pawns that need to navigate using the Unreal Engine's built-in navigation system. It includes features like pathfinding and avoidance.

UProjectileMovementComponent: This is a movement component that is designed for projectiles. It provides high-speed movement and includes features like bounces and homing.

UInterpToMovementComponent: This is a movement component that is used for smooth interpolation between two locations. It is often used for cinematic sequences.

Each of these movement components provides different functionality and can be used for different types of movement. You can also create your own custom movement component by inheriting from UPawnMovementComponent and implementing your own movement logic.


```cpp
// MyPawn.h

#pragma once

#include "GameFramework/Pawn.h"
#include "GameFramework/CharacterMovementComponent.h"
#include "MyPawn.generated.h"

UCLASS()
class MYGAME_API AMyPawn : public APawn
{
    GENERATED_BODY()

public:
    AMyPawn();

protected:
    virtual void BeginPlay() override;

private:
    UPROPERTY()
    UCharacterMovementComponent* MovementComponent;
};
```

```cpp
// MyPawn.cpp

#include "MyPawn.h"

AMyPawn::AMyPawn()
{
    // Set the default movement component to the built-in character movement component
    MovementComponent = CreateDefaultSubobject<UCharacterMovementComponent>("MyMovementComponent");
    SetMovementComponent(MovementComponent);
}

void AMyPawn::BeginPlay()
{
    Super::BeginPlay();

    // Enable jumping and set the jump velocity
    MovementComponent->SetJumpAllowed(true);
    MovementComponent->JumpZVelocity = 500.f;
}
```

