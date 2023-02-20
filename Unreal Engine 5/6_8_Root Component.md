# Root Component

Every Actor in Unreal Engine has a root component, which is the default component that is automatically created when the Actor is instantiated. The root component is the primary component of an Actor and is responsible for defining the Actor's position, orientation, and scale in the game world.

The root component can be any type of component, such as a Scene Component, Static Mesh Component, or Collision Component, depending on the needs of the Actor. For example, a simple game object might have a Scene Component as its root, while a character or vehicle might have a Skeletal Mesh Component or a Physics Component as its root.

The root component is required for an Actor to be placed in the game world and to interact with other Actors and the game environment. All other components that are added to an Actor are attached to the root component, forming a hierarchical tree of components that make up the Actor's behavior and appearance.

In addition to its primary function of defining an Actor's position and orientation, the root component can also have its own set of properties and functionality that can be customized to suit the needs of the game. For example, you can add collision, physics, or animation properties to the root component to make it interact with the game world and other objects in a more realistic way.