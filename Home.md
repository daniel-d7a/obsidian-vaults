## What topics do I have?
```dataview
TABLE  WITHOUT ID file.link as "Note", length(file.inlinks) as "connections"
FROM "1- MOCs"
```

## How many notes do I have?
we have `$=dv.pages("").length` notes

## How many notes need my attention?
Incomplete: `$=dv.pages('"_/_Inbox"').length`
Unorganized: `$=dv.pages('"2- Fleeting"').length`
## Some random topics
```dataview
TABLE WITHOUT ID file.link as "Note", file.mday as "Last Modified"
FROM ""
SORT hash(dateformat(date(today), "YYYY-MM-DD HH:mm"), file.name)
LIMIT 5
```
