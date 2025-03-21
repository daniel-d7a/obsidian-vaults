
pc test
## My to-do list for now

- [ ] last 4 hfooad videos at least
- [ ] work on 2 typescript videos
- [ ] work on 1 article
- [ ] play some games
- [ ] get the backend roadmap for Mazen
- [ ] quran for today
- [ ] surat al-kahf
---

## What topics do I have?

```dataview
TABLE  WITHOUT ID file.link as "Note", length(file.inlinks) as "connections"
FROM "1- MOCs"
```

---

## How many notes do I have? `$=dv.pages("").length`

## How many notes need my attention?

## Incomplete: `$=dv.pages('"_/_Inbox"').length`

## Unorganized: `$=dv.pages('"2Fleeting"').length`

---

## Some random topics

```dataview
TABLE WITHOUT ID file.link as "Note", file.mday as "Last Modified"
FROM ""
SORT hash(dateformat(date(today), "YYYY-MM-DD HH:mm"), file.name)
LIMIT 5
```
