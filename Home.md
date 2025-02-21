What topics do I have?
```dataview
TABLE length(file.inlinks) as "connections"
FROM "1- MOCs"
```

How many notes do I have?
we have `= list length(file.name)`

How many notes need my attention?
Incomplete: `get number of fleeting notes`
Unorganized: `get number of inbox notes`

Some random topics
`get 10 random notes here`