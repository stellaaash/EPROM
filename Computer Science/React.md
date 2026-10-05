---
tags:
  - framework
  - web/frontend
---



# Core Concepts
## Context
Context is useful to pass information down to components without having to drill props through layers and layers or components.
You create a component that will provide the context, and you wrap it around components that need it.
Then, the components will use the `useContext` hook to get the content of your context.
## Effect
Effects should be used only when needing to sync with an external system, like your application's backend.
## State
State is isolated between components. You can control when to preserve state and when to reset it between re-renders.
State is inherently tied to how React creates its render tree, because the component's position in the render tree **is how React remembers which state is which component's**. React will keep the state around for as long as you render the same component at the same position in the tree.
When React removes a component, it destroys its state.
React doesn't know the structure you have in your JSX, only the tree you return. If you have an if statement that might return a component with different props, if its the same component, the state will be shared, because the place in the tree will be the same.