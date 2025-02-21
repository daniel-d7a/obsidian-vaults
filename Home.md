What topics do I have?
```dataview
TABLE length(file.inlinks) as "connections"
FROM "1- MOCs"
```

How many notes do I have?
we have 
``` dataview
list link("")
limit 1
```

How many notes need my attention?
Incomplete: `=length(link(""))`
Unorganized: `get number of inbox notes`

Some random topics
`get 10 random notes here`