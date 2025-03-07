## My to-do list for now

- [ ] 3 hfooad videos at least
- [ ] 2 typescript videos
- [ ] 1 article
- [ ] type out my saas idea into obsidian
- [ ] play some games
- [x] get the books
- [ ] get the courses
- [x] get some more games
- [ ] organize obsidian some more
- [ ] quran for today
- [x] surat al-kahf
- [ ] work on my blog some more
- [ ] start the saas monorepo
- [ ] draw the database diagram

## What topics do I have?

```dataview
TABLE  WITHOUT ID file.link as "Note", length(file.inlinks) as "connections"
FROM "1- MOCs"
```

## How many notes do I have?

we have `$=dv.pages("").length` notes

## How many notes need my attention?

Incomplete: `$=dv.pages('"_/_Inbox"').length`

Unorganized: `$=dv.pages('"2Fleeting"').length`

## Some random topics

```dataview
TABLE WITHOUT ID file.link as "Note", file.mday as "Last Modified"
FROM ""
SORT hash(dateformat(date(today), "YYYY-MM-DD HH:mm"), file.name)
LIMIT 5
```
