
General notes about various new/hot JS frameworks and their differences

## Rendering

**React** - starts from the top and any update to state will re-renders all the way down the component tree

**Solid** or **Qwik**: Change in state is not associated with a component rather directly with a DOM node.

## Pre-rendering

**React and Solid** : Hydrate the html sent to the client

**Qwik** : Serialize the reactivity graph at the server, effectively lowering time to interactive (TTI)

## Interactivity

**React**: All components re-execute on state change from interactivity
**Solid** or **Qwik**: Only execute at the event handle

Imagining a simple app where Counter is the parent and Display/Increment are children that display and update parent state:
![https://www.builder.io/blog/resumability-vs-hydration?ck_subscriber_id=1441143038#client-side-rendering](/assets/images/2023-02-13-20-59-56.png)

## Resumability

Qwik uses 'resumability' as opposed to hydration which is a way to recover state without re-executing the application components on the client. This is done by serializing everything required e.g. html and event listeners, for the client to resume where the server left off.
