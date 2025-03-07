#sources/articles/tk_dodo #react/hooks 
## refernces
- [article link](https://tkdodo.eu/blog/use-state-vs-use-reducer)
- [[Readings & Studying]]

If we have separately changing state it should be stored separately.  

If we have state that changes together it should be stored together, e.g. mouse x & y.  

For form state a single state is best, since they live and update together, a custom hook is advised  

```ts
const useForm = <State extends Record<string, unknown>>(
  initialState: State
) => {
  const [values, setValues] = React.useState(initialState)
  const update = <Key extends keyof State>(name: Key, value: State[Key]) =>
    setValues((form) => ({ ...form, [name]: value }))

  return [values, update] as const
}
```

Storing state together is better for batching state updates, especially in async functions.  

## useReducer  

Could be used to trigger force updates before useSyncExternalStore was a thing, toggling boolean values, and updating state the is dependant on each other.  

Keep all the logic inside the reducer by modeling actions as events instead of setters  

By making the reducer a higher order function you can pass it any external data and have the latest data in your reducer  

```ts
const reducer = (data) => (state, action) => {
  // ✅ you'll always have access to the latest
  // server state in here
}

function App() {
  const { data } = useQuery(key, queryFn)
  const [state, dispatch] = React.useReducer(reducer(data))
}
```

this will re-create the reducer function every time the data prop changes (as it is a normal function) and passed the new value of data.
