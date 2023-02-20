# The Actor Class

`Tools->Create new c++ class`

### Private and Public

## Create a Blueprint from Actor C++ class

- Create a new `Blueprints` folder under the `Content` folder.
- Create more folders in the `Blueprints` folder to organize things according to the type of blueprints.
- Right click in that new folder and press Create **`Blueprint Class`** and search for the C++ class. Call the new blueprint with `BP_` before the name, ie the class called `Item` then the blueprint from this class will be `BP_Item`.
- You can now drag the blueprint into the world and that will give you more options.

### Blueprint editor

- Duable click the blueprint at the content browser.


> ## Ways to print messages


- Print String and Log String Blueprints
- UE_LOG - Tool for printing messages to output log for debuging.
```cpp
UE_LOG(LogTemp , Warning , TEXT("This will be in the output log"));
```
- GEngine - 
```cpp
if(GEngine)
{
    GEngine->AddOnScreenDebugMessage(1, 60.f , FColor::Cyan , FString("Item on screen msg!"));
    // args are - key , time , color , msg
}
```



> ## Debug Helpers

### Debug Sphere
```cpp
 DrawDebugSphere(GetWorld() , Location, 25.f , 12 ,FColor::Red , true);
```
In this function (and the some of the next functions) there is an argument set to `true` and is the `bPersistentLine` argument. by setting it to `true` the debug sphere will stay and will not disapear. If set to false, then there is an argument after that set the time that this sphere should stay on the screen. If you want to set it for one frame, it is good practice to set it like this:
```cpp
 DrawDebugSphere(GetWorld() , Location, 25.f , 12 ,FColor::Red , false , -1.f);
```

### Debug Line
```cpp
FVector Location = GetActorLocation();
FVector Forward = GetActorForwardVector();
DrawDebugLine(GetWorld() , Location , Location + Forward * 100.f , FColor::Red , true , -1.f , 0 , 1.f);
```

### Debug Point
```cpp
FVector Location = GetActorLocation();
FVector Forward = GetActorForwardVector();
DrawDebugPoint(GetWorld() , Location + Forward * 100.f , FColor::Red , true );
```


> ## Funciton Macros

Definition for the pre-procesor for replacing one code with another. By writing this line at the top of the `.cpp` script, the compiler will define this macro:

```cpp
#include "DrawDebugHelpers.h"

#define DRAW_SPHERE(Location) if (GetWorld()) DrawDebugSphere(GetWorld() , Location, 25.f , 12 , FColor::Red , true);
```
Then, for using it, just call it like that:

```cpp
FVector Location = GetActorLocation();
DRAW_SPHERE(Location)
```

By defining this macro at the Project `.h` file, you can import it from different scripts in the project. Another way is to [set a new costum header file](./5_5_Costum%20Header%20file.md).

### Macros On multiple lines
By using two macros, you can connect them into one as follows:
```cpp
#define DRAW_SPHERE(Location) if (GetWorld()) DrawDebugSphere(GetWorld() , Location, 25.f , 12 , FColor::Red , true);
#define DRAW_LINE(StartLocation , EndLocation) if (GetWorld()) DrawDebugLine(GetWorld() , StartLocation , EndLocation , FColor::Red , true , -1.f , 0 , 1.f);
#define DRAW_POINT(Location) if (GetWorld()) DrawDebugPoint(GetWorld() , Location , FColor::Red , true );

#define DRAW_VECTOR(StartLocation , EndLocation) if (GetWorld()) \
{\
DrawDebugLine(GetWorld() , StartLocation , EndLocation , FColor::Red , true , -1.f , 0 , 1.f); \
DrawDebugPoint(GetWorld() , EndLocation , FColor::Red , true );\
}

```


