## Exposing variables in blueprints from cpp

`UPROPERTY()` is allow the class to expose the variable to the reflection system.


Inside UPROPERY you can specify some options:

- EditDefaultOnly - allow edit of a property from the default panel, every change will effect all the instances.
- EditInstanceOnly - allow edit from only the default panel.
- EditAnywhere - Allow edit in both default panel and instance panel.
- VisibleDefaultsOnly - visible but not editable from the default panel.
- VisibleInstanceOnly -
- VisibleAnywhere -

## Exposing variable to the event graph

By adding another argument to `UPROPERTY()` macro, you can specify if you want to expose a variable to the blueprint and how.
- BlueprintReadOnly - expose read only option in the eventgraph, this option can’t be use on a private variable! The variable should be moved to the `protected` section.
- BlueprintReadWrite - let you get the variable and also set it.


The UPROPERTY MACRO has **Category** argument that can be set to a string. That will organize the variables in costume category:
```cpp
UCLASS()
class AMyActor : public AActor
{
    GENERATED_BODY()

public:
    UPROPERTY(EditAnywhere, Category = "My Category")
    int32 MyVariable;
};
```


## Exposing functions to blueprints
To expose a function you can use the `UFUNCTION()` macro. Similar to UPROPERTY, this macro has some special specifiers:

* BlueprintCallable - allow calling the function inside a blueprint.
* BlueprintPure - calculate a value and return it. In blueprint, don’t have an input execution pin , just input and output variables.

```cpp
UCLASS()
class AMyActor : public AActor
{
    GENERATED_BODY()

public:
    UFUNCTION(BlueprintCallable, Category = "My Category")
    void MyFunction(int32 MyParameter);
};

```