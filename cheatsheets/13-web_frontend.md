# Web Frontend

## HTML5

  - Canvas:
  - Drag & Drop:
  - Geolocation:
  - Notification:
    - The Notifications API allows displaying notifications to the user for given events, both passively and on user interactions.
  - Server-Sent Events
  - Web Socket:
    - WebSocket protocol defines an API establishing a persistent full-duplex (bidirectional) connection between a web browser and a server.
  - Web Worker:
    - WebWorker is a JavaScript running in the background, without affecting the performance of the page.


## Single-Page Applications

  - React
  - Vue
  - Ember
  - Angular
  - AngularJS

### React

  - *Unidirectional* data flow
  - **JSX**
    - Syntax extension to JavaScript
    - JSX is an Expression: JavaScript function calls that evaluate to objects
  - **Component**
    - *Function Components* vs. *Class Components*
    - **Props**
      - A component never modify its own props.
      - All React components must act like pure functions with respect to their props.
    - **State**
      - Do not modify state directly.
        - Use `setState({ ... }) or setState((state, props) => ...`
      - State updates may be asynchronous or/and batched.
      - State updates are merged.
    - **Hooks**
      - Hooks let you use more of React's features without classes.
      - Hooks allow reusing stateful logic (not state itself) without changing the component hierarchy. 
      - Hooks are functions that hook into React state and lifecycle features from function components.
      - Built-in Hooks:
        - `useState()`
        - `useEffect()`
        - `useContext()`
        - `useReducer()`
        - `useCallback()`
      - Custom Hooks are a convention in which a function's name starts with `use` and it calls other Hooks.
      - Rules:
        - Only call Hooks at the top level.
        - Only call Hooks from React function components.
    - *Lifecycle Methods*
      - Mounting
        - `constructor()`, `render()`, `componentDidMount()`
      - Updating
        - `shouldComponentUpdate()`, `render()`, `componentDidUpdate()`
      - Unmounting
        - `componentWillUnmount()`
      - Error Handling
        - `componentDidCatch()`
    - Cross-Cutting Concerns
      - *Render Props*
        - Sharing code between React components using a prop whose value is a function.
      - *Higher-Order Components*
        - A a pure function with zero side-effects that takes a component and returns a new component.
  - Tools:
    - create-react-app
    - react-devtools

### Redux

  - *One-way* data flow
  - State Management
    - **Actions**
      - An action is a plain JavaScript object that has a type field (a descriptive name).
      - An action object can have other fields with additional information (payload, etc.).
      - An action creator is a function that creates and returns an action object.
    - **Reducers**
      - `(state, action) => newState`
      - A reducer is a function that receives the current state and an action object.
      - It decides how to update the state if necessary and returns the new state.
    - **Store**
      - API: `subscribe`, `dispatch`, `getState`
      - The Redux application state lives in an object called the store.
      - Selectors are functions to extract specific pieces of information from a store state.
  - **Immutability**
    - Redux expects that all state updates are done immutably.
    - Objects and arrays must be copied and then modified.
  - Tools:
    - redux-toolkit
    - react-redux
    - redux-devtools-extensions


## Progressive Web Applications

  - Web App Manifest
  - Web Workers
    - Dedicated Workers
    - Shared Workers
    - Service Workers
  - Storage
    - CacheStorage
    - Web Storage
      - localStorage
      - sessionStorage
    - IndexedDB
  - Background Sync
  - Web Push Notifications


## Cross-Origin Resource Sharing (CORS)

  - Simple Requests
    - Methods:
      - GET
      - HEAD
      - POST
    - Headers:
      - Accept
      - Accept-Language
      - Content-Language
      - Content-Type
        - text/plain
        - multipart/form-data
        - application/x-www-form-urlencoded
  - Preflighted Requests
    - Methods:
      - PUT
      - PATCH
      - DELETE
      - TRACE
      - OPTIONS
      - CONNECT
    - Or any Header other than:
      - Accept
      - Accept-Language
      - Content-Language
      - Content-Type
    - Or any Content-Type other than:
      - text/plain
      - multipart/form-data
      - application/x-www-form-urlencoded

