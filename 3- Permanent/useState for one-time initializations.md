#sources/articles/tk_dodo #react/hooks 
## references
- [article link](https://tkdodo.eu/blog/use-state-for-one-time-initializations)
- [[Readings & Studying]]

Suppose you have a resource that you only want to initialize once per life-time of your app. The recommended pattern is usually to create the instance outside of the component.  

If we need multiple components each with its own resource we have a few options:  

1. Creating the resource inside the component  
This will re-create the resource each time the component is re-rendered, and we shouldn't rely on the component not re-rendering  
  
2. Using useMemo  
This gives us performance optimization, not a guarantee that the resource will not be re-created.  
  
3. Using state  
This will guarantee the resource will not be re-created unless the setter is called, and since we don't want that we can simply ignore the setter and not destructure it. (Plus using lazy initialization helps even more)  

```ts
const Component = () => {
  // ✅ truly stable
  const [resource] = React.useState(() => new Resource())
  return (
    <ResourceProvider resource={resource}>
      <App />
    </ResourceProvider>
  )
}
```

4. Using a ref  
Similar to the state solution but a bit verbose, and will have the probability of being undefined in typescript.

```ts
const Component = () => {
  // ✅ also works, but meh
  const resource = React.useRef(null)
  if (!resource.current) {
    resource.current = new Resource()
  }
  return (
    <ResourceProvider resource={resource.current}>
      <App />
    </ResourceProvider>
  )
}
```
