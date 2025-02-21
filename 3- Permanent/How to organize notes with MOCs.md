#notes

Use this dataview query in an index note to list all notes referring to it, and in any note related to the topic add a link to the index note.

```dataview
list from [[]] and !outgoing([[]])
```

This creates a list of all notes referring to the current - aka the index - note.

> *There are still somethings I don't understand about this query.*

We can further refine our index by dividing it into topics using subheaders and more specific queries.

## References

- [[How to take better Notes]]
