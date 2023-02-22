# Camera Component and Spring Arm

1. The **SpringArmComponent** is a component that attaches to a parent object and can be used to control the position and rotation of a child component, such as a camera.
2. The **CameraComponent** is a component that renders a view of the game world from a particular position and orientation, and can be attached to a SpringArmComponent to provide additional control over its position.
3. Together, the **SpringArmComponent** and **CameraComponent** are often used in Unreal Engine to create a smooth, follow-behind camera effect that tracks a player character as they move through the game world.

```cpp
// MyPawn.h

#pragma once

#include "GameFramework/Pawn.h"
#include "Camera/CameraComponent.h"
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
    class USpringArmComponent* SpringArmComponent;

    UPROPERTY()
    class UCameraComponent* CameraComponent;
};
```

```cpp
// MyPawn.cpp

#include "GameFramework/SpringArmComponent.h"
#include "MyPawn.h"

AMyPawn::AMyPawn()
{
    // Set up the spring arm component
    SpringArmComponent = CreateDefaultSubobject<USpringArmComponent>("SpringArm");
    SpringArmComponent->SetupAttachment(RootComponent);
    // change the length of the spring arm 
    SpringArmComponent->TargetArmLength = 500.f;
    // change the rotation of the spring arm
    
    FRotator CurrentRotation = SpringArmComponent->GetRelativeRotation();
    CurrentRotation.Yaw += 45.f; // Add 45 degrees to the current yaw angle
    SpringArmComponent->SetRelativeRotation(CurrentRotation);

    // Set up the camera component
    CameraComponent = CreateDefaultSubobject<UCameraComponent>("Camera");
    CameraComponent->SetupAttachment(SpringArmComponent, USpringArmComponent::SocketName);
}

void AMyPawn::BeginPlay()
{
    Super::BeginPlay();

    // Set the default camera position
    SpringArmComponent->SetRelativeLocation(FVector(0.f, 0.f, 50.f));
    CameraComponent->SetRelativeLocation(FVector(0.f, 0.f, 0.f));
}
```

In this example, we create two new properties in our AMyPawn class: a USpringArmComponent and a UCameraComponent. In the constructor, we set up the spring arm component by creating a new instance of USpringArmComponent, setting its parent to the root component of the pawn, and setting its target arm length. We then set up the camera component by creating a new instance of UCameraComponent, setting its parent to the spring arm component, and attaching it to the socket named USpringArmComponent::SocketName on the spring arm component.

In the BeginPlay function, we set the default camera position by setting the relative locations of the spring arm and camera components. In this example, we set the spring arm to be 50 units above the root component, and the camera to be at the same location as the root component.

Note that in this example, we also include the Camera/CameraComponent.h and GameFramework/SpringArmComponent.h header files, which are required to use the UCameraComponent and USpringArmComponent classes, respectively. You may need to include other header files depending on which components you are using.

