Below is a cheat sheet I compiled when reacquainting myself with React after a few years away - hope it helps!
## Hooks
### State Hooks
#### useState
Note the state is defined as an array and NOT an object:
```js
let [thisState, setThisState] = useState('initial value')
```

#### useEffect
```js
useEffect((prevProps) => {
	// callback function
}, [deps])
```
the `deps` can be:
- omitted: useEffect runs on every change of state in the component (shouldn't be needed)
- empty array `[]`: useEffect runs one on componentMount (only need one per component, where required)
- array of one or more state objects `[thisState]`: runs when that state object is updated (used for processing external data)

An alternative to using useEffect is to pass a callback function to child components, and in there perform the updates required.
### Context Hooks
#### useContext
_Context_ lets a component [receive information from distant parents without passing it as props.](https://react.dev/learn/passing-props-to-a-component)

##### Establishing context (i.e. router, theme etc.)
```js
function MyPage() {  
	return (
		<ThemeContext.Provider value="dark">
			<p>Page content</p>
		</ThemeContext.Provider>  

	);  
}
```

##### Fetching context
```js
import { useContext } from 'react';  

function Button() {  
	const theme = useContext(ThemeContext);
	...
```

React finds the closest parent context provider, so it's possible to override context at different levels in your app.
It DOES NOT look in the current component, only above.

##### Specify a default value
```js
import { createContext } from 'react';

const ThemeContext = createContext('light');
```
##### Performance concerns
Values passed to context providers are considered the same as props, and will update on any re-renders. e.g.
```js
function MyApp() {  
	const [currentUser, setCurrentUser] = useState(null);  
	
	function login(response) {  
		storeCredentials(response.credentials);  
		setCurrentUser(response.user);  
	}  

	return (  
		<AuthContext.Provider value={{ currentUser, login }}>  
			<Page />  
		</AuthContext.Provider>  
	);
}

```
Any components that `useContext(AuthContext)` will get a new copy of the `login` function whenever `currentUser` or the route updates.

To combat this, wrap the function in `useCallback`, and provide it via `useMemo` e.g.[uke]()
```js
import { useCallback, useMemo } from 'react';  

function MyApp() {  
	const [currentUser, setCurrentUser] = useState(null);  

	const login = useCallback((response) => {  
		storeCredentials(response.credentials);  
		setCurrentUser(response.user);  
	}, []);  

	const contextValue = useMemo(() => ({  
		currentUser,  
		login  
	}), [currentUser, login]);  

	return (  
		<AuthContext.Provider value={contextValue}>  
			<Page />  
		</AuthContext.Provider>  
	);  
}
```
By wrapping in `useMemo` and providing dependencies (`currentUser` and `login`), the `contextValue` only updates when `currentUser` does (as `login` is static).

N.B. prop on Provider tag should always be `value` and not a custom prop.

### Effect Hooks
Used to synchronise React with an external system.
Don't use them to:
- transform data for rendering
- handle user events

### Performance Hooks
- [`useCallback`](https://react.dev/reference/react/useCallback) lets you cache a function definition before passing it down to an optimised component.
- [`useMemo`](https://react.dev/reference/react/useMemo)lets you cache the result of an expensive calculation (and ensure recalculations are contingent on dependencies being updated)

Sometimes, you can’t skip re-rendering because the screen actually needs to update. In that case, you can improve performance by separating blocking updates that must be synchronous (like typing into an input) from non-blocking updates which don’t need to block the user interface (like updating a chart).

To prioritise rendering, use one of these Hooks:

- [`useTransition`](https://react.dev/reference/react/useTransition) lets you mark a state transition as non-blocking and allow other updates to interrupt it.
- [`useDeferredValue`](https://react.dev/reference/react/useDeferredValue) lets you defer updating a non-critical part of the UI and let other parts update first.

## Rendering
### conditional JSX
```js
{isTrue &&
	<>
		<h1>hi</h1>
		<p>hello</p>
	</>
}
```

JSX always needs to be wrapped in a single element, so multiple elements can't exist in a new JSX block. This includes conditionally rendered blocks, so you need to wrap them in a fragment. `<>` is the short syntax for a fragment. In older versions of React this is short for `<React.fragment>`. Now you use simply `<Fragment>`.

To use `<Fragment>`, it needs to be imported:
```js
import { Fragment } from 'react';
```

If you need to add a key to your fragment, you need to use the long form:
`<React.Fragment key={item.id}>`