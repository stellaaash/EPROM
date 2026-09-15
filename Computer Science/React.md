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