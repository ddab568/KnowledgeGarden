
## Concurrent Rendering

A behind-the-scenes mechanism introduced in React 18 in order to render more seamlessly.

Before React 18, rendering was a synchronous transaction meaning that once rendering started it could not be interrupted. React 18 introduces features such as suspense and stream server rendering meaning rendering can be interrupted, paused, resumed or abandoned.

The problem with synchronous rendering is that while a component is re-rendering, the rest of the app becomes unresponsive until it's complete since main thread is blocked. If we picture this being a list that is updated each time the user changes input and the list takes a while to re-render, the other components must wait until it completes making it a janky user experience.

## Automatic Batching

## Transitions

## New Suspense Features

## New Client and Server Rendering API

## New Strict Mode Behaviors

## New Hooks
