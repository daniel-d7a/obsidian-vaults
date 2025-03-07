#sources/articles/tk_dodo #react/hooks
## References

- [article link](https://tkdodo.eu/blog/dont-over-use-state](https://tkdodo.eu/blog/dont-over-use-state)
- [[Readings & Studying]]

Is it passed in from a parent via props? If so, it probably isn’t state. Does it remain unchanged over time? If so, it probably isn’t state. Can you compute it based on any other state or props in your component? If so, it isn’t state.

Effects shouldn't be used to sync state, they should be used to sync react with external resources.

If data should be only based on state, it should be computed, not set inside a state. Whenever a state setter function is only used synchronously in an effect, get rid of the state!

