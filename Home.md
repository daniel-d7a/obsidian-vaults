## What topics do I have?
```dataview
TABLE length(file.inlinks) as "connections"
FROM "1- MOCs"
```

## How many notes do I have?
we have `$=dv.pages("").length` notes

## How many notes need my attention?
Incomplete: `$=dv.pages('"_/_inbox"').length`
Unorganized: `$=dv.pages('"2- fleeting"').length`

## Some random topics
```dataview
TABLE file.mtime as "Last Modified"
FROM ""
SORT rand()
LIMIT 10
```